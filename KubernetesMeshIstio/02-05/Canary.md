While the deployment of a canary relase (small percentage of traffic scaling to the full system over time) is not fully automated with Istio, it is at least possible to manipulate the system weights to map to the target resources rather than having to manipulate the underlying services.  This can be done irrespective of actual load to the system, or to the number of resoruces providing the system response.

In our case, we'll deploy a 10:90 weighting for our service, and then manually manipulate that to a 90:10 relationship.  In both cases we'll have more than one backend pod to support the load on the system.

We start, as usual with a new virtualservice update:

kubectl apply -f hostname-virtualservice-canary.yaml

And we'll run a curl while loop to see that we're approximately correctly weighted:

while [ 1 ] ; do curl -Hhost:hostname.example.com http://$(minikube ip):31380/version/; done

We will then manually adjust the weights with:

kubectl edit virtualservice hostname
