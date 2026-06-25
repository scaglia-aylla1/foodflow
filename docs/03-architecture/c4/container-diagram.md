# FoodFlow - C4 Container Diagram

## Objetivo

Representar os containers (microsserviços) que compõem a solução.

---

# API Gateway

Ponto único de entrada para clientes externos.

Rotas:

- /auth
- /restaurants
- /orders
- /payments
- /deliveries

---

# Auth Service

Tecnologias:

- Java 21
- Spring Boot
- Spring Security
- JWT
- MySQL

Responsabilidades:

- Cadastro
- Login
- Autorização

---

# Restaurant Service

Tecnologias:

- Java 21
- Spring Boot
- MySQL

Responsabilidades:

- Restaurantes
- Cardápios
- Produtos
- Categorias

---

# Order Service

Tecnologias:

- Java 21
- Spring Boot
- Kafka
- MySQL

Responsabilidades:

- Pedidos
- Itens
- Avaliações

---

# Payment Service

Tecnologias:

- Java 21
- Spring Boot
- Kafka
- MySQL

Responsabilidades:

- Pagamentos
- Reembolsos

---

# Delivery Service

Tecnologias:

- Java 21
- Spring Boot
- Kafka
- MySQL

Responsabilidades:

- Entregadores
- Entregas

---

# Notification Service

Tecnologias:

- Java 21
- Spring Boot
- Kafka
- SNS
- SQS

Responsabilidades:

- Notificações
- Processamento de eventos

---

# AWS Lambda

Tecnologia:

- Python

Responsabilidades:

- Métricas
- Processamentos assíncronos

---

# Kafka

Topics:

- orders
- payments
- deliveries
- reviews
- notifications

---

# Bancos de Dados

- Auth DB

- Restaurant DB

- Order DB

- Payment DB

- Delivery DB

- Notification DB

---

# Fluxo Simplificado
```
Cliente
↓
API Gateway

↓

Auth Service

Restaurant Service

Order Service

Payment Service

Delivery Service

Notification Service

↓

Kafka

↓

AWS Lambda

↓

SNS / SQS

↓

RDS