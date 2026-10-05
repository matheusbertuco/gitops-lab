# gitops-lab

## Instalação Kind
kind create cluster --config ./kind/kind-config.yaml 

## Removendo Kind
kind delete cluster --name <NOME>

## Instalação ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd --server-side --force-conflicts \
  -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## Controlador Envoy Gateway
kubectl apply -f infrastructure/envoy-gateway/application.yaml

## ArgoCD acompanhar rotas
kubectl apply -f bootstrap/gateway-routes-app.yaml