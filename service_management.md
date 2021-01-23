# Gestão de serviços

* Escalar serviços
  * `docker service scale <NAME OF SERVICE>=<NUMBER OF REPLICAS>`
  * `docker service update --replicas=<NUMBER OF REPLICAS> <NAME OF SERVICE>`
  * Escalar múltiplos serviços
    * `docker service scale <NAME OF SERVICE 1>=<NUMBER OF REPLICAS> <NAME OF SERVICE 2>=<NUMBER OF REPLICAS>`
* Modos de serviços:
  * replicated
    * Pode escalar livremente podendo ter de 1 a N instâncias dentro do cluster
  * global
    * Garante que você tera um container do serviço especifica executando em cada nó do cluster
[![asciicast](https://asciinema.org/a/386415.svg)](https://asciinema.org/a/386415)

Comandos usados no gif acima:
```shell
# My cluster nodes
docker node ls

# Creating a service with replicated mode
docker service create --name nginx-replicated nginx
docker service ps nginx-replicated

# Creating a service with global mode
docker service create --mode global --name nginx-global nginx
docker service ps nginx-global
```
