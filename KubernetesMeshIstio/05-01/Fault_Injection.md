# Fault injection

For fault injection, we'll inject a simple "Fault", namely a delay in response,
and we can accomlish this by manipulating the virtual service that will define our
route and forwarding response.

In case you've cleaned up your environment, you can get the hostname app back by launching the combined manifest included here:

```
kubectl apply -f route.yaml
kubectl apply -f virtualservice.yaml
kubectl apply -f hostname.yaml
```

The virtualservice manifest included in this module already has a fault injected:
```
- match:
  - headers:
      cookie:
        exact: user=test
  fault:
    delay:
      percent: 100
      fixedDelay: 5s
```

And then apply that change to our service:
kubectl apply -f hostname-virtualservice.yaml

If we curl and include the cookie that matches our header, we should force a 5 second delay in response:
```
time curl -b user=test -Hhost:hostname.example.com http://$(minikube ip):31380/version/
```

If we don't include the user cookie, we bypass the fault.  This version should respond almost instantly:
```
time curl -Hhost:hostname.example.com http://$(minikube ip):31380/version/
```
