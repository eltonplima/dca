# Conceitos gerais

## Arquivos e diretórios importantes

* /etc/docker/daemon.json - Arquivos de configuração
* <pre>/var/lib/docker/
  ├── builder
  ├── buildkit
  ├── containers
  ├── image
  ├── network
  ├── overlay2
  ├── plugins
  ├── runtimes
  ├── swarm
  ├── tmp
  ├── trust
  └── volumes
</pre>

## Logging

* O formato padrão dos logs é `json-file`
* A opção que permite customizar o logging driver use: `docker container run -d --log-driver <DRIVER> <IMAGE>`

## Experimental features

Configure a seguinte chave no /etc/docker/daemon.json
[referencia](https://docs.docker.com/engine/reference/commandline/checkpoint_create/)
```json
{"experimental": true}
```
