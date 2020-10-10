In order to break the circuit, we need a few pieces of the deck to stack in our favor:
1) We need to be able to generate load in a way that would force a "break" in the connection between pieces of our environment.
2) We need to define what would be cause for the circuit to break
and
3) We need an app to break.

We'll reuse our venerable little hostname app as our target, but we'll need to make sure it's slow (because right now it's so fast that we'd have a hard time creating enough load).  Luckily, we can just inject some delay via Istio!
And for load generation, we'll again rely on the value of the Istio community, and leverage the fortio load generator, which is used to run some of the integration tests for the Istio fabric. It'll be used to generate more concurrent requests than what our system should allow, which will trigger the breaking of our circuit.

Firstly, let's load the destination rule that defines our desire to only allow one connection at a time.

kubectl apply -f hostname-cb.yaml

And we need to add our update to the virtualservice so that we have a small delay added to the requests:

kubectl apply -f hostname-virtualservice.yaml

Then, we can launch fortio in a pod so that we can generate load (and so that we can talk more directly to our service via the Istio mesh.

kubectl apply -f fortio-deploy.yaml

And lastly, we'll use a little helper script to exec into the fortio container and launch requests against the hostname service:

./fortio load -c 3 -n 20 -qps 0 http://hostname/version/

We can also check to make sure istio-proxy is seeing faults:
./fortio-faults
