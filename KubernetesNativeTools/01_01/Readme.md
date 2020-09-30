# Working with kubectl

## Chapter Goals
This chapter will cover the different ways to create objects in Kuberentes- the variations of the create command, and the apply command.

### Different ways to create objects
Simplest way: `kubectl run helloworld --image karthequian/helloworld:latest`
Common way (from file): `kubectl create -f red.yaml`
Multiple files: `kubectl create -f blue.yaml -f green.yaml`
Whole directory: `kubectl create ./colors`
URL: `kubectl apply -f https://raw.githubusercontent.com/karthequian/kubernetesHelloworld/master/hello.yaml`