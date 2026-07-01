# Quality Attributes

## Objetivo

Este documento descreve os atributos de qualidade do FoodFlow, definindo requisitos não funcionais que guiam decisões arquiteturais relacionadas a desempenho, escalabilidade, disponibilidade, segurança e observabilidade.

---

# Escalabilidade

## QA-001

O sistema deve ser capaz de escalar horizontalmente todos os microsserviços independentemente.

---

## QA-002

Cada microsserviço deve ser stateless para permitir escalabilidade horizontal eficiente.

---

## QA-003

O sistema deve suportar aumento de carga em picos (ex: horário de almoço e jantar) sem degradação crítica de performance.

---

## QA-004

O Kafka será utilizado como backbone de comunicação assíncrona para reduzir acoplamento e aumentar escalabilidade.

---

# Performance

## QA-005

As requisições síncronas devem ter tempo médio de resposta inferior a 300ms para operações comuns.

---

## QA-006

Consultas de leitura devem ser otimizadas com paginação obrigatória.

---

## QA-007

Operações de escrita críticas devem ser processadas de forma assíncrona sempre que possível.

---

## QA-008

O sistema deve priorizar consistência eventual em operações distribuídas para ganho de performance.

---

# Disponibilidade

## QA-009

Os microsserviços devem ser projetados para alta disponibilidade.

---

## QA-010

Falhas em um microsserviço não devem comprometer o funcionamento dos demais.

---

## QA-011

O sistema deve tolerar falhas temporárias em serviços downstream utilizando retry e fallback.

---

## QA-012

O Kafka deve atuar como buffer de resiliência em caso de indisponibilidade temporária de serviços consumidores.

---

# Consistência

## QA-013

O sistema adota o modelo de consistência eventual entre microsserviços.

---

## QA-014

Não são permitidas transações distribuídas (no distributed transactions / no 2PC).

---

## QA-015

A sincronização de estados entre serviços ocorre exclusivamente via eventos.

---

# Segurança

## QA-016

Todas as comunicações externas devem ser protegidas por autenticação JWT.

---

## QA-017

Credenciais e segredos devem ser armazenados fora do código-fonte.

---

## QA-018

Cada microsserviço deve validar permissões de acesso independentemente.

---

## QA-019

A comunicação entre microsserviços deve ocorrer em rede interna segura.

---

# Observabilidade

## QA-020

Todos os microsserviços devem gerar logs estruturados.

---

## QA-021

Cada requisição deve possuir um correlationId para rastreabilidade.

---

## QA-022

O sistema deve permitir rastreamento de eventos distribuídos entre serviços.

---

## QA-023

Métricas de performance e erro devem ser expostas para monitoramento.

---

# Resiliência

## QA-024

O sistema deve implementar retry automático para falhas transitórias.

---

## QA-025

Circuit breaker deve ser utilizado em chamadas síncronas entre serviços.

---

## QA-026

Mensagens não processadas no Kafka devem ser redirecionadas para dead letter queues.

---

# Evolução

## QA-027

A arquitetura deve permitir a adição de novos microsserviços sem impacto nos existentes.

---

## QA-028

Novos consumidores de eventos devem poder ser adicionados sem alteração dos produtores.

---

## QA-029

O sistema deve suportar evolução de contratos de eventos com versionamento.

---

# Decisões Arquiteturais Relacionadas

* Microservices Architecture
* Event-Driven Architecture
* Kafka as Message Broker
* Stateless Services
* Distributed Systems Design
* Eventually Consistent Systems
* Observability by Design
