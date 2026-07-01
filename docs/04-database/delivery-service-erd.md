# Delivery Service - Database Model

## Objetivo

Este documento descreve a modelagem de dados do Delivery Service, responsável pelo gerenciamento das entregas, disponibilidade dos entregadores e confirmação da entrega.

---

# Entidades

## Driver

Representa um entregador da plataforma.

### Campos

| Campo           | Tipo          |
| --------------- | ------------- |
| id              | UUID          |
| userId          | UUID          |
| vehicleType     | ENUM          |
| averageRating   | DECIMAL(3,2)  |
| totalReviews    | INTEGER       |
| totalDeliveries | INTEGER       |
| totalEarnings   | DECIMAL(10,2) |
| isOnline        | BOOLEAN       |
| createdAt       | TIMESTAMP     |
| updatedAt       | TIMESTAMP     |

---

### VehicleType

* MOTORCYCLE
* BICYCLE
* CAR

---

### Regras

* Um entregador deve estar aprovado no Auth Service para ficar online.
* Apenas entregadores online podem aceitar entregas.
* Um entregador pode possuir apenas uma entrega ativa por vez.
* As métricas (`averageRating`, `totalReviews`, `totalDeliveries` e `totalEarnings`) são atualizadas por eventos.

---

## Delivery

Representa uma entrega vinculada a um pedido.

### Campos

| Campo            | Tipo          |
| ---------------- | ------------- |
| id               | UUID          |
| orderId          | UUID          |
| driverId         | UUID          |
| deliveryFee      | DECIMAL(10,2) |
| confirmationCode | VARCHAR(6)    |
| status           | ENUM          |
| assignedAt       | TIMESTAMP     |
| pickedUpAt       | TIMESTAMP     |
| outForDeliveryAt | TIMESTAMP     |
| deliveredAt      | TIMESTAMP     |
| createdAt        | TIMESTAMP     |
| updatedAt        | TIMESTAMP     |

---

### DeliveryStatus

* AVAILABLE
* ASSIGNED
* PICKED_UP
* OUT_FOR_DELIVERY
* DELIVERED
* CANCELLED

---

### Fluxo da Entrega

```text
AVAILABLE
    ↓
ASSIGNED
    ↓
PICKED_UP
    ↓
OUT_FOR_DELIVERY
    ↓
DELIVERED
```

---

### Regras

* A entrega é criada quando o restaurante aceita o pedido.
* A entrega fica disponível para os entregadores online.
* O primeiro entregador que aceitar torna-se responsável pela entrega.
* O código de confirmação é gerado quando o pedido sai para entrega (`OUT_FOR_DELIVERY`).
* A entrega somente pode ser finalizada mediante validação do código informado pelo cliente.
* Após a confirmação da entrega, o código torna-se inválido.
* Após a entrega concluída:

  * O entregador recebe o valor da entrega.
  * O cliente pode avaliar o restaurante.
  * O cliente pode avaliar o entregador.

---

# Relacionamentos

Driver

1 → N Delivery

---

# Índices Recomendados

## Driver

* IDX(userId)
* IDX(isOnline)

## Delivery

* UK(orderId)
* IDX(driverId)
* IDX(status)

---

# Eventos Produzidos

* DELIVERY_ASSIGNED
* DELIVERY_PICKED_UP
* OUT_FOR_DELIVERY
* DELIVERY_COMPLETED

---

# Eventos Consumidos

* ORDER_ACCEPTED

---

# Observações

O Delivery Service segue o padrão **Database Per Service**.

O campo `userId` referencia um usuário existente no Auth Service, sem utilização de Foreign Key entre bancos.

O campo `orderId` referencia um pedido existente no Order Service, também sem Foreign Key.

Toda comunicação entre microsserviços ocorrerá através de APIs REST e eventos Kafka.
