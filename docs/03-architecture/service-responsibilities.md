# Service Responsibilities

## Objetivo

Este documento descreve as responsabilidades de cada microsserviço do FoodFlow.

Cada serviço possui um contexto de negócio bem definido e é responsável exclusivamente pelos dados e regras pertencentes ao seu domínio.

---

# Auth Service

## Responsabilidades

* Gerenciar usuários.
* Gerenciar autenticação.
* Emitir tokens JWT.
* Gerenciar papéis (Roles).
* Gerenciar endereços dos usuários.
* Aprovar restaurantes.
* Aprovar entregadores.

## Não é responsabilidade

* Gerenciar pedidos.
* Gerenciar pagamentos.
* Gerenciar entregas.
* Gerenciar cardápios.
* Gerenciar notificações.

---

# Restaurant Service

## Responsabilidades

* Gerenciar restaurantes.
* Gerenciar cardápios.
* Gerenciar categorias.
* Gerenciar produtos.
* Gerenciar horários de funcionamento.
* Gerenciar pedido mínimo.
* Gerenciar restaurantes favoritos.

## Não é responsabilidade

* Processar pagamentos.
* Gerenciar usuários.
* Gerenciar autenticação.
* Gerenciar entregas.
* Gerenciar notificações.

---

# Order Service

## Responsabilidades

* Criar pedidos.
* Gerenciar itens do pedido.
* Controlar o ciclo de vida do pedido.
* Armazenar snapshots dos produtos.
* Registrar avaliações.
* Manter o histórico de status do pedido.

## Não é responsabilidade

* Processar pagamentos.
* Gerenciar entregadores.
* Gerenciar cardápios.
* Gerenciar autenticação.

---

# Payment Service

## Responsabilidades

* Processar pagamentos.
* Registrar transações.
* Publicar eventos financeiros.
* Controlar o status do pagamento.

## Não é responsabilidade

* Criar pedidos.
* Gerenciar restaurantes.
* Gerenciar entregas.
* Gerenciar usuários.

---

# Delivery Service

## Responsabilidades

* Gerenciar entregadores.
* Gerenciar entregas.
* Atribuir entregadores aos pedidos.
* Controlar o status da entrega.
* Validar o código de confirmação da entrega.

## Não é responsabilidade

* Processar pagamentos.
* Criar pedidos.
* Gerenciar produtos.
* Gerenciar autenticação.

---

# Notification Service

## Responsabilidades

* Consumir eventos dos demais microsserviços.
* Gerar notificações.
* Persistir notificações.
* Disponibilizar o histórico de notificações.

## Não é responsabilidade

* Alterar pedidos.
* Alterar pagamentos.
* Alterar entregas.
* Alterar restaurantes.
* Alterar usuários.

---

# Comunicação entre Serviços

| Serviço              | REST | Kafka |
| -------------------- | ---- | ----- |
| Auth Service         | Sim  | Sim   |
| Restaurant Service   | Sim  | Sim   |
| Order Service        | Não  | Sim   |
| Payment Service      | Não  | Sim   |
| Delivery Service     | Não  | Sim   |
| Notification Service | Não  | Sim   |

---

# Princípios

Todos os microsserviços seguem os seguintes princípios:

* Single Responsibility Principle (SRP)
* Database per Service
* Domain-Driven Design (DDD)
* Event-Driven Architecture
* Eventual Consistency

---

# Decisões Arquiteturais

* Cada microsserviço possui seu próprio banco de dados.
* Nenhum microsserviço acessa diretamente o banco de outro.
* A comunicação entre serviços ocorre por APIs REST ou eventos Kafka.
* Cada serviço é responsável pela consistência dos seus próprios dados.

---

# Evoluções Futuras

A arquitetura foi projetada para permitir a inclusão de novos microsserviços sem impactar os serviços existentes.

Exemplos:

* Recommendation Service
* Coupon Service
* Promotion Service
* Analytics Service
* Search Service
