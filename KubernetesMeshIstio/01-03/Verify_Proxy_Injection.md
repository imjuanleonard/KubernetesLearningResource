# Verify that the Istio Proxy is injected and capturing traffic

In order to ensure that we are in fact capturing traffic in the pod, we can simply have a look at the logs from the now injected proxy.

```
POD=`kubectl get pods -l app=hostname | awk '/hostname/ {print $1}'`
kubectl logs $POD -c istio-proxy
```

We should see information indicating that a number of ports have been redirected via ipTables rules.

