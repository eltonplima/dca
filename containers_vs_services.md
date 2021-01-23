## Diferenças entre executar containers e serviços

* Containers
  * São executados na máquina onde o docker está executando
* Services
  * São executados dentro de algum nó do cluster
  * Podem ser escalados para cima ou para baixo
  * Podem migrar entre os nós dos cluster toda vez que é recriado

### Importante

Encontrei alguns links no stack overflow onde colocam entre as diferença, que ao usar o `docker run` não é possível reinicar o container em caso de falha e isso não é verdade conforme pode ser visto na [documentação oficial](https://docs.docker.com/engine/reference/run/#restart-policies---restart)
