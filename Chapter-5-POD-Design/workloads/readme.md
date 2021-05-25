# Workloads

* A series of tasks which start and finish 

```
docker run ubuntu expr 3+2
```

On running the below command, it shows that the container has already exited

```
docker ps -a
```

When you run an pod from kubernetes as described in **workload-1.yaml**,
the pod exits and continues to restart. This is because the default
behavior of a pod is to continue restarting until it exits.

To stop this we add a property

> restartPolicy 

to the template 

# Jobs


A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. 
As pods successfully complete, the Job tracks the successful completions. When a specified number of successful completions is reached, the task (ie, Job) is complete. Deleting a Job will clean up the Pods it created. Suspending a Job will delete its active Pods until the Job is resumed again.

Refer to **job.yaml** file.
- Followings the same structure as deployment
- There are 3 kinds of jobs:
  
    - No Parallels (Only one pod is started unless the pod fails, once job completes the job is terminated successfully).
  
    - Parallel Jobs w/ fixed completion counts : Runs until the completion counts are met. By default the value of .spec.

    - Parallel Jobs w/ work queue : Runs until the completion counts are met. By default the value of .spec.

- For a non-parallel Job, you can leave both .spec.completions and .spec.parallelism unset. When both are unset, both are defaulted to 1.

- For a fixed completion count Job, you should set .spec.completions to the number of completions needed. You can set .spec.parallelism, or leave it unset and it will default to 1.


```
kubect get jobs
kubectl get pods
kubectl logs -f job my-job
kubectl delete job my-job
```

To increase the number of pods use the following parameter in the definition file.

> completions

In order to run jobs in parallel

> parallelism

## Cron jobs

