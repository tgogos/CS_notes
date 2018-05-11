
## Worker Node Components: Container Runtime

To run and manage a container's lifecycle, we need a container runtime on the worker node. Some examples of container runtimes are: 

 - containerd
 - rkt
 - lxd

Sometimes, Docker is also referred to as a container runtime, but to be precise, **Docker is a platform which uses *containerd*** as a container runtime. 

## Worker Node Components: kubelet

The kubelet is an agent which runs on each worker node and communicates with the master node. It receives the Pod definition via various means (primarily, through the API server), and runs the containers associated with the Pod. It also makes sure that the containers which are part of the Pods are healthy at all times.

The kubelet connects to the container runtime using **Container Runtime Interface (CRI)**. The Container Runtime Interface consists of protocol buffers, gRPC API, and libraries. 

![](CRI.png)

As shown above, the kubelet (grpc client) connects to the CRI shim (grpc server) to perform container and image operations. CRI implements two services: `ImageService` and `RuntimeService`.

 - The `ImageService` is responsible for all the *image-related* operations, while
 - the `RuntimeService` is responsible for all the *Pod and container-related* operations.

> Container runtimes used to be hard-coded in Kubernetes, but with the development of CRI, Kubernetes can now use different container runtimes without the need to recompile. **Any container runtime that implements CRI can be used by Kubernetes to manage Pods, containers, and container images**.
