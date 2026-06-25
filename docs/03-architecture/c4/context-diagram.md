# FoodFlow - C4 Context Diagram

## Objetivo

Representar os usuários e sistemas externos que interagem com o FoodFlow.

---

# Usuários

## Cliente

Responsável por:

- Buscar restaurantes
- Realizar pedidos
- Acompanhar entregas
- Avaliar restaurantes
- Avaliar entregadores

---

## Restaurante

Responsável por:

- Gerenciar cardápio
- Aceitar pedidos
- Preparar pedidos

---

## Entregador

Responsável por:

- Aceitar entregas
- Atualizar status
- Finalizar entregas

---

## Administrador

Responsável por:

- Aprovar cadastros
- Monitorar a plataforma

---

# Sistemas Externos

## AWS

Serviços utilizados:

- ECS
- RDS
- SNS
- SQS
- Lambda
- API Gateway

---

## Kafka

Responsável pela comunicação assíncrona entre microsserviços.

---

# Visão Simplificada
```
Cliente
↓
FoodFlow
↑
Restaurante

Entregador
↓
FoodFlow

Administrador
↓
FoodFlow

FoodFlow
↓
AWS

FoodFlow
↓
Kafka