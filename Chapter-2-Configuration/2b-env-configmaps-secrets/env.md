# Environment Variables

## Setting via Docker
```shell
# Set environment variables via docker
docker run -e key=val <image-name>
```

### Sample 1:  Basics

```shell
k create -f samples/environment/samples-1/env.yml
k get po sample-1-env-pod

# Shell in to check out environment variables
k exec -it sample-1-env-pod /bin/ss
# env | grep DEMO_GREETING
DEMO_GREETING=Hello from the environment
# env | grep DEMO_FAREWELL
DEMO_FAREWELL=Such a sweet sorrow

k describe po sample-1-env-pod
```

![Alt Basics](docs/images/env/sample-1/env.png)

### Sample 2: Replacement of environment variables in the definition
```shell
k delete pods --all
k create -f samples/environment/samples-2/env.yml
k logs -f sample-2-env-pod
```

