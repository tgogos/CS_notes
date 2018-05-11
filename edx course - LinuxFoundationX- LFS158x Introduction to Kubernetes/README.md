
## Worker Node Components: Container Runtime

To run and manage a container's lifecycle, we need a container runtime on the worker node. Some examples of container runtimes are: 

 - containerd
 - rkt
 - lxd

Sometimes, Docker is also referred to as a container runtime, but to be precise, **Docker is a platform which uses *containerd*** as a container runtime. 

## Worker Node Components: kubelet

The kubelet is an agent which runs on each worker node and communicates with the master node. It receives the Pod definition via various means (primarily, through the API server), and runs the containers associated with the Pod. It also makes sure that the containers which are part of the Pods are healthy at all times.

The kubelet connects to the container runtime using **Container Runtime Interface (CRI)**. The Container Runtime Interface consists of protocol buffers, gRPC API, and libraries. 
