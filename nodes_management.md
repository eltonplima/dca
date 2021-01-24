# Gestão dos nós

## Upgrade dos nós

Por upgrade entenda updates do próprio O.S. ou update/upgrade do docker

Conectar em um dos managers para monitorar os nós do cluster

```bash
watch docker node ls
```

Se tiver algum serviço que possui containers distribuídos por todo cluster podes monitorar este serviço para ver a migração dos containers em real time

```bash
watch docker service ps <SERVICE NAME OR ID>
```

### Cluster com 3 managers e N workers

* Promover o _worker1_
* Fazer drain do _manager1_
* Garantir que não existe mais nenhum container de serviço em execução no _manager1_
* Fazer o demote do _manager1_
* Fazer upgrade e reiniciar(se for necessário) o _manager1_
* Fazer o promote do _manager1_
* Repetir os steps até atualizar todo o cluster
  * Ao finalizar fazer o demote do _worker1_

```shell
docker node promote <WORKER_NODE>
docker node update --availability drain <MANAGER_NODE>
docker container ls
docker node demote <MANAGER_NODE>
# sudo apt update && sudo apt upgrade && sudo reboot
docker node update --availability active <MANAGER_NODE>
docker node promote <MANAGER_NODE>
```
