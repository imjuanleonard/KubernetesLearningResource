To highlight access via Mutual TLS, we need to extend our micro-microservice with
a client _in_ the mesh rather than reaching in via the Ingress Gateway as we've
done previously.

But we'll keep things simple and just use a Curl capable container (tutum/curl is
the one the Istio folks use, so we'll follow their lead).

Launch a curl capable container in the default namespace, and verify that we can
still communicate with our service:

```
for n in mtls nomtls; do kubectl create namespace $n; done
kubectl label namespace mtls istio-injection=enabled
for n in mtls nomtls; do kubectl create -f curl.yaml -f hostname.yaml -n $n; done
```

We can run a simple script that will loop through all the connections:
nomtls->nomtls
nomtls->mtls
mtls->nomtls
mtls->mtls

```
./test
```

Now we can start by adding a policy that allows MTLS in "permissive mode" so that all services can still talk. *NOTE*: we will run the test script after each set to see what is possible.

kubectl apply -f permissive_policy.yaml

Next we can create a destination rule defining access only via MTLS to the mtls hostname app:

kubectl apply -f default_destination_rule.yaml

Then we can make communications strict:

kubectl apply -f strict_policy.yaml



