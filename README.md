
Welcome at the official Helm repository for Estafette.

## Installation

To start using the Helm charts from this repository run the following command

```bash
helm repo add estafette https://helm.estafette.io
```

To update and view all available charts in the repository run

```bash
helm repo update estafette
helm search estafette
```

From here on you can install or upgrade helm charts as follows

```bash
helm upgrade --install estafette-cloudflare-dns estafette/estafette-cloudflare-dns --namespace estafette --wait
helm upgrade --install estafette-letsencrypt-certificate estafette/estafette-letsencrypt-certificate --namespace estafette --wait
helm upgrade --install estafette-gke-preemptible-killer estafette/estafette-gke-preemptible-killer --namespace estafette --wait
helm upgrade --install estafette-k8s-hpa-scaler estafette/estafette-k8s-hpa-scaler --namespace estafette --wait
helm upgrade --install estafette-gcp-service-account estafette/estafette-gcp-service-account --namespace estafette --wait
```

## Local testing

If you'd like to test these Helm charts on your local machine first, follow the instructions below.

Prepare your Mac to run minikube with the following steps

```bash
brew install hyperkit
brew install kubernetes-helm
brew install minikube
```

Start minikube and configure Helm

```bash
minikube start --disk-size=50gb --memory=16gb --extra-config=apiserver.authorization-mode=RBAC
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default
kubectl -n kube-system create serviceaccount tiller
kubectl create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller --wait
```

From here on you can follow the steps as documented in the installation section above.

# Charts

| Chart         | Description   |
| ------------- | ------------- |
| [estafette-cloudflare-dns](https://github.com/estafette/estafette-cloudflare-dns) | Kubernetes controller to set and update dns records in Cloudflare for annotated services and ingresses |
| [estafette-letsencrypt-certificate](https://github.com/estafette/estafette-letsencrypt-certificate) | Kubernetes controller to retrieve and renews tls certificates from Letsencrypt for annotated Kubernetes secrets |
| [estafette-gke-preemptible-killer](https://github.com/estafette/estafette-gke-preemptible-killer) | Kubernetes controller to spread preemption for preemtible VMs in GKE to avoid mass deletion after 24 hours |
| [estafette-k8s-hpa-scaler](https://github.com/estafette/estafette-k8s-hpa-scaler) | Kubernetes controller to set minimum replicas from a Prometheus query on annotated HorizontalPodAutoscalers to avoid collapsing deployments in case of errors |
| [estafette-gcp-service-account](https://github.com/estafette/estafette-gcp-service-account) | Kubernetes controller to fetch GCP service account keyfiles for annotated secrets |