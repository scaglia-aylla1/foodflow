# Payment Service - Database Model

## Objetivo

Este documento descreve a modelagem de dados do Payment Service, responsável pelo processamento dos pagamentos, armazenamento das transações financeiras e publicação dos eventos relacionados ao pagamento.

O Payment Service é o único responsável pelos dados financeiros do sistema.

---

# Responsabilidades

O Payment Service é responsável por:

- Processar pagamentos
- Aprovar ou rejeitar pagamentos
- Persistir informações da transação
- Publicar eventos relacionados ao pagamento
- Manter histórico das transações

Não é responsabilidade deste serviço:

- Gerenciar pedidos
- Gerenciar restaurantes
- Gerenciar entregas
- Gerenciar usuários

---

# Entidades

## Payment

Representa uma tentativa de pagamento realizada para um pedido.

### Campos

| Campo | Tipo |
|---------|---------|
| id | UUID |
| orderId | UUID |
| customerId | UUID |
| amount | DECIMAL(10,2) |
| paymentMethod | ENUM |
| status | ENUM |
| providerTransactionId | UUID |
| processedAt | TIMESTAMP |
| createdAt | TIMESTAMP |
| updatedAt | TIMESTAMP |

---

# PaymentMethod

- PIX
- CREDIT_CARD
- DEBIT_CARD

---

# PaymentStatus

- PENDING
- APPROVED
- REJECTED

---

# Fluxo do Pagamento
```
Pedido criado

↓

Evento ORDER_CREATED

↓

Payment Service recebe o evento

↓

Processa pagamento

↓

Pagamento aprovado ou rejeitado

↓

Publica evento correspondente
```

---

# Regras de Negócio

## BR-001

Todo pagamento pertence a exatamente um pedido.

---

## BR-002

Um pedido possui apenas um pagamento no MVP.

---

## BR-003

O valor do pagamento é recebido através do evento ORDER_CREATED.

O Payment Service não consulta o Order Service para obter o valor.

---

## BR-004

Os dados financeiros pertencem exclusivamente ao Payment Service.

---

## BR-005

O processamento do pagamento ocorre de forma assíncrona através do Kafka.

---

## BR-006

No MVP o pagamento será simulado internamente.

Não haverá integração com gateways externos.

---

## BR-007

Durante a simulação:

- aproximadamente 90% dos pagamentos serão aprovados
- aproximadamente 10% serão rejeitados

Esta proporção existe apenas para permitir testes dos diferentes fluxos da aplicação.

---

## BR-008

Após o pagamento ser processado seu status não poderá retornar para PENDING.

---

# Relacionamentos

Payment

N → 1 Order (referenciado através do orderId)

Não existe Foreign Key entre microsserviços.

---

# Índices Recomendados

- UK(orderId)
- IDX(customerId)
- IDX(status)

---

# Eventos Consumidos

- ORDER_CREATED

---

# Eventos Produzidos

- PAYMENT_APPROVED
- PAYMENT_REJECTED

---

# Observações

O Payment Service segue o padrão Database Per Service.

Os dados do pedido são recebidos através de eventos Kafka.

Nenhum acesso direto ao banco do Order Service será realizado.

---

# Evoluções Futuras (V3)

- Integração com Mercado Pago
- Integração com Stripe
- Integração com Asaas
- Integração com PagSeguro

Também será adicionada uma entidade para armazenar informações específicas dos provedores de pagamento, como identificadores externos, códigos de autorização, respostas da API e histórico de tentativas.

---

# Decisões Arquiteturais Relacionadas

- Database Per Service
- Event-Driven Architecture
- Asynchronous Communication
- Event-Carried State Transfer