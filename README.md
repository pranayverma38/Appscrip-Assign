NOTE : I have followed all the steps as required in the assignment, you can refer to yaml files and tf files above for the same 
I made this readme file by myself and havent put long explanation of each step as this is not for public visibility.

# 1) Provision eks cluster with terraform, with public subnet + iam
to proceed, we need terraform and aws cli installed also terraform should be configured with AWS Account or role
# Terraform

Refer to Main.tf file in terraform folder

1) Use AWS Provider
2) Create Vpc + cidr 
3) put public subnet into vpc,
4) Create EKS module
5) configure node group + instance type

Run commands : 

<pre>terraform init</pre>
<pre>terraform validate</pre>
<pre>terraform apply</pre>

# 2) ArgoCD Login + Installation
install argo cd using 
<pre>kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml</pre>

expose ArgoCD using LoadBalancer type
<pre>kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'</pre>

Get initial Password 
<pre>kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d</pre>

Now login to argocd using the exposed public local Ip and using credentials from above secert.

# 3) public access URL for Nginx
No public URL from ingress because <pre>i run terraform destroy in order to save cost overnight</pre>

