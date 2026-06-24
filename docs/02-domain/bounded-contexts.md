# FoodFlow - Bounded Contexts

## Objetivo

Este documento descreve os Bounded Contexts identificados durante a modelagem de domínio do FoodFlow.

A definição destes contextos servirá como base para a arquitetura de microsserviços do sistema.

---

# 1. Auth Context

Responsável pela autenticação e autorização dos usuários da plataforma.

## Responsabilidades

- Cadastro de usuários
- Login
- Geração de JWT
- Refresh Token
- Controle de permissões
- Controle de papéis (Roles)

## Principais Conceitos

- User
- Role
- Permission
- Authentication

## Futuro Microsserviço

auth-service

---

# 2. Restaurant Context

Responsável pelo gerenciamento dos restaurantes e seus cardápios.

## Responsabilidades

- Cadastro de restaurantes
- Gestão de cardápios
- Gestão de categorias
- Gestão de produtos
- Horário de funcionamento

## Principais Conceitos

- Restaurant
- Category
- Product
- Menu
- OpeningHours

## Futuro Microsserviço

restaurant-service

---

# 3. Order Context

Responsável pelo ciclo de vida dos pedidos.

## Responsabilidades

- Criação de pedidos
- Cancelamento de pedidos
- Consulta de pedidos
- Controle de status
- Avaliações

## Principais Conceitos

- Order
- OrderItem
- Review

## Futuro Microsserviço

order-service

---

# 4. Payment Context

Responsável pelo processamento dos pagamentos.

## Responsabilidades

- Processamento de pagamentos
- Aprovação de pagamentos
- Rejeição de pagamentos
- Reembolsos

## Principais Conceitos

- Payment
- Transaction
- Refund

## Futuro Microsserviço

payment-service

---

# 5. Delivery Context

Responsável pelas entregas e entregadores.

## Responsabilidades

- Cadastro de entregadores
- Disponibilidade de entregadores
- Atribuição de entregas
- Atualização de status
- Finalização de entregas

## Principais Conceitos

- Delivery
- Driver
- DeliveryAssignment

## Futuro Microsserviço

delivery-service

---

# 6. Administration Context

Responsável pela gestão operacional da plataforma.

## Responsabilidades

- Aprovação de restaurantes
- Aprovação de entregadores
- Bloqueio de usuários
- Monitoramento da plataforma
- Métricas administrativas

## Principais Conceitos

- Approval
- Moderation
- Audit
- Dashboard

## Futuro Microsserviço

admin-service

---

# Ubiquitous Language

## Pedido

Solicitação realizada por um cliente para aquisição de produtos de um restaurante.

## Entrega

Processo de transporte de um pedido até o cliente.

## Restaurante

Estabelecimento parceiro da plataforma.

## Entregador

Usuário responsável pela entrega dos pedidos.

## Avaliação

Feedback realizado por um cliente após a conclusão de um pedido.

## Pagamento

Transação financeira associada a um pedido.

---

# Próximas Etapas

1. Definir arquitetura dos microsserviços
2. Definir comunicação síncrona e assíncrona
3. Definir eventos Kafka
4. Criar diagramas C4
5. Modelar banco de dados