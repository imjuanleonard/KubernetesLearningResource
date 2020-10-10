In order to enable access to non-MTLS hosts, we simply have to create
a destination rule that allows traffic to exit the mesh.  This assumes
that we already have a destination rule that is forcing default MTLS
behavior, but that is the standard practice.

We can expose our nonmtls service with:

kubectl apply -f nomtls_destination.yaml
