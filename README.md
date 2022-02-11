# python-helloworld
## Argo CD installation 
### 1. start virtual box vm with vagrant up
### 2. rke up
### 3. export KUBECONFIG=./kube_config_cluster.yml
### 4. deploy argo cd
```
# deploy ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
### 5. Create the NodePort service for ArgoCD server 
```
kubectl apply -f argocd/argocd_server_load_balance.yml
```
### 6. Argoc CD login credentials: user name = admin. Please get be retrieved from following link:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```