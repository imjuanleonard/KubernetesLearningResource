# Deleting resources in Kubernetes

## Chapter Goals
Understand how to delete pods, and resources in k8s.

#### More details
`kubectl delete pods --all` deletes all pods in the default namespace
`kubectl delete pods -n cart --all` deletes all pods in the cart namespace
`kubectl delete pods -l env=staging -n social` Deletes the pods in the social namespace that match the staging environment