Mirroring traffic allows us to send traffic to two destinations, with the potential to either deal with faults, or to keep a system in sync.

As with other fault style resources in Istio, we can inject data with a match command to allow us to turn the capability on or off.  In this case, it isn't a "fault" we are injection, but in fact we're defining what looks like an alternate route:

```
   - match:
    - headers:
        cookie:
          exact: user=test
    route:
    - destination:
        host: hostname
        subset: v1
      weight: 100
    mirror:
      host: hostname
      subset: v2
```

We also have two subsets, one for the primary traffic, and one for the mirrored traffic to get to.

In order to see the results of the mirroring cleanly, we've created a script that grabs just the last three lines of the log file from a v1 and a v2 subset pod (the assumption is that you have only one of each running).  If necessary, scale down your deployment if you scaled it up in a previous module.  In addition, we can "clean up" the logs by simply deleting the pods running the v1 and v2 hostname services.  The magic of Kubernetes will restart clean versions for us.

For our mirror test though, we first need to install our updated virtualservice:

```
kubectl apply -f hostname-virtualservice.yaml
```

And then before we try to mirror any data, we can run a check of the current logs so we have something to compare with.  The mirror_logs script grabs the last three lines of the log files from the v1 hostname and v2 hostname pods.

./mirror_logs

We'll run that after each of the following two tests:

First, let's run without the match header to get a non-mirrored output
```
curl -Hhost:hostname.example.com http://$(minikube ip):31380/version/
./mirror_logs
```
Then we can run a test with the mirror output, and we should see a matching log entry in the v2 service log
```
curl -b user=test -Hhost:hostname.example.com http://$(minikube ip):31380/version/
./mirror_logs
```
