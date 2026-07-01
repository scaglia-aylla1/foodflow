# API Design Overview

## Objetivo

Este documento define os padrões de design das APIs REST do FoodFlow, incluindo convenções, versionamento, estrutura de requests e responses, e diretrizes gerais de implementação.

---

# Princípios de API

As APIs do FoodFlow seguem os seguintes princípios:

* RESTful design
* Stateless communication
* Resource-based URLs
* Padronização de responses
* Versionamento explícito
* Separação clara entre comandos e consultas

---

# Versionamento

## API Versioning

Todas as APIs deverão ser versionadas via URL:

```
/api/v1/
```

---

# Convenção de Endpoints

## Padrão geral

```
/api/v1/{resource}
```

Exemplos:

* /api/v1/users
* /api/v1/restaurants
* /api/v1/orders
* /api/v1/payments
* /api/v1/deliveries

---

# HTTP Methods

| Método | Uso                  |
| ------ | -------------------- |
| GET    | Consulta de dados    |
| POST   | Criação de recursos  |
| PUT    | Atualização completa |
| PATCH  | Atualização parcial  |
| DELETE | Remoção lógica       |

---

# Padrão de Request

Todos os requests devem utilizar JSON.

Exemplo:

```json id="req01"
{
  "restaurantId": "UUID",
  "items": [
    {
      "productId": "UUID",
      "quantity": 2
    }
  ],
  "deliveryAddressId": "UUID"
}
```

---

# Padrão de Response

## Sucesso

```json id="res01"
{
  "timestamp": "2026-06-30T14:30:00Z",
  "status": 200,
  "data": {
    "id": "UUID",
    "message": "Operation successful"
  }
}
```

---

## Erro

```json id="err01"
{
  "timestamp": "2026-06-30T14:30:00Z",
  "status": 400,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request data"
  }
}
```

---

# Separação de Contextos

Cada microsserviço possui sua própria API:

## Auth Service

* /auth/register
* /auth/login
* /auth/users
* /auth/addresses

---

## Restaurant Service

* /restaurants
* /restaurants/{id}
* /restaurants/{id}/menu
* /categories

---

## Order Service

* /orders
* /orders/{id}
* /orders/{id}/status
* /orders/{id}/reviews

---

## Payment Service

* /payments
* /payments/{id}

---

## Delivery Service

* /deliveries
* /deliveries/{id}
* /deliveries/{id}/status

---

## Notification Service

* /notifications
* /notifications/{id}
* /notifications/read

---

# Separação Command vs Query

O FoodFlow adota uma separação leve entre comandos e consultas:

## Commands

* Criar pedido
* Confirmar pagamento
* Aceitar entrega

## Queries

* Listar restaurantes
* Consultar pedidos
* Ver notificações

---

# Regras de Consistência

* APIs são stateless
* Não há transações distribuídas
* Consistência é eventual
* Atualizações são propagadas via eventos

---

# Paginação

Listagens devem sempre suportar paginação:

```
?page=0&size=10
```

Resposta padrão:

```json id="pag01"
{
  "content": [],
  "page": 0,
  "size": 10,
  "totalElements": 100,
  "totalPages": 10
}
```

---

# Segurança

* Todas as APIs protegidas exigem JWT
* Token deve ser enviado via header Authorization
* Endpoints públicos devem ser explicitamente documentados

---

# Padronização de Erros

## Códigos comuns

| Código | Descrição              |
| ------ | ---------------------- |
| 400    | Erro de validação      |
| 401    | Não autenticado        |
| 403    | Sem permissão          |
| 404    | Recurso não encontrado |
| 500    | Erro interno           |

---

# Boas Práticas

* Evitar endpoints aninhados excessivos
* Não expor entidades internas diretamente
* Usar DTOs para entrada e saída
* Evitar acoplamento com modelos de banco
* Versionar mudanças incompatíveis

---

# Evoluções Futuras

* Introdução de GraphQL para consultas específicas
* API Gateway centralizado
* Rate limiting por usuário
* Cache distribuído
* WebSockets para tracking de pedidos em tempo real

---

# Decisões Arquiteturais Relacionadas

* RESTful Architecture
* Microservices Architecture
* Event-Driven Architecture
* JWT Authentication
* Stateless APIs
