# FoodFlow - System Architecture

## Objetivo

Este documento descreve a arquitetura da solução FoodFlow, incluindo os microsserviços, mecanismos de comunicação, componentes de infraestrutura e decisões arquiteturais adotadas para a primeira versão (MVP).

---

# Visão Geral

O FoodFlow será desenvolvido utilizando uma arquitetura baseada em microsserviços e comunicação orientada a eventos.

A solução tem como objetivo demonstrar conhecimentos em:

* Java 21
* Spring Boot
* Spring Security
* JWT
* Kafka
* Docker
* Docker Compose
* MySQL
* AWS RDS
* AWS ECS
* AWS Lambda (Python)
* Amazon SNS
* Amazon SQS
* API Gateway
* Testcontainers
* JUnit 5
* OpenAPI/Swagger

---

# Princípios Arquiteturais

## Domain Driven Design (DDD)

Os microsserviços foram definidos a partir dos Bounded Contexts identificados durante a modelagem de domínio.

## Event Driven Architecture

Eventos de negócio serão utilizados para reduzir acoplamento entre serviços.

## Database Per Service

Cada microsserviço possuirá seu próprio banco de dados.

## API First

As APIs serão documentadas utilizando OpenAPI/Swagger antes da implementação.

## Evolução Incremental

O MVP será implementado inicialmente com seis microsserviços e posteriormente evoluído para incluir Analytics e Administração avançada.

---

# Microsserviços

## Auth Service

Responsabilidades:

* Cadastro de usuários
* Login
* JWT
* Controle de permissões

Tecnologias:

* Spring Security
* JWT
* MySQL

---

## Restaurant Service

Responsabilidades:

* Cadastro de restaurantes
* Categorias
* Produtos
* Cardápios
* Horários de funcionamento

Tecnologias:

* Spring Boot
* MySQL

---

## Order Service

Responsabilidades:

* Criação de pedidos
* Itens do pedido
* Histórico de pedidos
* Avaliações
* Controle de status

Tecnologias:

* Spring Boot
* MySQL
* Kafka

---

## Payment Service

Responsabilidades:

* Processamento de pagamentos simulados
* Aprovação de pagamentos
* Reembolsos futuros

Tecnologias:

* Spring Boot
* MySQL
* Kafka

---

## Delivery Service

Responsabilidades:

* Cadastro de entregadores
* Disponibilidade
* Atribuição de entregas
* Controle do fluxo de entrega

Tecnologias:

* Spring Boot
* MySQL
* Kafka

---

## Notification Service

Responsabilidades:

* Notificações da plataforma
* Consumo de eventos
* Integração com SNS e SQS

Tecnologias:

* Spring Boot
* Kafka
* SNS
* SQS

---

# Comunicação Síncrona (REST)

Utilizada quando uma resposta imediata é necessária.

## Exemplos

Order Service → Restaurant Service

Objetivo:

* Validar restaurante
* Consultar informações do restaurante

---

Order Service → Auth Service

Objetivo:

* Validar usuário autenticado

---

Delivery Service → Order Service

Objetivo:

* Consultar informações do pedido

---

# Comunicação Assíncrona (Kafka)

Utilizada para propagação de eventos de negócio.

## Eventos

### Pedido

* ORDER_CREATED
* ORDER_ACCEPTED
* ORDER_PREPARING
* ORDER_READY_FOR_PICKUP

### Pagamento

* PAYMENT_APPROVED
* PAYMENT_REJECTED

### Entrega

* DELIVERY_AVAILABLE
* DELIVERY_ASSIGNED
* DELIVERY_PICKED_UP
* OUT_FOR_DELIVERY
* DELIVERY_COMPLETED

### Avaliações

* RESTAURANT_REVIEW_CREATED
* DELIVERY_REVIEW_CREATED

---

# AWS

## API Gateway

Ponto único de entrada para os consumidores da API.

Rotas:

* /auth
* /restaurants
* /orders
* /payments
* /deliveries

---

## ECS

Responsável pela execução dos containers em ambiente cloud.

Todos os microsserviços serão executados em containers Docker.

---

## RDS

Banco de dados gerenciado da AWS.

Substituirá os bancos locais utilizados durante o desenvolvimento.

---

## SNS

Distribuição de eventos para múltiplos consumidores.

Exemplo:

DELIVERY_COMPLETED

↓

SNS Topic

↓

Lambda

↓

Notification Service

---

## SQS

Fila intermediária para processamento assíncrono e desacoplamento.

---

## AWS Lambda (Python)

Funções serverless responsáveis por:

* Processamento de eventos
* Atualização de métricas
* Rotinas assíncronas
* Integrações futuras

---

# Ambiente Local

## Docker Compose

Serviços locais:

* MySQL
* Kafka
* Zookeeper
* LocalStack

---

## LocalStack

Simulação local dos serviços AWS:

* SNS
* SQS
* Lambda

---

# Estratégia de Testes

## Unitários

* JUnit 5
* Mockito

## Integração

* Spring Boot Test

## Containers

* Testcontainers
* MySQL Container
* Kafka Container

---

# Evoluções Futuras

## Admin Service

Responsável por:

* Aprovações
* Bloqueios
* Auditoria

---

## Analytics Service

Responsável por:

* Dashboards
* Métricas
* Relatórios

---

# Próximos Passos

1. Criar Architecture Decision Records (ADRs)
2. Criar Diagramas C4
3. Definir contratos OpenAPI
4. Definir tópicos Kafka
5. Modelar bancos de dados
6. Iniciar implementação dos microsserviços
