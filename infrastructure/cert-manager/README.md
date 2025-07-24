# Cert Manager

[Cert Manager](https://cert-manager.io) automatically provisions SSL certificates for the cluster's ingress routes.
It provides all services exposed via [Traefik](https://traefik.io) with a certificate from [Let's Encrypt](https://letsencrypt.org).

## Why not use Traefik's built-in ACME client?

As per the [docs](https://doc.traefik.io/traefik/providers/kubernetes-ingress/#letsencrypt-support-with-the-ingress-provider), Traefik's built-in ACME client doesn't support High-Availability environments.
Since Traefik handles the entire cluster's ingress, it is critical infrastructure, and so needs to be Highly Available.

Additionally, Cert Manager is a lot more feature-rich and can be used for services outside Traefik. 

## Why the DNS01 challenge?

While Cert Manager has great support for both `http01` and `dns01` challenges, `dns01` is more reliable for my use-case.
This is because `dns01` only relies on having a good connection with the Cloudflare API, while `http01` requires the cluster to be accessible from the internet, where there a number of potential points of failure.
It would also require me to have an ingress controller already in place, even though the ingress controller I'm using relies on Cert Manager working, creating an unnecessary cyclic dependency.

Additionally, the `dns01` challenge allows wildcard certificates.

## Why not use a static certificate?

While I could easily generate some certificates with Cloudflare and pass them to Traefik manually, this is not as cool.
Cert Manager completely automates the process of renewing certificates, reduces the amount of stuff I need to manually add to the cluster and makes me feel really smart all in one go.

## Why use a ClusterIssuer?

Because the majority of certificate requests will be for the same domain, so there's no point in having to specify the configuration multiple times.

In the rare exceptions where other domains may be used, I will create scoped Issuers within the namespaces they're needed.

## How are certificates requested?

Certificates are requested by adding an annotation to the Ingress resource, rather than directly through Traefik.
This allows Ingress resources to use different Issuers if needed, while still using the same Traefik configuration.