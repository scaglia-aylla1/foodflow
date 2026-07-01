# Restaurant Business Rules

## Objetivo

Este documento descreve as regras de negócio relacionadas ao gerenciamento dos restaurantes, cardápio, produtos e funcionamento do FoodFlow.

---

# Aprovação

### REST-001

Todo restaurante deverá ser aprovado por um administrador antes de iniciar suas operações.

---

### REST-002

Enquanto não aprovado, o restaurante poderá acessar sua conta, porém não poderá receber pedidos.

---

### REST-003

A aprovação gera o evento:

* RESTAURANT_APPROVED

---

# Funcionamento

### REST-004

Todo restaurante deverá possuir horário de funcionamento cadastrado.

---

### REST-005

O restaurante somente poderá receber pedidos quando estiver dentro do horário de funcionamento.

---

### REST-006

O restaurante poderá alterar seu horário de funcionamento a qualquer momento.

---

### REST-007

Caso esteja fechado, novos pedidos não poderão ser realizados.

---

# Pedido Mínimo

### REST-008

Todo restaurante deverá definir um valor mínimo para pedidos.

---

### REST-009

Pedidos com valor inferior ao mínimo não poderão ser finalizados.

---

# Cardápio

### REST-010

Todo restaurante poderá cadastrar categorias para organizar seu cardápio.

Exemplos:

* Lanches
* Pizzas
* Bebidas
* Sobremesas

---

### REST-011

Cada produto deverá pertencer a uma categoria.

---

### REST-012

Produtos poderão ser ativados ou desativados.

---

### REST-013

Produtos desativados não serão exibidos aos clientes.

---

### REST-014

Alterações no cadastro de produtos não afetam pedidos já realizados.

Os pedidos armazenam um snapshot dos produtos.

---

# Produtos

### REST-015

Todo produto deverá possuir:

* nome
* descrição
* preço
* categoria

---

### REST-016

O preço do produto deverá ser maior que zero.

---

### REST-017

O restaurante poderá alterar o preço dos produtos a qualquer momento.

As alterações valerão apenas para novos pedidos.

---

### REST-018

Produtos excluídos logicamente (Soft Delete) não poderão ser vendidos, mas permanecerão registrados para fins de histórico.

---

# Favoritos

### REST-019

Clientes poderão favoritar restaurantes.

---

### REST-020

Um restaurante poderá ser favoritado apenas uma vez pelo mesmo cliente.

---

### REST-021

Clientes poderão remover restaurantes da lista de favoritos.

---

# Disponibilidade

### REST-022

O restaurante poderá suspender temporariamente o recebimento de pedidos.

---

### REST-023

Enquanto suspenso, o restaurante continuará visível aos clientes, porém não aceitará novos pedidos.

---

# Avaliações

### REST-024

A nota média do restaurante será calculada a partir das avaliações recebidas.

---

### REST-025

Somente pedidos concluídos poderão gerar avaliações.

---

REST-026

Todo restaurante possui um status operacional.

---

REST-027

Apenas restaurantes com status ACTIVE podem receber pedidos.

---

# Observações

O Restaurant Service é responsável exclusivamente pelos dados relacionados aos restaurantes e seus cardápios.

Informações sobre pedidos, pagamentos, entregas e usuários pertencem aos respectivos microsserviços.

---

# Decisões Arquiteturais Relacionadas

* Database per Service
* Soft Delete
* Snapshot Pattern
* Domain-Driven Design (DDD)
* Event-Driven Architecture
