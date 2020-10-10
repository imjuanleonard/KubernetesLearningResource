# Abort injection

and we can accomplish this by manipulating the virtual service that will define our
route and forwarding response.

If we update our virtual service with a match statement similar to the following:
```
- match:
  - headers:
      cookie:
        exact: user=test
  fault:
    abort:
      percent: 100
      httpStatus: 500
```
And then apply that service:
```
kubectl apply -f hostname-virtualservice.yaml
```

When we include the cookie that matches our header, we should now force an abort in the connection:
```
curl -b user=test -Hhost:hostname.example.com http://$(minikube ip):31380/version/
```

If we don't include the user cookie, we bypass the fault.  This version should respond almost instantly:
```
curl -Hhost:hostname.example.com http://$(minikube ip):31380/version/
```
