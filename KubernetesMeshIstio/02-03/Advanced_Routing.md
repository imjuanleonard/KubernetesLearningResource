In order to route to multiple services and leverage labels for further classification, we need more services to map to. In the kubernetes work, a service maps to an underlying resource based on a label, and in our application, we are using the "app=hostname" label for the service.  But we also have a "version=vX" label (X is the version number), and we can create an additional hostname service backend with that label:

kubectl create -f hostname-v2.yaml

while [ 1 ]; do curl  http://$(minikube ip):31575/version/ ; done

We can then update our virtual service to map to the v2 service only if we have a cookie defined (analogous to a user cookie on logging in):

hostname-virtualservice-v2.yaml

curl -b user=test -Hhost:hostname.example.com http://$(minikube ip):31380/version/

curl -Hhost:hostname.example.com http://$(minikube ip):31380/version/
