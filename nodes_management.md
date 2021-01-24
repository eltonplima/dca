# Gestão dos nós

## Upgrade dos nós

Por upgrade entenda updates do próprio O.S. ou update/upgrade do docker

### Cluster com 3 managers e N workers

* Promover um worker para manager
* Fazer drain de um dos managers
* Fazer upgrade, reiniciar(se for necessário)

```shell
docker node update --availability drain <NODE>
```
