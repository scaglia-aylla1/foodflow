# FoodFlow - Vision Document

## 1. Visão do Produto

O FoodFlow é uma plataforma de delivery baseada em microsserviços e arquitetura orientada a eventos.

O sistema conecta clientes, restaurantes e entregadores, permitindo o gerenciamento completo do ciclo de vida de um pedido, desde sua criação até a entrega final.

O projeto tem como objetivo servir como estudo prático de arquiteturas modernas utilizando Java, Spring Boot, Kafka, AWS e Microsserviços, simulando cenários encontrados em empresas de grande porte.

---

# 2. Objetivos do Produto

* Permitir que clientes realizem pedidos online.
* Permitir que restaurantes gerenciem cardápios e pedidos.
* Permitir que entregadores realizem entregas.
* Disponibilizar métricas para os participantes da plataforma.
* Utilizar arquitetura orientada a eventos para garantir desacoplamento e escalabilidade.

---

# 3. Atores do Sistema

## Cliente

Responsável por realizar pedidos e acompanhar entregas.

### Funcionalidades

* Criar conta
* Realizar login
* Buscar restaurantes
* Favoritar restaurantes
* Criar pedidos
* Cancelar pedidos
* Avaliar restaurantes
* Avaliar entregadores
* Acompanhar entregas

---

## Restaurante

Responsável pelo gerenciamento do cardápio e processamento dos pedidos.

### Funcionalidades

* Solicitar cadastro
* Enviar documentação
* Gerenciar categorias
* Gerenciar produtos
* Alterar preços
* Desativar produtos
* Aceitar pedidos
* Rejeitar pedidos
* Definir tempo estimado de preparo
* Atualizar status dos pedidos
* Visualizar métricas
* Configurar horário de funcionamento

### Status

* PENDING_APPROVAL
* APPROVED
* REJECTED
* BLOCKED

---

## Entregador

Responsável pela entrega dos pedidos.

### Funcionalidades

* Solicitar cadastro
* Enviar documentação
* Visualizar entregas disponíveis
* Aceitar entregas
* Atualizar status da entrega
* Finalizar entrega
* Visualizar métricas

### Status de Cadastro

* PENDING_APPROVAL
* APPROVED
* REJECTED
* BLOCKED

### Status Operacional

* OFFLINE
* ONLINE
* BUSY

---

## Administrador

Responsável pela gestão da plataforma.

### Funcionalidades

* Aprovar restaurantes
* Aprovar entregadores
* Rejeitar cadastros
* Bloquear contas
* Monitorar pedidos
* Monitorar restaurantes
* Monitorar entregadores
* Visualizar métricas gerais

---

# 4. Regras de Negócio Identificadas

## RN-001

Um restaurante não pode receber pedidos enquanto estiver com status diferente de APPROVED.

## RN-002

Um entregador não pode aceitar entregas enquanto estiver com status diferente de APPROVED.

## RN-003

O sistema deve impedir novos pedidos fora do horário de funcionamento do restaurante.

## RN-004

Clientes podem avaliar restaurantes e entregadores após a conclusão do pedido.

## RN-005

Um entregador pode aceitar apenas uma entrega por vez quando estiver com status BUSY.

---

# 5. Visão Inicial da Arquitetura

O sistema será desenvolvido utilizando:

* Java 21
* Spring Boot
* Spring Security
* JWT
* Kafka
* MySQL
* Docker
* Docker Compose
* LocalStack
* AWS (simulada localmente)
* OpenFeign
* MapStruct
* Resilience4j
* Prometheus
* Grafana
* Testcontainers
* GitHub Actions

A arquitetura seguirá os princípios de:

* Microsserviços
* Event Driven Architecture
* Clean Architecture
* SOLID
* DDD Simplificado

---

# 6. Próximas Etapas

1. Modelagem de Domínio
2. Identificação de Entidades
3. Definição dos Bounded Contexts
4. Arquitetura dos Microsserviços
5. Modelagem do Banco de Dados
6. Definição dos Eventos Kafka
7. Definição das APIs
8. Implementação
