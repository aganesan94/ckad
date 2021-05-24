# Commands

The below command just runs and exits. This is because if you take a look at the Dockerfile for this particular use case it does not have any instructions to keep the command running.

```
docker run ubuntu
```

> Note: Containers are meant to run a computation, once its done a container exits.

Running the below command keeps the container running for 5 seconds before it terminates.

```
docker run ubuntu sleep 5
```

To keep this running permanently, create a Dockerfile with the following sequence

```
FROM UBUNTU
CMD sleep 5
```

The CMD command can be specified in the following ways

* CMD ["sleep","5"]
* CMD sleep 5

Build the above docker file using the build command

```
docker build -t <image-name> .
docker run <image-name>
```

# How do we pass an argument? so we can change the 5 to some other value

```
docker run ubuntu-sleeper sleep 10
```

* The 10 overrides 5

In order to make it more legible we replace the *CMD* with *ENTRYPOINT* in the Dockerfile


```
FROM UBUNTU
ENTRYPOINT ["sleep"]
```

This command will have the container sleep for 10 seconds before terminating.

```
docker run ubuntu-sleeper 10
```

If no command is specified with the following command

```
docker run ubuntu-sleeper
```


the error would be
```
sleep: missing operand
```

In order to override the argument there are 2 ways

```
FROM UBUNTU
ENTRYPOINT ["sleep"]
CMD 5
```

Let us create a image from the above called ubuntu-sleeper-2

```
docker build -t . ubuntu-sleeper-2
```

## Setting environment variables using Docker and K8

```
docker run -e APP_COLOR=pink simple-webapp-color
```