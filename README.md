# nginx-chart
nginx-chart demo 
Nginx Helm Chart
This Helm chart deploys an Nginx server on Kubernetes. It supports enabling HTTPS protocol through values.yaml and exposes the Nginx landing page on a NodePort. It utilizes a self-signed certificate for testing purposes.

Prerequisites
Kubernetes cluster
Helm
Installation
Clone the repository:


git clone <repository-url>
Customize the values in nginx-chart/values.yaml according to your requirements. Pay attention to the https.enabled flag, which enables or disables HTTPS support.

Install the Helm chart:


helm install my-nginx nginx-chart
Accessing the Nginx Server
Get the NodePort assigned to the Nginx service:


kubectl get services my-nginx
Note the value under the PORT(S) column. It corresponds to the NodePort assigned to the Nginx service.

Update your /etc/hosts file to map the hostname to the IP address of your Kubernetes cluster. Add the following entry:


<cluster-ip> mynginx
Replace <cluster-ip> with the actual IP address of your cluster.

Access the Nginx landing page through your web browser:


https://mynginx:<node-port>
Replace <node-port> with the NodePort value obtained in step 1.

Cleaning Up
To delete the Helm release and associated resources, run the following command:

helm uninstall my-nginx
This will remove the Nginx deployment, service, and associated resources from your Kubernetes cluster.