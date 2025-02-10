# LinuxWorld_Project
#DevOps project

Create Kubernetes Cluster
```
eksctl create cluster --name devopsproj
```
Create a namespace for ArgoCD
```
kubectl create namespace argocd
```
Apply the ArgoCD installation manifest:

```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
Set the current namespace to argocd:
```
kubectl config set-context --current --namespace=argocd
```
Login to ArgoCD with the admin account:
```
argocd login --core
```
Retrieve the initial admin password:
```
argocd admin initial-password -n argocd
```
Forward port 8080 to access the ArgoCD UI:
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Access ArgoCD at https://127.0.0.1:8080.

![Screenshot (22)](https://github.com/user-attachments/assets/5e77346e-2639-4411-bb4b-08c19d6a8844)


Initialize a new Git repository and push it to GitHub
```
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/Omprakashkumar01/devops_project.git
git push -u origin master
```

Download the bookinfo.yaml file:

```
curl https://raw.githubusercontent.com/Omprakashkumar01/devops_project/refs/heads/main/bookinfo.yaml  -o bookinfo.yaml
```
Add and push updates
```
git add .
git commit -m first .
git push
```
Deploy the resources from the YAML file
```
kubectl apply -f bookinfo.yaml
```
Verify the pods:
```
kubectl get pods -n default
```
Forward the productpage service port:
```
kubectl port-forward  svc/productpage  -n default  80:9080
```

http://127.0.0.1/productpage
![Screenshot (58)](https://github.com/user-attachments/assets/bd04ea2c-d73f-409a-bf62-39feeb4fdc15)


Install Istio using the demo profile:

```
istioctl  install --set profile=demo
```
Verify Istio installation:
```
kubectl get pods -n istio-system
kubectl get svc  -n istio-system
```
Enable automatic sidecar injection for the default namespace:
```
kubectl label namespace default  istio-injection=enabled
```
Restart pods in the namespace to apply injection:
```
kubectl delete pods  --all -n default
kubectl get pods -n default
```
Apply the gateway configuration:
```
kubectl apply -f bookinfo-gateway.yaml
```
adding yaml files
```
kubectl.exe apply -f addons/
kubectl get pods -n istio-system
```
Verify gateway and virtual service:
```
kubectl get svc -n istio-system
kubectl get gateway -n default
kubectl get vs -n default
```
Install Kiali via Helm:
```
helm repo add kiali https://kiali.org/helm-charts
helm repo update
```
Access monitoring dashboards:
Kiali:
```
kubectl port-forward -n istio-system svc/kiali 20001:20001
```
![Screenshot (62)](https://github.com/user-attachments/assets/6cb02809-5b2e-4959-96ce-c69675f0a10f)

Access at http://127.0.0.1:20001.

Prometheus:
```
kubectl port-forward -n istio-system svc/prometheus 9090:9090
```
![Screenshot (64)](https://github.com/user-attachments/assets/e06ab53d-b47b-4bb0-af5c-76ee2256c829)

Access at http://127.0.0.1:9090.

Grafana
```
kubectl port-forward -n istio-system svc/grafana 3000:3000
```
Access at http://127.0.0.1:3000.
![Screenshot (66)](https://github.com/user-attachments/assets/54e63269-fa89-49f4-9090-03cf74a592e2)
