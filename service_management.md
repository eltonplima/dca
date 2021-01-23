# Gestão de serviços

* Escalar serviços
  * `docker service scale <NAME OF SERVICE>=<NUMBER OF REPLICAS>`
  * `docker service update --replicas=<NUMBER OF REPLICAS> <NAME OF SERVICE>`
* Modos de serviços:
  * replicated
    * Pode escalar livremente podendo ter de 1 a N instâncias dentro do cluster
  * global
    * Garante que você tera um container do serviço especifica executando em cada nó do cluster
