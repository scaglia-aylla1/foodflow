# Project Glossary

## Objetivo

Este documento define os termos do domínio do FoodFlow para garantir uma linguagem ubíqua consistente entre todos os microsserviços, desenvolvedores e documentos da arquitetura.

---

# Termos do Domínio

## User

Entidade base do sistema que representa qualquer pessoa cadastrada no FoodFlow.

Pode atuar como cliente, restaurante, entregador ou administrador.

---

## Customer

Usuário que realiza pedidos na plataforma.

---

## Restaurant

Estabelecimento comercial que disponibiliza produtos para venda através da plataforma.

---

## Driver

Entregador responsável por realizar a entrega dos pedidos ao cliente final.

---

## Order

Representa uma solicitação de compra realizada por um cliente em um restaurante.

---

## Order Item

Item individual dentro de um pedido, representando um produto e sua quantidade.

---

## Payment

Processo de validação e registro financeiro associado a um pedido.

---

## Delivery

Processo logístico responsável pela entrega do pedido ao cliente.

---

## Notification

Mensagem gerada pelo sistema para informar usuários sobre eventos relevantes.

---

## Product

Item vendido por um restaurante dentro do sistema.

---

## Category

Agrupamento lógico de produtos dentro de um restaurante.

---

## Address

Local físico associado a um usuário, utilizado para entregas.

---

## Event

Mensagem assíncrona utilizada para comunicação entre microsserviços.

---

## Snapshot

Cópia imutável dos dados de um produto armazenada no momento da criação do pedido.

---

## Status

Estado atual de uma entidade (ex: OrderStatus, DeliveryStatus).

---

## Bounded Context

Área isolada do domínio que possui regras de negócio, dados e responsabilidades próprias.

---

## Eventual Consistency

Modelo de consistência onde os dados entre microsserviços não são atualizados instantaneamente, mas convergem ao longo do tempo via eventos.

---

## Kafka Event

Mensagem publicada em um tópico Kafka para comunicação entre microsserviços.

---

## JWT

Token utilizado para autenticação stateless entre cliente e sistema.

---

## Soft Delete

Estratégia de exclusão lógica onde o registro permanece no banco de dados, mas é marcado como inativo.

---

## Correlation ID

Identificador único utilizado para rastrear uma requisição através de múltiplos microsserviços.

---

# Regras de Linguagem

## GL-001

Todos os documentos, código e comunicação interna devem utilizar os termos definidos neste glossário.

---

## GL-002

Não devem ser utilizados sinônimos não padronizados para termos do domínio.

---

## GL-003

Qualquer novo termo de domínio deve ser adicionado a este glossário antes de ser utilizado na arquitetura.

---

# Benefícios

* Redução de ambiguidades
* Padronização da linguagem entre equipes
* Facilita onboarding de novos desenvolvedores
* Melhora a comunicação entre microsserviços
* Evita inconsistências no domínio

---

# Decisões Arquiteturais Relacionadas

* Domain-Driven Design (DDD)
* Ubiquitous Language
* Microservices Architecture
* Event-Driven Architecture
