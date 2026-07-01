# Notification Service - Database Model

## Objetivo

Este documento descreve a modelagem de dados do Notification Service, responsável pelo gerenciamento e persistência das notificações enviadas aos usuários da plataforma.

O Notification Service centraliza todas as notificações do FoodFlow, permitindo que os usuários consultem seu histórico de mensagens diretamente pelo aplicativo.

---

# Responsabilidades

O Notification Service é responsável por:

* Receber eventos publicados pelos demais microsserviços.
* Persistir notificações.
* Disponibilizar histórico de notificações.
* Controlar leitura das notificações.
* Fornecer informações para navegação do usuário.

Não é responsabilidade deste serviço:

* Gerenciar pedidos.
* Processar pagamentos.
* Gerenciar entregas.
* Gerenciar usuários.

---

# Entidades

## Notification

Representa uma notificação destinada a um usuário.

### Campos

| Campo | Tipo |
|---------|---------|
| id | UUID |
| recipientId | UUID |
| type | ENUM |
| channel | ENUM |
| title | VARCHAR(150) |
| message | TEXT |
| referenceType | ENUM |
| referenceId | UUID |
| isRead | BOOLEAN |
| createdAt | TIMESTAMP |
| readAt | TIMESTAMP |

---

# NotificationType

* ORDER
* PAYMENT
* DELIVERY
* SYSTEM

---
# NotificationChannel

- IN_APP
- EMAIL
- PUSH
- SMS

# ReferenceType

* ORDER
* PAYMENT
* DELIVERY

---

# Fluxo
```
Microsserviço publica um evento

↓

Notification Service recebe o evento

↓

Cria uma notificação

↓

Persiste no banco

↓

Usuário visualiza no aplicativo

↓

Notificação marcada como lida
```
---

# Regras de Negócio

## BR-001

Toda notificação pertence a um único usuário.

---

## BR-002

Uma notificação nasce com:

* isRead = false

---

## BR-003

Ao visualizar a notificação:

* isRead = true
* readAt recebe a data e hora da leitura.

---

## BR-004

A navegação da aplicação utiliza:

* referenceType
* referenceId

para abrir a tela correspondente.

---

## BR-005

O Notification Service nunca consulta diretamente outros bancos de dados.

Toda informação necessária chega através dos eventos publicados.

---

## BR-006

No MVP todas as notificações serão enviadas através do canal:

- IN_APP

Os demais canais serão implementados nas próximas versões da aplicação.

# Índices Recomendados

* IDX(recipientId)
* IDX(isRead)
* IDX(createdAt)

---

# Eventos Consumidos

## Cadastro

* RESTAURANT_APPROVED
* DRIVER_APPROVED

## Pedido

* ORDER_CREATED
* ORDER_CANCELLED

## Pagamento

* PAYMENT_APPROVED
* PAYMENT_REJECTED

## Restaurante

* ORDER_ACCEPTED
* ORDER_PREPARING

## Entrega

* DELIVERY_ASSIGNED
* OUT_FOR_DELIVERY
* DELIVERY_COMPLETED

---

# Eventos Produzidos

Nenhum.

O Notification Service apenas consome eventos.

---

# Observações

O Notification Service segue o padrão **Database Per Service**.

Nenhum microsserviço acessa diretamente suas tabelas.

Toda comunicação ocorre através de eventos Kafka.

---

# Evoluções Futuras (V2)

- Envio de notificações por e-mail.
- Envio de notificações Push.
- Envio de SMS.
- Preferências de notificação por usuário.
- Possibilidade de enviar a mesma notificação por múltiplos canais.
- Expiração automática de notificações.

---

# Decisões Arquiteturais Relacionadas

* Database Per Service.
* Event-Driven Architecture.
* Event-Carried State Transfer.
* Single Responsibility Principle.
