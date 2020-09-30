# Searching, sorting and filtering in Kubernetes

## Chapter Goals
Understand how to search, sort and filter applications

#### More details
`kubectl get pods --sort-by=.metadata.name` sorts pods by name
`kubectl get pods -o wide --all-namespaces` returns more details
`kubectl get pods/cart-dev -n cart -o json` returns the pod json
`kubectl get pods  -n cart -o=jsonpath="{..image}" -l app=cart-dev` searches cart-dev, and returns the image based on the jsonpath
`kubectl get pods --all-namespaces -o jsonpath="{.items[*].spec.containers[*].image}"` all container images running
