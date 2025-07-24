# Hydra

Hydra is Constellation's resident Kubernetes cluster. 
It runs the majority of Constellation's software stack, acting as the general compute resource for the system.

## Infrastructure

These deployments are critical to the cluster's operation. 
It includes services like:

- [Traefik](infrastructure/traefik/README.md), the cluster's ingress controller
- [MetalLB](infrastructure/metallb/README.md), which provides virtual IPs via ARP to LoadBalancer services
- [Cert Manager](infrastructure/cert-manager/README.md), which issues SSL certificates for the cluster's ingress routes
- [Sealed Secrets](infrastructure/sealed-secrets/README.md), which allows Kubernetes Secrets to be encrypted while stored in a Git repository

## Applications

These deployments are not critical to the cluster's operation. 
Services like Prometheus exporters, Grafana and other monitoring tools, while important to the cluster, are not critical infrastructure and so fall under the applications category.