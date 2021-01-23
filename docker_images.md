# Imagens docker

* [best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

O comando **RUN** só vai criar uma nova layer se executar alguma instrução que exija alterar o filesystem

[![asciicast](https://asciinema.org/a/F3OPtIj4YltuyiXofxEWjEP3W.svg)](https://asciinema.org/a/F3OPtIj4YltuyiXofxEWjEP3W)

```shell
# Check the base image layers
docker image inspect ubuntu | jq ".[0].RootFS.Layers"


# Using RUN with a command that do not change the filesystem will not create a new layer
docker build -t eltonplima/ubuntu -<<EOF
FROM ubuntu
RUN echo -e "\033[33;1mHello\033[0m"
EOF
docker image inspect eltonplima/ubuntu | jq ".[0].RootFS.Layers"


# Each RUN with a command that change the filesystem will create a new layer
docker build -t eltonplima/ubuntu -<<EOF
FROM ubuntu
RUN apt update
RUN apt upgrade -y
EOF
docker image inspect eltonplima/ubuntu | jq ".[0].RootFS.Layers"


# We can optimize the RUN commands to create a single extra layer
docker build -t eltonplima/ubuntu -<<EOF
FROM ubuntu
RUN apt update && apt upgrade -y
EOF
docker image inspect eltonplima/ubuntu | jq ".[0].RootFS.Layers"
```
