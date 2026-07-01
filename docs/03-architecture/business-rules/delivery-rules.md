# Delivery Business Rules

## Objetivo

Este documento descreve as regras de negócio relacionadas ao gerenciamento das entregas e dos entregadores no FoodFlow.

O Delivery Service é responsável pela atribuição das entregas, acompanhamento do processo de entrega e atualização do status dos entregadores.

---

# Cadastro

### DELIVERY-001

Todo entregador deverá ser aprovado por um administrador antes de realizar entregas.

---

### DELIVERY-002

Enquanto não aprovado, o entregador poderá acessar sua conta, mas não poderá aceitar entregas.

---

### DELIVERY-003

Após a aprovação, o entregador poderá ficar disponível para receber entregas.

---

# Disponibilidade

### DELIVERY-004

O entregador poderá alternar entre os estados ONLINE e OFFLINE.

---

### DELIVERY-005

Somente entregadores ONLINE poderão visualizar entregas disponíveis.

---

### DELIVERY-006

Entregadores OFFLINE não receberão novas entregas.

---

# Aceitação da Entrega

### DELIVERY-007

Uma entrega poderá ser aceita por apenas um entregador.

---

### DELIVERY-008

Após aceitar uma entrega, o entregador terá seu status alterado para BUSY.

---

### DELIVERY-009

Um entregador não poderá aceitar outra entrega enquanto estiver BUSY.

---

# Processo de Entrega

### DELIVERY-010

Após aceitar a entrega, o entregador deverá se deslocar até o restaurante.

---

### DELIVERY-011

O entregador aguardará a conclusão do preparo do pedido.

---

### DELIVERY-012

Quando retirar o pedido, o status da entrega será alterado para OUT_FOR_DELIVERY.

---

### DELIVERY-013

A entrega será considerada concluída somente após a validação do código de confirmação informado pelo cliente.

---

### DELIVERY-014

Após a confirmação da entrega, o entregador retornará automaticamente ao status ONLINE.

---

# Pagamento ao Entregador

### DELIVERY-015

O entregador somente receberá pela entrega após sua conclusão.

---

# Eventos

### DELIVERY-016

Ao aceitar uma entrega, o sistema publicará o evento:

* DELIVERY_ASSIGNED

---

### DELIVERY-017

Ao iniciar o deslocamento ao cliente, o sistema publicará o evento:

* OUT_FOR_DELIVERY

---

### DELIVERY-018

Após a confirmação da entrega, o sistema publicará o evento:

* DELIVERY_COMPLETED

---

# Integridade

### DELIVERY-019

Toda entrega deverá estar associada a um único pedido.

---

### DELIVERY-020

As entregas nunca serão excluídas fisicamente do banco de dados.

---

# Evoluções Futuras

### DELIVERY-021

Na V2, o sistema poderá sugerir automaticamente o entregador mais próximo.

---

### DELIVERY-022

Na V2, será possível acompanhar a localização do entregador em tempo real.

---

### DELIVERY-023

Na V3, o sistema poderá redistribuir automaticamente entregas recusadas ou expiradas.

---

# Observações

O Delivery Service é responsável exclusivamente pela logística de entrega.

Não é responsabilidade deste serviço gerenciar pedidos, pagamentos ou restaurantes.

---

# Decisões Arquiteturais Relacionadas

* Event-Driven Architecture
* Database per Service
* Eventual Consistency
* Domain-Driven Design (DDD)
