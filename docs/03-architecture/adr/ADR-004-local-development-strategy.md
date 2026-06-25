# ADR-004 - Estratégia de Desenvolvimento Local

## Status

Accepted

## Contexto

O projeto utiliza diversos serviços AWS.

Executar recursos reais durante o desenvolvimento geraria custos recorrentes.

## Alternativas Consideradas

### Opção 1

Utilizar AWS real desde o início.

### Opção 2

Utilizar LocalStack.

## Decisão

Utilizar LocalStack para desenvolvimento local.

## Consequências

### Positivas

- Custo zero
- Ambiente reproduzível
- Desenvolvimento offline

### Negativas

- Algumas diferenças em relação à AWS real