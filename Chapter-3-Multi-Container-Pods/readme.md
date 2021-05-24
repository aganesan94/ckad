# Multi Container Pods

* Microservices when deployed need to have a log agent. Each service will need to have a log agent.
* Multi container pods share the same life cycle, network, storage

- Side Car - Ex Logging agent along with a server
- Adapter - Ex Convert logs from different servers using an adapter and then forward to a logging server
- Ambassador - Ex: Different environments will have different databases, apps can refer to the respective databases based on the environment.