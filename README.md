# python-helloworld repo for demo of cloud native CI/CD with github actions and argo cd
## Github Actions
### 1. Push anything to any branch and observe the job running in github actions, there are three examples under .github/woprkflows folder

## Argo CD Setup 
### 1. start virtual box vm
```
vagrant up
```
### 2. start cluster
```
rke up
```
### 3. Copy ssh key to vagrant box
```
ssh-keygen -t rsa -b 2048
sudo ssh-copy-id -i ~/.ssh/id_rsa root@192.168.56.11
```
### 4. Setup KUBECONFIG environment so that so you don't need to include in kubectl command everytime
```
export KUBECONFIG=./kube_config_cluster.yml
```
### 5. deploy argo cd
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
### 6. Create the NodePort service for ArgoCD server 
```
kubectl apply -f argocd/argocd_server_load_balance.yml
```
### 7. Argoc CD login credentials: user name = admin. Password can be retrieved from following command:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
### 8. Open https://192.168.56.11:30008 for gocd web UI
### 9. Once logged into ArgoCD server, application can be created using command:
```
kubectl apply -f argocd/argo_python.yml
```
### 10. Visit helloworld python app
```
http://192.168.56.11:30009/
```

