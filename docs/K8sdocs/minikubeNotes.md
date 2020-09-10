 

Using the  docker driver when using Minikube instead of Docker Desktop.

The docker driver is not supported for use in   currently does not work with any type of ingress:

https://minikube.sigs.k8s.io/docs/drivers/docker/#known-issues

If you have started the course with the docker driver, you will need to switch to a different driver in order to continue.

Delete your cluster:

minikube delete

Restart with a different driver:

macOS:

minikube start --driver=hyperkit

or

minikube start --driver=virtualbox

Windows:

minikube start --driver=hyperv

or

minikube start --driver=virtualbox
 
Ingress NGINX 🔗︎
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/kind/deploy.yaml
 
The manifests contains kind specific patches to forward the hostPorts to the ingress controller, set taint tolerations and schedule it to the custom labelled node.

Now the Ingress is all setup. Wait until is ready to process requests running:

kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
 
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=90s
Refer Using Ingress for a basic example usage.

Ingress on Macbook

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml

Ran this command to confirm ingress service was running:

kubectl get svc -n ingress-nginx

Created the PG secret:

kubectl create secret generic pgpassword --from-literal PGPASSWORD= 

Then finally:

kubectl apply -f k8s/

After all of this, going to https://localhost the application works as expected.

Something definitely went wrong with the initial setup of ingress I think. I would try running thru all of the above commands again to see if you can get a different result.

### 3 Bare-metal
Using NodePort:


kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.35.0/deploy/static/provider/baremetal/deploy.yaml
Tip

For extended notes regarding deployments on bare-metal, see Bare-metal considerations.

