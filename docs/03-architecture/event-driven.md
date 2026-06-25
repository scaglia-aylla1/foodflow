# FoodFlow - Event Driven Architecture

## Objetivo

Este documento descreve a arquitetura orientada a eventos do FoodFlow, incluindo eventos de domínio, publishers, consumers e integrações utilizando Kafka, SNS, SQS e AWS Lambda.

---

# Visão Geral

O FoodFlow utiliza uma arquitetura Event-Driven para reduzir acoplamento entre microsserviços e permitir escalabilidade horizontal.

A comunicação assíncrona será realizada principalmente através do Apache Kafka.

SNS, SQS e AWS Lambda serão utilizados para processamento assíncrono complementar e futuras integrações externas.

---

# Estratégia de Tópicos Kafka

Os tópicos foram organizados por domínio de negócio.

## Tópicos

- orders
- payments
- deliveries
- reviews
- notifications

---

# Estrutura Padrão dos Eventos

Todos os eventos devem seguir o mesmo contrato.

```json
{
  "eventId": "uuid",
  "eventType": "PAYMENT_APPROVED",
  "aggregateId": "order-id",
  "occurredAt": "2026-01-01T10:00:00Z",
  "payload": {}
}
```

## Campos

### eventId

Identificador único do evento.

### eventType

Tipo do evento.

### aggregateId

Identificador da entidade principal relacionada ao evento.

### occurredAt

Data e hora da ocorrência.

### payload

Dados específicos do evento.

---

# Topic: orders

## ORDER_CREATED

### Publisher

- order-service

### Consumers

- notification-service

### Objetivo

Informar a criação de um novo pedido.

---

## ORDER_ACCEPTED

### Publisher

- restaurant-service

### Consumers

- order-service
- delivery-service
- notification-service

### Objetivo

Informar que o restaurante aceitou o pedido.

---

## ORDER_PREPARING

### Publisher

- restaurant-service

### Consumers

- order-service
- notification-service

### Objetivo

Atualizar status do pedido.

---

## ORDER_READY_FOR_PICKUP

### Publisher

- restaurant-service

### Consumers

- delivery-service
- order-service
- notification-service

### Objetivo

Informar que o pedido está pronto para retirada.

---

## ORDER_CANCELLED

### Publisher

- order-service

### Consumers

- payment-service
- delivery-service
- notification-service

### Objetivo

Informar cancelamento do pedido.

---

# Topic: payments

## PAYMENT_APPROVED

### Publisher

- payment-service

### Consumers

- order-service
- restaurant-service
- notification-service

### Objetivo

Liberar o processamento do pedido.

---

## PAYMENT_REJECTED

### Publisher

- payment-service

### Consumers

- order-service
- notification-service

### Objetivo

Informar falha no pagamento.

---

## PAYMENT_REFUNDED

### Publisher

- payment-service

### Consumers

- order-service
- notification-service

### Objetivo

Informar reembolso.

---

# Topic: deliveries

## DELIVERY_AVAILABLE

### Publisher

- delivery-service

### Consumers

- notification-service

### Objetivo

Informar disponibilidade de entrega.

---

## DELIVERY_ASSIGNED

### Publisher

- delivery-service

### Consumers

- order-service
- notification-service

### Objetivo

Informar que um entregador aceitou a entrega.

---

## DELIVERY_PICKED_UP

### Publisher

- delivery-service

### Consumers

- order-service
- notification-service

### Objetivo

Informar retirada do pedido.

---

## OUT_FOR_DELIVERY

### Publisher

- delivery-service

### Consumers

- order-service
- notification-service

### Objetivo

Informar saída para entrega.

---

## DELIVERY_COMPLETED

### Publisher

- delivery-service

### Consumers

- order-service
- notification-service
- AWS Lambda

### Objetivo

Finalizar pedido e liberar avaliações.

---

# Topic: reviews

## RESTAURANT_REVIEW_CREATED

### Publisher

- order-service

### Consumers

- restaurant-service
- AWS Lambda

### Objetivo

Atualizar reputação do restaurante.

---

## DELIVERY_REVIEW_CREATED

### Publisher

- order-service

### Consumers

- delivery-service
- AWS Lambda

### Objetivo

Atualizar reputação do entregador.

---

# Topic: notifications

## NOTIFICATION_CREATED

### Publisher

- notification-service

### Consumers

- futuros serviços de monitoramento

---

# Integração com SNS

## Objetivo

Distribuir eventos para múltiplos consumidores.

Exemplo:
```
DELIVERY_COMPLETED

↓

SNS Topic

↓

SQS Queue

↓

AWS Lambda

↓

Atualização de métricas
```
---

# Integração com SQS

## Objetivo

Garantir processamento desacoplado e resiliente.

Exemplos:

- Atualização de métricas
- Processamento de notificações
- Rotinas futuras

---

# AWS Lambda (Python)

## Responsabilidades

### Métricas

- Total de pedidos
- Total de entregas
- Avaliação média
- Faturamento

### Processamentos Assíncronos

- Atualização de dashboards
- Agregações
- Integrações futuras

---

# Benefícios da Arquitetura

## Baixo Acoplamento

Serviços não dependem diretamente uns dos outros.

## Escalabilidade

Consumidores podem crescer independentemente.

## Resiliência

Eventos permanecem disponíveis para reprocessamento.

## Observabilidade

Eventos permitem rastrear o fluxo completo do pedido.

---

# Próximos Passos

1. Criar ADRs
2. Criar Diagramas C4
3. Modelar bancos de dados
4. Definir contratos OpenAPI
5. Implementar microsserviços