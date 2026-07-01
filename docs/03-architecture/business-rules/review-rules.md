# Review Business Rules

## Objetivo

Este documento descreve as regras de negócio relacionadas às avaliações realizadas pelos clientes após a conclusão de um pedido.

As avaliações permitem medir a qualidade do atendimento dos restaurantes e dos entregadores.

---

# Elegibilidade

### REVIEW-001

Somente pedidos com status `DELIVERED` poderão ser avaliados.

---

### REVIEW-002

Somente o cliente que realizou o pedido poderá registrar avaliações.

---

### REVIEW-003

Cada pedido poderá gerar apenas uma avaliação para o restaurante.

---

### REVIEW-004

Cada pedido poderá gerar apenas uma avaliação para o entregador.

---

# Avaliação do Restaurante

### REVIEW-005

A avaliação do restaurante deverá conter uma nota de 1 a 5 estrelas.

---

### REVIEW-006

O comentário é opcional.

---

### REVIEW-007

A nota média do restaurante será calculada com base em todas as avaliações recebidas.

---

# Avaliação do Entregador

### REVIEW-008

A avaliação do entregador deverá conter uma nota de 1 a 5 estrelas.

---

### REVIEW-009

O comentário é opcional.

---

### REVIEW-010

A nota média do entregador será calculada com base em todas as avaliações recebidas.

---

# Integridade

### REVIEW-011

As avaliações nunca poderão ser alteradas após o envio.

---

### REVIEW-012

As avaliações nunca serão excluídas fisicamente do banco de dados.

---

### REVIEW-013

Toda avaliação deverá estar vinculada a um único pedido.

---

# Eventos

### REVIEW-014

Após o envio de uma avaliação, o sistema poderá publicar o evento:

* REVIEW_CREATED

---

# Evoluções Futuras

### REVIEW-015

Na V2, clientes poderão anexar fotos às avaliações.

---

### REVIEW-016

Na V2, restaurantes poderão responder às avaliações.

---

### REVIEW-017

Na V3, o sistema poderá utilizar Inteligência Artificial para identificar avaliações ofensivas ou fraudulentas.

---

### REVIEW-018

A avaliação somente poderá ser registrada dentro de um período de até 30 dias após a conclusão da entrega.

---

# Observações

As avaliações pertencem ao contexto de pedidos, mas influenciam diretamente a reputação de restaurantes e entregadores.

---

# Decisões Arquiteturais Relacionadas

* Domain-Driven Design (DDD)
* Event-Driven Architecture
* Eventual Consistency
* Snapshot Pattern
