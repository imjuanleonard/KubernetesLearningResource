# Working with many applications, and namespacing

## Chapter Goals
1. Better real world example using namespaces

### Working with many applications
Deploy sample infrastructure: `kubectl apply -f sample-infrastructure.yaml`

#### Namespaces:
`kubectl get pods` returns no results.
`kubectl get pods --all-namespaces` returns all our results.
`kubectl get namespaces` Returns just the namespaces

