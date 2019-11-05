# helm.estafette.io

Welcome at the official Helm repository for Estafette.

To start using helm charts from this repository run the following command

```bash
helm repo add estafette https://helm.estafette.io
```

From here on you can install or upgrade helm charts as follows

```bash
helm upgrade --install estafette-cloudflare-dns estafette/estafette-cloudflare-dns --namespace estafette
helm upgrade --install estafette-letsencrypt-certificate estafette/estafette-letsencrypt-certificate --namespace estafette
helm upgrade --install estafette-gke-preemptible-killer estafette/estafette-gke-preemptible-killer --namespace estafette
helm upgrade --install estafette-k8s-hpa-scaler estafette/estafette-k8s-hpa-scaler --namespace estafette
```

## charts

| Chart         | Description   |
| ------------- | ------------- |
| [estafette-cloudflare-dns](https://github.com/estafette/estafette-cloudflare-dns) | Kubernetes controller to set and update dns records in Cloudflare for annotated services and ingresses |
| [estafette-letsencrypt-certificate](https://github.com/estafette/estafette-letsencrypt-certificate) | Kubernetes controller to retrieve and renews tls certificates from Letsencrypt for annotated Kubernetes secrets |
| [estafette-gke-preemptible-killer](https://github.com/estafette/estafette-gke-preemptible-killer) | Kubernetes controller to spread preemption for preemtible VMs in GKE to avoid mass deletion after 24 hours |
| [estafette-k8s-hpa-scaler](https://github.com/estafette/estafette-k8s-hpa-scaler) | Kubernetes controller to set minimum replicas from a Prometheus query on annotated HorizontalPodAutoscalers to avoid collapsing deployments in case of errors |