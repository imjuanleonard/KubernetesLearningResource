If you decide to use minikube rather than AWS (via Kops) or 
another Cloud drive kubernetes, you will likely need to 
change from LoadBalancer to NodePort configuration in the
service descriptions, and you will need to use a different
URL to communicate with Prometheus.

The following will switch LoadBalancer for NodePort
in the service manifest 'type' field:

    grep Load *yml | cut -d: -f1 | xargs sed -i '' -e  s/LoadBalancer/NodePort/

Note that when port "9090" is referenced, or the discovery 
of the service is defined, that this information will
be different.  In the minikube case, the prometheus UI will
be on the minikube IP, which can be discovered as:

    minikube ip

and on the statically defined (nodePort in the .yml definitions)
as 30990.  The following command should generate an HTTP:// URL 
for use in a browser:

    echo "http://$(minikube ip):30990/"


