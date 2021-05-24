# Probes

  There are 3 types of probes

  - readiness
  - liveness
  - startup

## Readiness Probe

- Kubelet uses this probe to find outout when the container is ready to start acepting traffic.
- All of its containers need to be ready for the probe to succeed.
- The pods which are not ready are removed from the load balancers
  
## Liveness Probe

- Useed to restart a container to make sure it is back online in case of deadlocks or bugs

## Startup Probes

- Used to determine when an application has started.
- This probe when configured disables the readiness and liveness probes until the probe succeeds. This is to ensure no other probe intereferes during the start up.
- This is primarily used to check on slow starting containers and avoiding them from getting killed before they are up and running.