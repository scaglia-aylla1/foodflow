# Restaurant Service - Database Model

## Objetivo

Este documento descreve a modelagem de dados do Restaurant Service, responsável pelo gerenciamento de restaurantes, categorias, produtos e horários de funcionamento.

---

# Entidades

## Restaurant

Representa um restaurante cadastrado na plataforma.

### Campos

| Campo             | Tipo      |
| ----------------- | --------- |
| id                | UUID      |
| name              | VARCHAR   |
| description       | VARCHAR   |
| phone             | VARCHAR   |
| street            | VARCHAR   |
| number            | VARCHAR   |
| neighborhood      | VARCHAR   |
| city              | VARCHAR   |
| zipCode           | VARCHAR   |
| deliveryFee       | DECIMAL   |
| minimumOrderValue | DECIMAL   |
| averageRating     | DECIMAL   |
| totalReviews      | INTEGER   |
| isOpen            | BOOLEAN   |
| isApproved        | BOOLEAN   |
| isActive          | BOOLEAN   |
| createdAt         | TIMESTAMP |
| updatedAt         | TIMESTAMP |

---

## Category

Representa uma categoria do cardápio.

### Campos

| Campo        | Tipo      |
| ------------ | --------- |
| id           | UUID      |
| restaurantId | UUID      |
| name         | VARCHAR   |
| description  | VARCHAR   |
| isActive     | BOOLEAN   |
| createdAt    | TIMESTAMP |

### Regras

* Utiliza Soft Delete.
* Categorias inativas não devem ser exibidas aos clientes.

---

## Product

Representa um item comercializado pelo restaurante.

### Campos

| Campo        | Tipo      |
| ------------ | --------- |
| id           | UUID      |
| restaurantId | UUID      |
| categoryId   | UUID      |
| name         | VARCHAR   |
| description  | VARCHAR   |
| price        | DECIMAL   |
| available    | BOOLEAN   |
| createdAt    | TIMESTAMP |
| updatedAt    | TIMESTAMP |

### Regras

* Produtos indisponíveis permanecem cadastrados.
* Produtos indisponíveis não podem ser adicionados ao carrinho.

---

## OpeningHours

Representa os horários de funcionamento do restaurante.

### Campos

| Campo        | Tipo    |
| ------------ | ------- |
| id           | UUID    |
| restaurantId | UUID    |
| dayOfWeek    | VARCHAR |
| openTime     | TIME    |
| closeTime    | TIME    |

### Exemplo

| Dia     | Abertura | Fechamento |
| ------- | -------- | ---------- |
| MONDAY  | 18:00    | 23:00      |
| TUESDAY | 18:00    | 23:00      |
| SUNDAY  | 11:00    | 22:00      |

---

# Relacionamentos

Restaurant

1 → N Category

Restaurant

1 → N Product

Restaurant

1 → N OpeningHours

Category

1 → N Product

---

# Métricas

Os campos abaixo serão atualizados através de eventos Kafka:

* averageRating
* totalReviews

Evento consumido:

RESTAURANT_REVIEW_CREATED

---

# Observações

O Restaurant Service segue o padrão Database Per Service.

Não existirão Foreign Keys para bancos pertencentes a outros microsserviços.

As avaliações dos restaurantes são armazenadas no Order Service e propagadas através de eventos Kafka.
