# Notification Business Rules

## Objetivo

Este documento descreve as regras de negócio relacionadas ao envio, persistência e gerenciamento das notificações do FoodFlow.

O Notification Service centraliza todas as notificações da plataforma e mantém um histórico para consulta pelos usuários.

---

# Geração de Notificações

### NOTIFY-001

Toda notificação deverá ser originada a partir de um evento publicado por outro microsserviço.

---

### NOTIFY-002

O Notification Service apenas consome eventos, não iniciando processos de negócio.

---

# Destinatário

### NOTIFY-003

Toda notificação deverá possuir um único destinatário.

---

### NOTIFY-004

O destinatário será identificado pelo `recipientId`.

---

# Persistência

### NOTIFY-005

Todas as notificações serão persistidas no banco de dados.

---

### NOTIFY-006

Toda notificação será criada inicialmente com o status de não lida (`isRead = false`).

---

### NOTIFY-007

Ao ser visualizada pelo usuário, a notificação será marcada como lida (`isRead = true`) e a data de leitura será registrada.

---

# Navegação

### NOTIFY-008

A notificação poderá conter um `referenceType` e um `referenceId` para permitir a navegação direta para o recurso relacionado.

---

# Canal de Envio

### NOTIFY-009

No MVP, todas as notificações utilizarão exclusivamente o canal `IN_APP`.

---

### NOTIFY-010

O canal utilizado será armazenado no campo `channel`.

---

# Eventos Consumidos

### NOTIFY-011

O Notification Service poderá consumir, entre outros, os seguintes eventos:

* RESTAURANT_APPROVED
* DRIVER_APPROVED
* ORDER_CREATED
* ORDER_ACCEPTED
* ORDER_PREPARING
* PAYMENT_APPROVED
* PAYMENT_REJECTED
* DELIVERY_ASSIGNED
* OUT_FOR_DELIVERY
* DELIVERY_COMPLETED

---

# Integridade

### NOTIFY-012

O Notification Service não realizará consultas diretas aos bancos de dados de outros microsserviços.

Todas as informações necessárias deverão estar presentes no evento recebido.

---

### NOTIFY-013

As notificações nunca serão excluídas fisicamente do banco de dados.

---

# Evoluções Futuras

### NOTIFY-014

Na V2, o sistema poderá enviar notificações por:

* E-mail
* Push Notification
* SMS

---

### NOTIFY-015

Na V2, o usuário poderá configurar suas preferências de recebimento por canal.

---

### NOTIFY-016

Na V3, será possível enviar uma mesma notificação por múltiplos canais simultaneamente.

---

# Observações

O Notification Service é um consumidor de eventos e não altera o estado dos demais microsserviços.

Sua responsabilidade é informar os usuários sobre acontecimentos relevantes da plataforma.

---

# Decisões Arquiteturais Relacionadas

* Event-Driven Architecture
* Database per Service
* Event-Carried State Transfer
* Single Responsibility Principle
