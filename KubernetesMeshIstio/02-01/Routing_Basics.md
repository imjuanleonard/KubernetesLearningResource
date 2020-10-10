Add a gateway:

```
kubectl create -f hostname-gateway.yaml
```

And then associate a virtual service and basic route to the gateway:

```
kubectl create -f hostname-virtualservice.yaml
```

Get "service" NodePort access:

```
curl -I http://$(minikube ip):31575
```

Get "gateway" NodePort access:
```
kubectl get svc -n istio-system
```

Talk to the port 80 nodeport mapping
```
curl -I -Hhost:hostname.example.com http://$(minikube ip):31380
```
