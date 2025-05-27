# 🧭 Kubernetes Architecture Overview

Kubernetes operates on a **master-worker** architecture, comprising a **Control Plane** (Master Node) and multiple **Worker Nodes**.


## 🧠 Control Plane (Master Node)

The Control Plane manages the Kubernetes cluster and consists of the following components:

- **API Server**: Serves as the front-end of the Kubernetes control plane, handling RESTful requests from users and other components.
- **etcd**: A consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data.
- **Scheduler**: Assigns newly created pods to nodes based on resource availability and other constraints.
- **Controller Manager**: Runs controller processes that regulate the state of the system, ensuring the desired state matches the current state.
- **Cloud Controller Manager**: Manages cloud-specific control logic, allowing the Kubernetes cluster to interact with the cloud provider's API.

## 🛠️ Worker Nodes

Worker Nodes run the applications and are managed by the Control Plane. Each node contains the following components:

- **kubelet**: An agent that ensures containers are running in a pod. It communicates with the Control Plane to receive instructions and report back the status of the node.
- **kube-proxy**: Maintains network rules on nodes, enabling network communication to your Pods from network sessions inside or outside of your cluster.
- **Container Runtime**: The software responsible for running containers. Kubernetes supports several runtimes, including Docker, containerd, and CRI-O.

## 📦 Pods and Services

- **Pods**: The smallest and simplest Kubernetes object. A Pod represents a set of running containers on your cluster.
- **Services**: An abstraction that defines a logical set of Pods and a policy by which to access them, often used to expose applications running on a set of Pods.

---

For a visual representation of this architecture, you can refer to the following diagram:

![Kubernetes Architecture Diagram](https://www.opsramp.com/wp-content/uploads/2022/07/Kubernetes-Architecture-1536x972.png)

*Source: [OpsRamp - An Overview of Kubernetes Architecture](https://www.opsramp.com/guides/why-kubernetes/kubernetes-architecture/)*

---

This overview should provide a clear understanding of the fundamental components and their roles within the Kubernetes architecture.
"""
