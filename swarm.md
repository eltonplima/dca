# docker swarm

https://docs.docker.com/engine/swarm/swarm_manager_locking/

* Inicializar o cluster com autolock ativado:
  * docker swarm init --autolock
* Ativar o autolock em um cluster ativo:
  * docker swarm update --autolock=true
* Desativar o autolock:
  * docker swarm update --autolock=false
