# Argo CD
Argocd 

Implemented in the GKE 
#### Works well on GKE 
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl create clusterrolebinding kunal-cluster-admin-binding --clusterrole=cluster-admin --user=kunal
```

#### Change argocd-server service from ClusterIP to LB 
```kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```
#### Get password - Here pod name of argcod-server is the default password for admin user 
```kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
```
#### Login into argocd 
```kubectl exec -it argocd-server-POD_NAME -n argocd -- /bin/bash
argocd login <ARGOCD_SERVER> => IP address of the LB 
Username: admin
Password: default-password
```
#### Update Password of argocd 
```argocd account update-password
```
