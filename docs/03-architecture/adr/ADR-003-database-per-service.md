# ADR-003 - Database per Service

## Status

Accepted

## Contexto

Cada microsserviço precisa manter autonomia sobre seus dados.

## Alternativas Consideradas

### Opção 1

Banco compartilhado.

### Opção 2

Database per Service.

## Decisão

Cada microsserviço possuirá seu próprio banco de dados.

## Consequências

### Positivas

- Baixo acoplamento
- Independência
- Escalabilidade

### Negativas

- Maior complexidade
- Necessidade de consistência eventual