In order to build more advanced rules, the first step is to ensure that there is a way to define different backends.  This is done by mapping Kubernetes Labels to "subsets" in Istio with a DestinationRule.

We'll create a destination rule for two labels:  v1 and v2:

```
kubectl apply -f hostname-destination-rule.yaml
```

And then we'll create a subest based rule for our default route:

```
kubectl apply -f hostname-virtualservice-subset.yaml
```

And we can verify that we're still communicating with the service with curl:

```
curl -Hhost:hostname.example.com http://$(minikube ip):31380/version/
```
