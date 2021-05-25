# Lifecyle of a POD

---
## POD status

### Pending
- Pod is not scheduled by the scheduler
- Waiting on downloading the container images over the network
- Containers have not been set up and in running state.

### Running
- Pod has been scheduled and bound to a node
- All containers are created
- One container is running

### Succeeded

- All containers have been terminated
- None of the containers will be restarted


### Failed

- One or more containers of the pod terminated
- Termination caused because the container exited with a non-zero status or was terminated by the system

### Unknown

- Unable to fetch the status of the phase
- Likely a communication failure between the node and pod.

### Terminating (Note this is not a pod Phase)

- Default 30 seconds to terminate a pod else terminate by force.

---

## Container status

### Waiting

- Container is still running to complete start up

### Running

- Container executing without issues.

### Terminated

- Ran to completion or failed for some reason.


## Condition Status

- Pod Scheduled
- Initialized
- Container Ready
- Ready
