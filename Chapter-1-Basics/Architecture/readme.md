# Architecture

Pod - Smallest Unit where containers are run.

Node - Worker machine where containers are launched.
  - Master Node : Node with Kubernetes installed in it and responsible for managing the cluster
  - Worker Nodes : Nodes where pods are scheduled

Cluster - Set of nodes grouped together which is fault tolerant

## Components

(Kevin Ate Eggless Cakes Called Scoops )

- API Server - Front end for Kubernetes, User mgmt, CLI for K8 cluster.
- etcd - Key store, key/value store which is distributed to manage the cluster.
- Kubelet - Runs on each node on the cluster, ensures containers are running.
- Container runtime - (Docker) - Runtime used to run containers.
- Controller - Orchestration of nodes. Make decisions on nodes.
- Scheduler - Assigns containers/pods to nodes.