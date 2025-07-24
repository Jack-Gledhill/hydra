# Sealed Secrets

[Sealed Secrets](https://github.com/bitnami-labs/sealed-secrets) allows Kubernetes Secrets to be encrypted while stored in a Git repository, and decrypted when applied to the cluster.

## Accessing the public key

Sealed Secrets has a web server built into it that exposes the current public key which can be used to encrypt secrets.
This server is exposed via [Traefik](https://traefik.io) to https://hydra.starsystem.dev/v1/cert.pem.

Thus, you can seal a secret simply by running:
```bash
kubeseal --cert https://hydra.starsystem.dev/v1/cert.pem -f secret.yml -w sealed-secret.yml
```

**Note:** you're likely to get an SSL warning from this URL. That's because [Cert Manager](https://cert-manager.io) relies on Sealed Secrets to issue certificates, so this route does not have a certificate.