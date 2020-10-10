In addition to header and URI routing, we can leverage weights to distribute
load.

We'll set up an equal distribution forwarding model with weights at 50/50 across
our v1 and v2 services:

kubectl apply -f hostname-virtualservice.yaml

while [ 1 ] ; do curl -Hhost:hostname.example.com http://$(minikube ip):31380/version/; done
