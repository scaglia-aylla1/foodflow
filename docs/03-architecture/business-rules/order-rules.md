# Order Business Rules

## Objetivo

Este documento descreve as regras de negócio relacionadas ao ciclo de vida dos pedidos no FoodFlow.

O Order Service é responsável por gerenciar os pedidos desde sua criação até sua conclusão ou cancelamento.

---

# Criação do Pedido

### ORDER-001

Todo pedido deve pertencer a um único cliente.

---

### ORDER-002

Todo pedido deve pertencer a um único restaurante.

---

### ORDER-003

Todo pedido deve possuir pelo menos um item.

---

### ORDER-004

Todos os itens do pedido devem pertencer ao mesmo restaurante.

---

### ORDER-005

O valor total do pedido deve ser igual à soma dos valores dos itens.

---

### ORDER-006

O pedido deve atender ao valor mínimo definido pelo restaurante.

---

### ORDER-007

No momento da criação, o pedido deve armazenar um snapshot das informações dos produtos.

---

# Pagamento

### ORDER-008

Após a criação, o pedido aguardará o processamento do pagamento.

---

### ORDER-009

Enquanto o pagamento estiver pendente, o restaurante não visualizará o pedido.

---

### ORDER-010

Pagamento aprovado altera o status do pedido para **PAID**.

---

### ORDER-011

Pagamento rejeitado altera o status do pedido para **CANCELLED**.

---

# Aceitação pelo Restaurante

### ORDER-012

Somente pedidos pagos poderão ser aceitos pelo restaurante.

---

### ORDER-013

O restaurante poderá aceitar ou recusar o pedido.

---

### ORDER-014

Ao aceitar o pedido, o restaurante inicia sua preparação.

---

### ORDER-015

Pedidos recusados pelo restaurante serão cancelados.

---

# Preparação

### ORDER-016

Durante a preparação, o pedido não poderá ser cancelado pelo cliente.

---

### ORDER-017

Ao finalizar a preparação, o pedido ficará disponível para atribuição de um entregador.

---

# Cancelamento

### ORDER-018

O cliente poderá cancelar o pedido apenas antes da aceitação pelo restaurante.

---

### ORDER-019

Pedidos cancelados não poderão ser reativados.

---

# Entrega

### ORDER-020

Após um entregador aceitar a entrega, o pedido terá o status **DRIVER_ASSIGNED**.

---

### ORDER-021

Quando o entregador iniciar o deslocamento ao cliente, o pedido terá o status **OUT_FOR_DELIVERY**.

---

### ORDER-022

A entrega será considerada concluída somente após a validação do código de confirmação informado pelo cliente.

---

### ORDER-023

Após a confirmação da entrega, o pedido terá o status **DELIVERED**.

---

# Avaliação

### ORDER-024

Somente pedidos entregues poderão ser avaliados.

---

### ORDER-025

Cada pedido permitirá apenas uma avaliação do restaurante.

---

### ORDER-026

Cada pedido permitirá apenas uma avaliação do entregador.

---

# Integridade

### ORDER-027

Pedidos nunca serão excluídos fisicamente do banco de dados.

---

### ORDER-028

Todas as alterações de status deverão ser registradas no histórico do pedido.

---

# Eventos

### ORDER-029

Ao criar um pedido, o Order Service deverá publicar o evento:

* ORDER_CREATED

---

### ORDER-030

Sempre que houver alteração de status, os eventos correspondentes deverão ser publicados para os demais microsserviços.

---

# Observações

O Order Service é responsável apenas pelas informações do pedido.

Pagamentos, entregas, restaurantes, notificações e usuários são gerenciados pelos respectivos microsserviços.

---

# Decisões Arquiteturais Relacionadas

* Snapshot Pattern
* Event-Driven Architecture
* Database per Service
* Eventual Consistency
* Domain-Driven Design (DDD)
