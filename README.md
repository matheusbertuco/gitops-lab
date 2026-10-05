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

## Desabilitar HTTPS do ArgoCD
kubectl patch configmap argocd-cmd-params-cm -n argocd \
  --type merge \
  -p '{"data":{"server.insecure":"true"}}'

kubectl rollout restart deployment argocd-server -n argocd

## Senha inicial do ArgoCD
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath='{.data.password}' | base64 --decode
echo