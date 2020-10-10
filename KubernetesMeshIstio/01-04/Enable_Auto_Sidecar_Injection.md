One of the features we previously disabled was the automatic injection of the Istio proxy.  This is appropriate for an environment where we wish to transition an application to Istio, or one where multiple application environments may exist, all of which may not use a service mesh.  If we want to enable Istio by default for resources deployed into the environment we simply need to "label" the namespace that we want to enable auto-injection into.

First, clean up the hostname environment:

```
kubectl delete -f hostname.yaml
```

Reset the istio relase to include the auto-injection webhook:
```
helm upgrade istio install/kubernetes/helm/istio \
  --namespace istio-system \
  --set gateways.istio-ingressgateway.type=NodePort \
  --set gateways.istio-egressgateway.type=NodePort \
  --set sidecarInjectorWebhook.enabled=true \
  --set global.mtls.enabled=false \
  --set tracing.enabled=true
```

Label the namespace with the "istio-injection" key:
```
kubectl label namespace default istio-injection=enabled
```

Now, re-install the hostname.yaml app and we should see that the sidecar is automatically
injected:

```
kubectl apply -f hostname.yaml
kubectl get pods -l app=hostname
```
