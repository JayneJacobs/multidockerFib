# Docker Desktop's Kubernetes Dashboard
updated 9-2-2020

This note is for students using Docker Desktop's built-in Kubernetes. If you are using Minikube, the setup here does not apply to you and can be skipped.

If you are using Docker Desktop's built-in Kubernetes, setting up the admin dashboard is going to take a little more work.

1. Grab the kubectl script we need to apply from the GitHub repository: https://github.com/kubernetes/dashboard

2. We will need to download the config file locally so we can edit it (make sure you are copying the most current version from the repo).

If on Mac or using GitBash on Windows enter the following:

curl -O https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.3/aio/deploy/recommended.yaml

If using PowerShell:

Invoke-RestMethod -Uri https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.3/aio/deploy/recommended.yaml -Outfile kubernetes-dashboard.yaml

3. Open up the downloaded file in your code editor and find line 116. Add the following two lines underneath --auto-generate-certificates:

args:
  - --auto-generate-certificates
  - --enable-skip-login
  - --disable-settings-authorizer
4. Run the following command inside the directory where you downloaded the dashboard yaml file a few steps ago:

kubectl apply -f kubernetes-dashboard.yaml

5. Start the server by running the following command:

kubectl proxy

6. You can now access the dashboard by visiting:

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

7. You will be presented with a login screen:


8. Click the "SKIP" link next to the SIGN IN button.

9. You should now be redirected to the Kubernetes Dashboard:


Important! The only reason we are bypassing RBAC Authorization to access the Kubernetes Dashboard is because we are running our cluster locally. You would never do this on a public facing server like Digital Ocean and would need to refer to the official docs to get the dashboard setup:
https://github.com/kubernetes/dashboard/wiki/Access-control

Fullscreen
Expand
257. The Minikube Dashboard
259. The Deployment Process

## Setting up Ingress with Docker Desktop's Kubernetes
This note is only for  Docker Desktop's built-in Kubernetes. If you are using Minikube, this section does not apply to you and can be skipped.

The following instructions apply to both Docker for Mac and Docker for Windows, even though the docs only list Docker for Mac.

1. Execute the provider-specific command noted here:

https://kubernetes.github.io/ingress-nginx/deploy/#docker-for-mac

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.35.0/deploy/static/provider/cloud/deploy.yaml

2. Verify the service was enabled by running the following:

kubectl get pods -n ingress-nginx
POD_NAMESPACE=ingress-nginx
POD_NAME=$(kubectl get pods -n $POD_NAMESPACE -l app.kubernetes.io/name=ingress-nginx --field-selector=status.phase=Running -o jsonpath='{.items[0].metadata.name}')

kubectl exec -it $POD_NAME -n $POD_NAMESPACE -- /nginx-ingress-controller --version


It should show something similar:

ingress-nginx-controller-5cc4589cc8-x7pg2   1/1     Running     0          66s

Fullscreen
Expand
251. Setting up Ingress Locally with Minikube
253. Ingress Update "this.state.seenIndexes.map is…

