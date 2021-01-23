# Imagens docker

* [best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

## Build via stdin

Toda vez que fazemos o build de uma imagem precisamos fornecer um contexto, que geralmente é o diretório corrente, mas quando fazemos o build via stdin a única coisa que existe no contexto é o Dockerfile criado via heredoc.

No exemplo a seguir podemos ver que o build irá falhar por não conseguir encontrar o arquivo **somefile.txt**

[![asciicast](https://asciinema.org/a/Mz7qqKoFiq6sARziW8bcyRaDM.svg)](https://asciinema.org/a/Mz7qqKoFiq6sARziW8bcyRaDM)

```
# create a directory to work in
mkdir example
cd example

# create an example file
touch somefile.txt

docker build -t myimage:latest -<<EOF
FROM busybox
COPY somefile.txt .
RUN cat /somefile.txt
EOF
```

## Otimização de layers

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
