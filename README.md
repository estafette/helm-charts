# helm.estafette.io

Welcome at the official Helm repository for Estafette.

To start using helm charts from this repository run the following command

```bash
helm repo add estafette https://helm.estafette.io
```

From here on you can install or upgrade helm charts as follows

```bash
helm upgrade --install estafette-cloudflare-dns estafette/estafette-cloudflare-dns --namespace estafette
```

## charts

| Chart         | Description   |
| ------------- | ------------- |
| [estafette-cloudflare-dns](https://github.com/estafette/estafette-cloudflare-dns) | Kubernetes controller to set and update dns records in Cloudflare for annotated services and ingresses |