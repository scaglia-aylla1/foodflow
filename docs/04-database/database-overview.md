# Database Overview

## Objetivo

Este documento apresenta a visão geral da arquitetura de dados do FoodFlow.

Cada microsserviço possui seu próprio banco de dados, seguindo o padrão **Database per Service**, garantindo baixo acoplamento, autonomia e independência entre os serviços.

Não existem acessos diretos ao banco de dados de outro microsserviço.

Toda comunicação entre serviços ocorre através de APIs ou eventos publicados no Kafka.

---

# Princípios Arquiteturais

O FoodFlow adota os seguintes princípios para persistência de dados:

* Cada microsserviço é proprietário exclusivo de seu banco de dados.
* Não existem Foreign Keys entre bancos diferentes.
* A comunicação ocorre apenas por APIs REST ou eventos Kafka.
* Cada serviço é responsável por manter a consistência dos seus próprios dados.
* A consistência global do sistema é eventual (Eventual Consistency).

---

# Visão Geral

## Auth Service

Responsável pela autenticação e autorização dos usuários.

### Entidades

* User
* Address
* Role

---

## Restaurant Service

Responsável pelos restaurantes, cardápios e categorias.

### Entidades

* Restaurant
* Category
* Product
* OpeningHours
* FavoriteRestaurant

---

## Order Service

Responsável pelo ciclo de vida dos pedidos.

### Entidades

* Order
* OrderItem
* Review

---

## Payment Service

Responsável pelo processamento financeiro.

### Entidades

* Payment

---

## Delivery Service

Responsável pelo gerenciamento das entregas.

### Entidades

* Driver
* Delivery

---

## Notification Service

Responsável pelas notificações enviadas aos usuários.

### Entidades

* Notification

---

# Comunicação entre os Serviços

| Serviço              | Banco Próprio | Comunicação  |
| -------------------- | ------------- | ------------ |
| Auth Service         | Sim           | REST + Kafka |
| Restaurant Service   | Sim           | REST + Kafka |
| Order Service        | Sim           | Kafka        |
| Payment Service      | Sim           | Kafka        |
| Delivery Service     | Sim           | Kafka        |
| Notification Service | Sim           | Kafka        |

---

# Propriedade dos Dados (Data Ownership)

Cada informação possui um único proprietário dentro da arquitetura.

| Informação      | Serviço Responsável  |
| --------------- | -------------------- |
| Usuários        | Auth Service         |
| Endereços       | Auth Service         |
| Restaurantes    | Restaurant Service   |
| Produtos        | Restaurant Service   |
| Categorias      | Restaurant Service   |
| Pedidos         | Order Service        |
| Itens do Pedido | Order Service        |
| Avaliações      | Order Service        |
| Pagamentos      | Payment Service      |
| Entregadores    | Delivery Service     |
| Entregas        | Delivery Service     |
| Notificações    | Notification Service |

---

# Compartilhamento de Dados

Os microsserviços não compartilham tabelas.

Quando um serviço precisa referenciar uma entidade pertencente a outro contexto, utiliza apenas o identificador (UUID).

Exemplos:

* customerId
* restaurantId
* driverId
* orderId

Essa estratégia elimina dependências entre bancos de dados e facilita a evolução independente de cada microsserviço.

---

# Consistência dos Dados

O FoodFlow utiliza o padrão **Eventual Consistency**.

Fluxo simplificado:

1. O Order Service cria um pedido.
2. O Order Service publica o evento `ORDER_CREATED`.
3. O Payment Service processa o pagamento.
4. O Payment Service publica `PAYMENT_APPROVED` ou `PAYMENT_REJECTED`.
5. Os demais microsserviços atualizam seus estados de forma independente.

Não existem transações distribuídas entre os bancos.

---

# Visão Geral da Arquitetura

```text
                           +----------------------+
                           |     Auth Service     |
                           | User                 |
                           | Address              |
                           | Role                 |
                           +----------+-----------+
                                      |
                                      |
                                      v

                 +---------------------------------------+
                 |            Kafka / Event Bus          |
                 +---------------------------------------+
                     |                           |
                     v                           v 
        +--------------------+          +---------------------+
        | Restaurant Service |          |    Order Service    |
        | Restaurant         |<-------->| Order               |
        | Product            |          | OrderItem           |
        | Category           |          | Review              |
        | OpeningHours       |          +----------+----------+
        | FavoriteRestaurant |                     |
        +---------+----------+                     |
                  |                                |
                  |                                |
                  v                                v

        +--------------------+          +---------------------+
        | Payment Service    |          | Delivery Service    |
        | Payment            |          | Driver              |
        +---------+----------+          | Delivery            |
                  |                     +----------+----------+
                  |                                |
                  +----------------+---------------+
                                   |
                                   v

                    +-------------------------------+
                    | Notification Service          |
                    | Notification                  |
                    +-------------------------------+
```

---

# Decisões Arquiteturais Relacionadas

* Database per Service
* Event-Driven Architecture
* Eventual Consistency
* Data Ownership
* Event-Carried State Transfer
* Domain-Driven Design (DDD)

---

# Evoluções Futuras

Na V2 e V3 poderão ser adicionados novos microsserviços sem necessidade de alterações estruturais nos bancos existentes, preservando a autonomia e o baixo acoplamento da arquitetura.
