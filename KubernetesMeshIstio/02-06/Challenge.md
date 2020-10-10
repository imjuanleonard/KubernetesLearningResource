# Challenge - Create a v3 service and migrate load from v2 to v3

At the end of the last module, we have traffic moving to our v2 service, and our development team has just released v3.  Create a v3 deployment and pod (using rstarmer/hostname:v3 as the container image), update the DestinationRule for hostname to include a v3 subset, and update the virtual service to support a 50/50 mix between a v2 service and a v3 service.

You can use the destinationrule from module 02-02, the hostname service and deployment from 02-03, and the canary virtual service from 02-05.

This task should take you approximately 10 minutes to complete.

