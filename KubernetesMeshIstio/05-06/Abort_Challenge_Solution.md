# Abort injection

The process is as simple as modifying the abort fault in our virutal service:
```
- match:
  - headers:
      cookie:
        exact: user=test
  fault:
    abort:
      percent: 50
      httpStatus: 500
```

And then apply that service:
```
kubectl apply -f hostname-virtualservice.yaml
```

When we include the cookie that matches our header, we should now force an abort in the connection, and if we run this a number of times, we should see some completions, and some aborts, with about a 50/50 probability of an abort.
```
for ((n=1;n<10;n++)); do
curl -b user=test -Hhost:hostname.example.com http://$(minikube ip):31380/version/
done
```
