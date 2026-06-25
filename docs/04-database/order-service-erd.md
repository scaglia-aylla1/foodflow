# Order Service - Database Model

## Objetivo

Este documento descreve a modelagem de dados do Order Service, responsável pelo gerenciamento de pedidos, itens de pedidos e avaliações.

---

# Entidades

## Order

Representa um pedido realizado por um cliente.

### Campos

| Campo                | Tipo      |
| -------------------- | --------- |
| id                   | UUID      |
| customerId           | UUID      |
| restaurantId         | UUID      |
| status               | ENUM      |
| totalAmount          | DECIMAL   |
| deliveryStreet       | VARCHAR   |
| deliveryNumber       | VARCHAR   |
| deliveryNeighborhood | VARCHAR   |
| deliveryCity         | VARCHAR   |
| deliveryZipCode      | VARCHAR   |
| createdAt            | TIMESTAMP |
| updatedAt            | TIMESTAMP |

### Status

* CREATED
* PAYMENT_PENDING
* PAID
* ACCEPTED
* PREPARING
* READY_FOR_PICKUP
* OUT_FOR_DELIVERY
* DELIVERED
* CANCELLED

---

## OrderItem

Representa um item pertencente a um pedido.

### Campos

| Campo       | Tipo      |
| ----------- | --------- |
| id          | UUID      |
| orderId     | UUID      |
| productId   | UUID      |
| productName | VARCHAR   |
| unitPrice   | DECIMAL   |
| quantity    | INTEGER   |
| totalPrice  | DECIMAL   |
| observation | VARCHAR   |
| createdAt   | TIMESTAMP |

---

## Review

Representa uma avaliação realizada pelo cliente.

### Campos

| Campo      | Tipo      |
| ---------- | --------- |
| id         | UUID      |
| orderId    | UUID      |
| customerId | UUID      |
| targetType | ENUM      |
| targetId   | UUID      |
| rating     | INTEGER   |
| comment    | VARCHAR   |
| createdAt  | TIMESTAMP |

### TargetType

* RESTAURANT
* DELIVERY_DRIVER

### Regras

* Rating deve estar entre 1 e 5.
* Um cliente só pode avaliar após a entrega ser concluída.

---

# Relacionamentos

Order

1 → N OrderItem

Order

1 → N Review

---

# Observações

O Order Service segue o padrão Database Per Service.

Não existirão Foreign Keys para bancos pertencentes a outros microsserviços.

Os campos customerId, restaurantId e productId serão utilizados apenas como referências de negócio.
