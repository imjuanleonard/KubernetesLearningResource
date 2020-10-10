# Installing Istio

## First make sure you have a Kubernetes enviornment
Get and install kubectl:

https://kubernetes.io/docs/tasks/tools/install-kubectl

If you don't have a Kubernetes environment, the quickest way to get one running is likely via minikube:

https://kubernetes.io/docs/tasks/tools/install-minikube/

## We'll also leverage Helm to install the pieces of our Istio enviornment
Get and install helm for your environment:

https://docs.helm.sh/using_helm/#installing-helm

*Note*: If you are installing helm into a public environment, it is always a good idea to follow the instructions for securing your Helm installation with a client side certificate.  If you are following along and using minikube, you can ignore the warning for now.

##  Then we can get and install the Istio components

https://github.com/istio/istio/releases/

We'll be using the 1.0.2 release available at the time of this recording

To install Istio, we'll leverage the Helm chart, as it's a fairly straightforward
process for installing the pre-requisite elements.

The following steps are also documented on the Istio pages here:

https://istio.io/docs/setup/kubernetes/helm-install/

Firstly, get the istio release appropriate to your OS, as we'll want to get the
_istioctl_ command line tool from the release that matches your computers operating
system

https://github.com/istio/istio/releases/tag/1.0.2

Download the appropriate package, and extract the files.  For 1.0.2, you should have
a directory called ```istio-1.0.2```, we will work from within that directory.

For example, if you are on an OSX machine, you could do:
```
cd ~/Class/
curl -sLO https://github.com/istio/istio/releases/download/1.0.2/istio-1.0.2-osx.tar.gz
tar xfz istio-1.0.2-osx.tar.gz
cd ~/Class/istio-1.0.2
```

Throughout this class, we will use the ~/Class/istio-1.0.2 directory for certain functions. If you extract your istio download elsewhere, just keep this in mind.

We will also need access to the istio command line tool, which is in the ~/Class/istio-1.0.2/bin/ directory, and we can either move the file to be in our path,
such as moving it to /usr/local/bin on a Linux or OSX machine, or perhaps into %system32%\
on a Windows machine.  Alternatively, we could just add the current ~/Class/istio-1.0.2/bin/ directory
to our PATH environment variable.

## Install Istio
Finally we are ready to get started installing. We're going to use helm and we'll assume we're building on a minikube environment, for which we're going to use the NodePort model for communicating with services.  If you are on a cloud based system that supports the LoadBalancer service, you can remove the two '--set gateways*' lines from the following commands.

```
kubectl apply -f install/kubernetes/helm/helm-service-account.yaml
helm init --upgrade --service-account tiller
helm install install/kubernetes/helm/istio --name istio \
  --namespace istio-system \
  --set gateways.istio-ingressgateway.type=NodePort \
  --set gateways.istio-egressgateway.type=NodePort \
  --set sidecarInjectorWebhook.enabled=false \
  --set global.mtls.enabled=false \
  --set tracing.enabled=true
```

This will install not only Istio (really the Pilot component), but also the metrics
and monitoring components and services (Mixer, Prometheus, Jaeger/Zipkin) and the
default Istio ingress gateway.

We can see that all the services started properly with a simple check of the
istio-service namespace:

```
kubectl get pods -n istio-system
```
