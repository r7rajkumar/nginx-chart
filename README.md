#Helm chart enables the deployment of an NGINX server on Kubernetes using a self-signed certificate

Prerequisites: Kubernetes cluster Helm Installation

Clone the repository:

git clone https://github.com/r7rajkumar/nginx-chart.git

Install the Helm chart:

helm install my-nginx nginx-chart

Create the "dev" namespace: kubectl create namespace dev

Generate private key: openssl genrsa -out server.key 2048

Generate a self-signed SSL certificate and private key using OpenSSL: openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt

Apply the YAML files to deploy the resources:

kubectl apply -f nginx-chart/nginx/templates/hello-app.yaml --namespace dev kubectl apply -f nginx-chart/nginx/templates/hello-service.yaml --namespace dev kubectl apply -f nginx-chart/nginx/templates/ingress.yaml --namespace dev

Create a Kubernetes secret to store the SSL certificate and private key:

kubectl create secret tls hello-app-tls --cert=tls.crt --key=tls.key --namespace dev

Note: Alternatively, you can also create the TLS secret using a (hello-app-tls) YAML file. update your cert (tls.crt, tls.key) content inside this file

Verify the deployment:

kubectl get deployment hello-service -n dev kubectl get pods -n dev kubectl get service hello-service -n dev kubectl get ingress -n dev

Access the deployed application over HTTPS:

Update your local DNS or hosts file to map demo.rajkumar.home to the IP address of your Kubernetes cluster.

Open a web browser and navigate to https://demo.rajkumar.home You can replace with your hostname to verify the page.

Cleaning Up:

To delete the Helm release and associated resources, run the following command

helm uninstall my-nginx

This will remove the Nginx deployment, service, and associated resources from your Kubernetes cluster.
