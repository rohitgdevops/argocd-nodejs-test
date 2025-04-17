# argocd-nodejs-test

Commands
Install Kind:
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

Install Kubectl
curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
sudo mv kubectl /usr/local/bin/

Create Cluster
cat <<EOF > kind-config.yaml
# kind-config.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
EOF

kind create cluster --name mycluster --config kind-config.yaml

 kubectl create namespace argocd
  kubectl get ns
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  kubectl get all -n argocd
  sudo lsof -i 8080
  sudo ss -tuln | grep :8080
  kubectl port-forward service/argocd-server -n argocd 8080:443

  kubectl -n argocd get secret argocd-initial-admin-secret           -o jsonpath="{.data.password}" | base64 -d; echo

  Install helm    
  curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
   33  chmod 700 get_helm.sh
   34  ./get_helm.sh

   helm repo add stable https://charts.helm.sh/stable
   37  help repo update
