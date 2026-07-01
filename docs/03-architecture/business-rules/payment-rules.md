# Payment Business Rules

## Objetivo

Este documento descreve as regras de negócio relacionadas ao processamento dos pagamentos no FoodFlow.

O Payment Service é responsável por processar pagamentos, registrar transações e publicar os eventos financeiros da plataforma.

---

# Processamento

### PAY-001

Todo pagamento pertence a um único pedido.

---

### PAY-002

Cada pedido possui apenas um pagamento no MVP.

---

### PAY-003

O processamento do pagamento ocorre de forma assíncrona através de eventos Kafka.

---

### PAY-004

O Payment Service recebe o evento `ORDER_CREATED` para iniciar o processamento.

---

### PAY-005

O Payment Service não consulta diretamente o Order Service para obter informações do pedido.

Os dados necessários são recebidos através do evento `ORDER_CREATED`.

---

# Métodos de Pagamento

### PAY-006

Os métodos de pagamento suportados no MVP são:

* PIX
* Cartão de Crédito
* Cartão de Débito

---

### PAY-007

Dados sensíveis, como número do cartão, CVV e data de validade, não serão armazenados pelo FoodFlow.

---

# Aprovação

### PAY-008

No MVP, o pagamento será processado por um simulador interno.

---

### PAY-009

O simulador aprovará aproximadamente 90% dos pagamentos e rejeitará aproximadamente 10%.

---

### PAY-010

Após processado, o pagamento receberá um dos seguintes status:

* APPROVED
* REJECTED

---

### PAY-011

Após deixar o estado `PENDING`, o pagamento não poderá retornar para esse estado.

---

# Eventos

### PAY-012

Pagamentos aprovados publicam o evento:

* PAYMENT_APPROVED

---

### PAY-013

Pagamentos rejeitados publicam o evento:

* PAYMENT_REJECTED

---

# Integridade

### PAY-014

Todas as transações deverão possuir um identificador único (`providerTransactionId`).

---

### PAY-015

Os registros de pagamento nunca serão excluídos fisicamente do banco de dados.

---

# Evoluções Futuras

### PAY-016

Na V3, o sistema poderá integrar gateways reais de pagamento, como:

* Mercado Pago
* Stripe
* PagSeguro
* Asaas

---

### PAY-017

Na V3, será possível registrar múltiplas tentativas de pagamento para um mesmo pedido.

---

# Observações

O Payment Service é responsável exclusivamente pelos dados financeiros.

Não é responsabilidade deste serviço gerenciar pedidos, entregas ou usuários.

---

# Decisões Arquiteturais Relacionadas

* Event-Driven Architecture
* Event-Carried State Transfer
* Database per Service
* Eventual Consistency
