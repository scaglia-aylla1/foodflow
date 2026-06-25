# ADR-002 - Estratégia de Tópicos Kafka

## Status

Accepted

## Contexto

A arquitetura necessita de eventos assíncronos para comunicação entre microsserviços.

## Alternativas Consideradas

### Opção 1

Um tópico por evento.

Exemplos:

- payment-approved
- order-created
- delivery-completed

### Opção 2

Um tópico por domínio.

Exemplos:

- orders
- payments
- deliveries
- reviews

## Decisão

Utilizar tópicos organizados por domínio.

## Consequências

### Positivas

- Melhor organização
- Menor quantidade de tópicos
- Escalabilidade
- Evolução simplificada

### Negativas

- Consumidores precisam filtrar eventType