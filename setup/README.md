# Argo Setup

## ArgoCD

`kubectl create namespace argocd`

`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`

Ingress

`kubectl apply -f argocd.ingress.yaml`

Admin password

`kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`

## Argo Rollouts

`kubectl create namespace argo-rollouts`

`export version=v1.7.2`

`kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/download/$version/install.yaml`

Dashboard

`kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/download/$version/dashboard-install.yaml`

`kubectl apply -f argo-rollouts.ingress.yaml`

## Deploy Application

Blue Green

`argocd app create blue-green-app -f blue-green.application.yaml`

Canary

`argocd app create canary-app -f canary.application.yaml`