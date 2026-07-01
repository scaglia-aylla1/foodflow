# Context Mapping

## Objetivo

Este documento descreve os Bounded Contexts do FoodFlow e os relacionamentos entre eles, seguindo os princípios de Domain-Driven Design (DDD).

Cada contexto representa uma área de negócio independente, com seu próprio modelo de domínio, regras de negócio e banco de dados.

---

# Bounded Contexts

## Auth Context

### Responsabilidades

* Cadastro de usuários
* Autenticação
* Autorização
* Papéis (Roles)
* Endereços
* Aprovação de restaurantes
* Aprovação de entregadores

### Entidades

* User
* Address
* Role

---

## Restaurant Context

### Responsabilidades

* Restaurantes
* Cardápios
* Categorias
* Produtos
* Horários de funcionamento
* Pedido mínimo
* Restaurantes favoritos

### Entidades

* Restaurant
* Category
* Product
* OpeningHours
* FavoriteRestaurant

---

## Order Context

### Responsabilidades

* Pedidos
* Itens do pedido
* Histórico de status
* Avaliações

### Entidades

* Order
* OrderItem
* Review
* OrderStatusHistory

---

## Payment Context

### Responsabilidades

* Pagamentos
* Transações financeiras

### Entidades

* Payment

---

## Delivery Context

### Responsabilidades

* Entregadores
* Entregas
* Código de confirmação

### Entidades

* Driver
* Delivery

---

## Notification Context

### Responsabilidades

* Histórico de notificações
* Leitura de notificações
* Consumo de eventos

### Entidades

* Notification

---

# Relacionamento entre Contextos

| Origem     | Destino      | Tipo de Comunicação |
| ---------- | ------------ | ------------------- |
| Auth       | Restaurant   | REST                |
| Auth       | Delivery     | REST                |
| Order      | Payment      | Evento Kafka        |
| Payment    | Order        | Evento Kafka        |
| Restaurant | Delivery     | Evento Kafka        |
| Delivery   | Order        | Evento Kafka        |
| Todos      | Notification | Evento Kafka        |

---

# Dependências

## Auth Context

Não depende de nenhum outro contexto.

---

## Restaurant Context

Depende do Auth Context para validação da identidade do restaurante.

---

## Order Context

Depende do Restaurant Context para validação do restaurante e do cardápio.

---

## Payment Context

Depende do Order Context por meio do evento `ORDER_CREATED`.

---

## Delivery Context

Depende do Restaurant Context e do Order Context para iniciar a entrega.

---

## Notification Context

Depende exclusivamente dos eventos publicados pelos demais contextos.

---

# Princípios

Cada contexto possui:

* Modelo de domínio próprio.
* Banco de dados próprio.
* Regras de negócio próprias.
* APIs próprias.
* Eventos próprios.

Nenhum contexto acessa diretamente o banco de dados de outro contexto.

---

# Benefícios

A divisão em Bounded Contexts proporciona:

* Baixo acoplamento.
* Alta coesão.
* Evolução independente dos microsserviços.
* Facilidade de manutenção.
* Escalabilidade.
* Clareza das responsabilidades.

---

# Evoluções Futuras

Novos contextos poderão ser adicionados sem impactar os existentes.

Exemplos:

* Coupon Context
* Promotion Context
* Recommendation Context
* Analytics Context
* Search Context

---

# Decisões Arquiteturais Relacionadas

* Domain-Driven Design (DDD)
* Bounded Context
* Database per Service
* Event-Driven Architecture
* Eventual Consistency


## Context Map Diagram

```text
                +----------------------+
                |     Auth Context     |
                |----------------------|
                | Users                |
                | Roles                |
                | Addresses            |
                +----------+-----------+
                           |
                           | REST
                           v
                +----------------------+
                | Restaurant Context   |
                |----------------------|
                | Restaurants          |
                | Products             |
                | Categories           |
                +----------+-----------+
                           |
                           | Kafka
                           v
                +----------------------+
                |   Order Context      |
                |----------------------|
                | Orders               |
                | OrderItems           |
                | Reviews              |
                +-----+--------+------+
                      |        |
                      |        |
                  Kafka       Kafka
                      |        |
                      v        v
        +----------------+   +----------------+
        | Payment Context|   | Delivery Context|
        |----------------|   |----------------|
        | Payments       |   | Deliveries     |
        | Transactions   |   | Drivers        |
        +--------+------+   +--------+-------+
                 \               /
                  \             /
                   \           /
                    v         v
             +----------------------+
             | Notification Context |
             |----------------------|
             | Notifications        |
             +----------------------+