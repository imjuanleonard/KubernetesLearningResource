# Install Bookinfo

In order to work with the tracing capabilites, we need a more functional
application, and we will leverage the bookinfo example from the Istio
community.

Installation is simple, as we can leverage the kubernetes manifest
in the samples directory of our istio download.  Change to the istio-1.0.2
directory, and launch the sample application:

```
pushd ~/Class/istio-1.0.2
kubectl create namespace bookinfo
kubectl label namespace bookinfo istio-injection=enabled
kubectl apply -n bookinfo -f samples/bookinfo/platform/kube/bookinfo.yaml
kubectl apply -n bookinfo -f samples/bookinfo/networking/bookinfo-gateway.yaml
kubectl apply -n bookinfo -f samples/bookinfo/networking/destination-rule-all.yaml
kubectl apply -n bookinfo -f samples/bookinfo/networking/virtual-service-all-v1.yaml
popd
```

Connect to the bookinfo app by first determining your minikube IP:
```
minikube ip
```
And with that address, navigate to the productpage service in the bookinfo app:
```
http://{minikube ip}:31380/productpage
```
#Note: replace $(minikube ip) with the ip address of your minikube instance

For tracing to work, we need to tell Istio to capture and forward messages.
Our helm based deployment already includes the key services needed with
Jaeger capturing the key data for traces.  We need to expose the Jaeger
dashboard, and we'll do that with a simple port-forward:

```
kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=jaeger -o jsonpath='{.items[0].metadata.name}') 16686:16686 &
```
