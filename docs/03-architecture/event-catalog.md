# Event Catalog

## Objetivo

Este documento descreve todos os eventos publicados e consumidos pelos microsserviços do FoodFlow.

O catálogo de eventos serve como contrato de comunicação entre os serviços, garantindo baixo acoplamento e integração baseada em eventos.

---

# Convenções

Todos os eventos seguem o padrão:

* Nome em UPPER_SNAKE_CASE
* Payload em JSON
* Identificador único (UUID)
* Data e hora do evento

Cada evento possui:

* Producer
* Consumers
* Payload
* Descrição

---

# ORDER_CREATED

## Producer

Order Service

## Consumers

* Payment Service
* Notification Service

## Descrição

Publicado quando um pedido é criado com sucesso.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T14:30:00Z",
  "orderId": "UUID",
  "customerId": "UUID",
  "restaurantId": "UUID",
  "amount": 85.90
}
```

---

# PAYMENT_APPROVED

## Producer

Payment Service

## Consumers

* Order Service
* Notification Service

## Descrição

Publicado quando o pagamento é aprovado.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T14:31:00Z",
  "paymentId": "UUID",
  "orderId": "UUID",
  "status": "APPROVED"
}
```

---

# PAYMENT_REJECTED

## Producer

Payment Service

## Consumers

* Order Service
* Notification Service

## Descrição

Publicado quando o pagamento é rejeitado.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T14:31:00Z",
  "paymentId": "UUID",
  "orderId": "UUID",
  "status": "REJECTED"
}
```

---

# ORDER_ACCEPTED

## Producer

Restaurant Service

## Consumers

* Delivery Service
* Notification Service

## Descrição

Publicado quando o restaurante aceita o pedido.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T14:35:00Z",
  "orderId": "UUID",
  "restaurantId": "UUID"
}
```

---

# ORDER_PREPARING

## Producer

Restaurant Service

## Consumers

* Notification Service

## Descrição

Publicado quando o restaurante inicia o preparo do pedido.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T14:40:00Z",
  "orderId": "UUID"
}
```

---

# DELIVERY_ASSIGNED

## Producer

Delivery Service

## Consumers

* Order Service
* Notification Service

## Descrição

Publicado quando um entregador aceita uma entrega.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T14:45:00Z",
  "deliveryId": "UUID",
  "orderId": "UUID",
  "driverId": "UUID"
}
```

---

# OUT_FOR_DELIVERY

## Producer

Delivery Service

## Consumers

* Order Service
* Notification Service

## Descrição

Publicado quando o entregador inicia o trajeto até o cliente.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T15:05:00Z",
  "deliveryId": "UUID",
  "orderId": "UUID"
}
```

---

# DELIVERY_COMPLETED

## Producer

Delivery Service

## Consumers

* Order Service
* Notification Service

## Descrição

Publicado após a confirmação da entrega pelo código informado pelo cliente.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T15:20:00Z",
  "deliveryId": "UUID",
  "orderId": "UUID"
}
```

---

# REVIEW_CREATED

## Producer

Order Service

## Consumers

* Restaurant Service

## Descrição

Publicado quando um cliente registra uma avaliação.

## Payload

```json
{
  "eventId": "UUID",
  "occurredAt": "2026-06-30T15:30:00Z",
  "reviewId": "UUID",
  "orderId": "UUID",
  "rating": 5
}
```

---

# RESTAURANT_APPROVED

## Producer

Auth Service

## Consumers

* Notification Service

## Descrição

Publicado quando um restaurante é aprovado por um administrador.

---

# DRIVER_APPROVED

## Producer

Auth Service

## Consumers

* Notification Service

## Descrição

Publicado quando um entregador é aprovado por um administrador.

---

# Convenções de Payload

Todos os eventos deverão conter, sempre que aplicável:

* eventId
* occurredAt
* aggregateId
* aggregateType
* eventType

Além dos dados específicos de cada evento.

---

# Observações

Os microsserviços não realizam chamadas diretas para sincronizar estados.

Toda sincronização ocorre através dos eventos publicados no Kafka.

Cada serviço é responsável por atualizar seu próprio estado após consumir um evento.

---

# Decisões Arquiteturais Relacionadas

* Event-Driven Architecture
* Event-Carried State Transfer
* Eventual Consistency
* Database per Service
* Domain-Driven Design (DDD)
