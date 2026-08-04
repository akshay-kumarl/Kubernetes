## Installation ArgoCD 

Install argoCD through ArgoCD Documentation 

#### A simple way to access 

> kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 0.0.0.0 &

#### via LB also we can access but you need to run it on a cloud platform
go to 
> kubectl edit svc argocd-server -n argocd

> Then change clusterIP to NodePort or LodeBalancer service and save

> If using nodeport then follow the below command<br/>
> minikube service argocd-server -n argocd


#### to get the password follow the below commands 
> kubectl get secret -n argocd<br/>
> kubectl edit secret argocd-initial-admin-secret -n argocd<br/>
> echo cVY2RTBPRElrVEtqZGdabA== | base64 --decode 

CLI is also there<br/>
argocd command refernce type in google 

For reference watch the below video <br/>
https://www.youtube.com/watch?v=ZgJQG475oME 

---

# Notes 

ArgoCD server notes 
argo server => UI is depended on this <br/>
repo server =>  this interacts with version control system <br/>
redis => caching purpose<br/>
notifications => <br/>
dex server => setup for login via google FB <br/>
application sets => <br/>
application controller => state controller 

=============================================================

how to access private repo in argo cd 

