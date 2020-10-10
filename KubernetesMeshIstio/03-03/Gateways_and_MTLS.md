Gateways are the mechanism for connecting into an Istio environment, and as such
they support access for non-authenticated services to connet to MTLS authenticated resources. We'll add a gateway, and a virtualservice (which provides the internal forwarding connection) to our environment and validate that we are able to talk to our hostname-v3 resource.

First, deploy the gateway and virtual service:

kubectl apply -f gateway.yaml
kubectl apply -f virtualservice.yaml

We also need to modify the default destinationrule, as we need to include the subset to label mapping as is required for any other virtualservice based rule

kubectl apply -f mtls-rule.yaml

Now we should be able to connect to our hostname-v3 service, via our gatway/virtualservice pair, and the updated subset destination route:

curl -Hhost:hostname.mtls.com http://$(minikube ip):31380/version/

This is an unauthenticated connection traversing our MTLS fabric and talking to an MTLS authenticated service.

Last thing to do is clean up:

kubectl delete ns mtls &
kubectl delete ns nomtls &
