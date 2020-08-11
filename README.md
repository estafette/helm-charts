
Welcome at the official Helm repository for Estafette.

## Installation

To start using the Helm charts from this repository run the following command

```bash
helm repo add estafette https://helm.estafette.io
```

To update and view all available charts in the repository run

```bash
helm repo update estafette
helm search repo estafette
```

From here on you can install or upgrade helm charts as follows

```bash
helm upgrade --install estafette-cloudflare-dns estafette/estafette-cloudflare-dns --namespace estafette --wait
helm upgrade --install estafette-letsencrypt-certificate estafette/estafette-letsencrypt-certificate --namespace estafette --wait
helm upgrade --install estafette-gke-preemptible-killer estafette/estafette-gke-preemptible-killer --namespace estafette --wait
helm upgrade --install estafette-k8s-hpa-scaler estafette/estafette-k8s-hpa-scaler --namespace estafette --wait
helm upgrade --install estafette-gcp-service-account estafette/estafette-gcp-service-account --namespace estafette --wait
helm upgrade --install estafette-gcloud-quota-exporter estafette/estafette-gcloud-quota-exporter --namespace estafette --wait
helm upgrade --install estafette-google-cloud-dns estafette/estafette-google-cloud-dns --namespace estafette --wait
helm upgrade --install estafette-gcloud-mig-scaler estafette/estafette-gcloud-mig-scaler --namespace estafette --wait
helm upgrade --install estafette-gke-node-pool-shifter estafette/estafette-gke-node-pool-shifter --namespace estafette --wait
helm upgrade --install estafette-vulnerability-scanner estafette/estafette-vulnerability-scanner --namespace estafette --wait
helm upgrade --install estafette-k8s-node-compactor estafette/estafette-k8s-node-compactor --namespace estafette --wait
helm upgrade --install k8s-node-termination-handler estafette/k8s-node-termination-handler --namespace kube-system --wait
```

## Local testing

If you'd like to test these Helm charts on your local machine first, follow the instructions below.

Prepare your Mac to run minikube with the following steps

```bash
brew install minikube
brew install hyperkit
brew install kubernetes-helm
```

Configure some defaults for minikube (optional)

```bash
minikube config set vm-driver hyperkit
minikube config set cpus 2
minikube config set memory 16384
minikube config set disk-size 50gb
```

Start minikube with RBAC enabled and configure Helm

```bash
minikube start --extra-config=apiserver.authorization-mode=RBAC
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default
kubectl -n kube-system create serviceaccount tiller
kubectl create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller --wait
```

From here on you can follow the steps as documented in the installation section above.

# Charts

| Chart                                                                                               | Description                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [estafette-cloudflare-dns](https://github.com/estafette/estafette-cloudflare-dns)                   | Kubernetes controller to set and update dns records in Cloudflare for annotated services and ingresses                                                                 |
| [estafette-letsencrypt-certificate](https://github.com/estafette/estafette-letsencrypt-certificate) | Kubernetes controller to retrieve and renews tls certificates from Letsencrypt for annotated Kubernetes secrets                                                        |
| [estafette-gke-preemptible-killer](https://github.com/estafette/estafette-gke-preemptible-killer)   | Kubernetes controller to spread preemption for preemtible VMs in GKE to avoid mass deletion after 24 hours                                                             |
| [estafette-k8s-hpa-scaler](https://github.com/estafette/estafette-k8s-hpa-scaler)                   | Kubernetes controller to set minimum replicas from a Prometheus query on annotated HorizontalPodAutoscalers to avoid collapsing deployments in case of errors          |
| [estafette-gcp-service-account](https://github.com/estafette/estafette-gcp-service-account)         | Kubernetes controller to fetch GCP service account keyfiles for annotated secrets                                                                                      |
| [estafette-gcloud-quota-exporter](https://github.com/estafette/estafette-gcloud-quota-exporter)     | Prometheus exporter to turn Google Cloud quota into Prometheus timeline series                                                                                         |
| [estafette-google-cloud-dns](https://github.com/estafette/estafette-google-cloud-dns)               | Kubernetes controller to update dns record in a Google Cloud DNS zone for annotated services and ingresses                                                             |
| [estafette-gcloud-mig-scaler](https://github.com/estafette/estafette-gcloud-mig-scaler)             | Controller to scale a Google Cloud managed instance groups based on request rate retrieved from Prometheus                                                             |
| [estafette-gke-node-pool-shifter](https://github.com/estafette/estafette-gke-node-pool-shifter)     | Kubernetes controller that can shift nodes from one node pool to another, to favour for example preemptibles over regular vms                                          |
| [estafette-vulnerability-scanner](https://github.com/estafette/estafette-vulnerability-scanner)     | Kubernetes controller to scan any used container image in a cluster for vulnerabilities                                                                                |
| [estafette-k8s-node-compactor](https://github.com/estafette/estafette-k8s-node-compactor)           | Kubernetes controller to assist Cluster Autoscaler in compacting nodes more efficiently                                                                                |
| [k8s-node-termination-handler](https://github.com/estafette/k8s-node-termination-handler)           | Helm chart for [Google's k8s-node-termination-handler](https://github.com/GoogleCloudPlatform/k8s-node-termination-handler) to cleanly shutdown preempted preemptibles |