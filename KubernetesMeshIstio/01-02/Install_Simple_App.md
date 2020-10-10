# Starting simple

Before we install a complex application, let's deploy a simpler container to get a better understanding of the sidecar injection aspect of Istio/kubernetes by first launching a simple web server (based on the Nginx web server), and looking at the system both without injection and with sidecar injection.  The app is available in the hostname directory as a Dockerfile and a simple script, or can be downloaded from Docker Hub.

Using the hostname.yaml document, we can create an Nginx based instance and by exposing a service via a NodePort (assuming we are using a minikube deployed Kubernetes), we can curl the resource once it is up and running and determine if it is alive:

```
kubectl create -f hostname.yaml
sleep 10
kubectl get pod -l app=hostname
# once the pod is in "Running" state, we can check that we can reach it
NODEPORT=`minikube ip`
curl -so - http://${NODEPORT}:31575
```

*NOTE*: We've pre-defined the nodeport address for the related service (defined
in the service section of the nginx.yaml file) so the above curl command
should work without modification for minikube users.

In order to get istio running with this app though, we need to inject the istio proxy into the configuration.  We can do that manually with istioctl:

```
~/Class/istio-1.0.2/bin/istioctl kube-inject -f hostname.yaml
```
Or inject and launch with Kubectl:

```
~/Class/istio-1.0.2/bin/istioctl kube-inject -f hostname.yaml | kubectl apply -f -
```

