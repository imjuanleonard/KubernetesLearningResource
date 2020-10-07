#Readme

Required installations:
Docker (Community Edition, Stable build): https://www.docker.com/community-edition#/download
kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/
Virtualbox: https://www.virtualbox.org/wiki/Downloads
minikube: https://github.com/kubernetes/minikube/releases/tag/v0.25.2

For instance, my versions are as follows:
Docker Version:
```
: docker version
Client:
 Version:	18.03.0-ce
 API version:	1.37
 Go version:	go1.9.4
 Git commit:	0520e24
 Built:	Wed Mar 21 23:06:22 2018
 OS/Arch:	darwin/amd64
 Experimental:	false
 Orchestrator:	swarm

Server:
 Engine:
  Version:	18.03.0-ce
  API version:	1.37 (minimum version 1.12)
  Go version:	go1.9.4
  Git commit:	0520e24
  Built:	Wed Mar 21 23:14:32 2018
  OS/Arch:	linux/amd64
  Experimental:	true
: 
```

Kubectl version:
```
: kubectl version
Client Version: version.Info{Major:"1", Minor:"9", GitVersion:"v1.9.6", GitCommit:"9f8ebd171479bec0ada837d7ee641dec2f8c6dd1", GitTreeState:"clean", BuildDate:"2018-03-21T15:21:50Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"", Minor:"", GitVersion:"v1.9.4", GitCommit:"bee2d1505c4fe820744d26d41ecd3fdd4a3d6546", GitTreeState:"clean", BuildDate:"2018-03-21T21:48:36Z", GoVersion:"go1.9.1", Compiler:"gc", Platform:"linux/amd64"}
```

Virtualbox version: 
```
Version 5.2.8 r121009 (Qt5.6.3)
```

Minikube:
```
: minikube version
minikube version: v0.25.2
```