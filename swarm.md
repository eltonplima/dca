# docker swarm

https://docs.docker.com/engine/swarm/swarm_manager_locking/

* Inicializar o cluster:
  * `docker swarm init --autolock` - autolock ativado
  * `docker swarm init --advertise-addr` - permite escolher qual interface o docker ira utilizar
* Gerenciar nós:
  * `docker swarm join-token (manager|worker)` - gera o comando que deverá ser executado no nó que deve se juntar ao cluster.
  * `docker swarm join` - permite adicionar um novo nó
  * `docker node update --availability drain <SWARM NODE>` - informa ao cluster que os container em execução no nó devem ser migrados e novos containers não podem ser criados nele
  * `docker node update --availability active <SWARM NODE>` - informa ao cluster que o nó está disponível para uso
* Ativar o autolock em um cluster ativo:
  * `docker swarm update --autolock=true`
* Desativar o autolock:
  * `docker swarm update --autolock=false`
* Para desbloquear o nó execute:
  * `docker swarm unlock`
* Visualizar os services de um stack
 * `docker stack ps <SERVICE>`
* Limitar quantidade de CPUs para todos os containers de um service
 * `docker service update --limit-cpu <DECIMAL VALUE> <SERVICE NAME>`
* **Gerenciar serviços**
 * `docker service create --replicas <N> <IMAGE>` - cria um serviço com N réplicas
 * `docker service create --network <NETWORK NAME OR ID> <IMAGE>` - cria um serviço conectado a uma rede específica
