# Environment Variables

## Setting via Docker
```shell
# Set environment variables via docker
docker run -e key=val <image-name>
```

### Sample 1:  Basics

```shell
k create -f samples/env/samples-1/env.yml
k get po sample-1-env-pod
k exec -it sample-1-env-pod /bin/ss
k describe po sample-1-env-pod
```

![Alt Basics](docs/images/env/sample-1/env.png)
---
