# Node Affinity

Node affinity is conceptually similar to nodeSelector -- it allows you to constrain which nodes your pod is eligible to be scheduled on, based on labels on the node.

2 types

* requiredDuringSchedulingIgnoredDuringExecution : rules that must be met for a pod to be scheduled onto a node
* preferredDuringSchedulingIgnoredDuringExecution : references that the scheduler will try to enforce but will not guarantee.
* requiredDuringSchedulingRequiredDuringExecution : Same as *requiredDuringSchedulingIgnoredDuringExecution*, it evicts pods from nodes which do not satisfy requirements.

* requiredDuringSchedulingIgnoredDuringExecution affinity would be "co-locate the pods of service A and service B in the same zone, since they communicate a lot with each other" and an example preferredDuringSchedulingIgnoredDuringExecution anti-affinity would be "spread the pods from this service across zones" (a hard requirement wouldn't make sense, since you probably have more pods than zones).