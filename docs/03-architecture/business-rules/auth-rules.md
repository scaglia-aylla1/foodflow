# Authentication Business Rules

## Objetivo

Este documento descreve as regras de negócio relacionadas ao cadastro, autenticação, autorização e gerenciamento de usuários do FoodFlow.

---

# Cadastro

### AUTH-001

Todo usuário deve possuir uma conta cadastrada para acessar o sistema.

---

### AUTH-002

O login será realizado utilizando e-mail e senha.

---

### AUTH-003

O e-mail deve ser único no sistema.

Não é permitido que dois usuários utilizem o mesmo endereço de e-mail.

---

### AUTH-004

O CPF deve ser único no sistema.

Não é permitido que dois usuários compartilhem o mesmo CPF, independentemente do tipo de usuário.

---

### AUTH-005

Todo usuário deve possuir pelo menos um endereço cadastrado.

---

### AUTH-006

O endereço principal será utilizado como padrão para novas entregas.

---

### AUTH-007

O cliente poderá cadastrar múltiplos endereços.

---

### AUTH-008

O cliente poderá definir apenas um endereço como principal.

---

# Autenticação

### AUTH-009

Após o login com sucesso, o sistema deverá emitir um JWT para autenticação das requisições.

---

### AUTH-010

O JWT deverá ser enviado em todas as requisições para endpoints protegidos.

---

### AUTH-011

Usuários não autenticados não poderão acessar recursos protegidos.

---

# Autorização

### AUTH-012

Cada usuário possuirá um papel (Role) que determinará suas permissões.

---

### AUTH-013

Um cliente poderá acessar apenas funcionalidades destinadas aos clientes.

---

### AUTH-014

Um restaurante poderá acessar apenas funcionalidades destinadas aos restaurantes.

---

### AUTH-015

Um entregador poderá acessar apenas funcionalidades destinadas aos entregadores.

---

### AUTH-016

Administradores poderão acessar todas as funcionalidades administrativas.

---

# Aprovação

### AUTH-017

Restaurantes deverão ser aprovados por um administrador antes de iniciar suas operações.

---

### AUTH-018

Entregadores deverão ser aprovados por um administrador antes de aceitar entregas.

---

### AUTH-019

Enquanto não aprovados, restaurantes e entregadores poderão acessar o sistema, mas não poderão operar.

---

# Segurança

### AUTH-020

As senhas nunca serão armazenadas em texto puro.

---

### AUTH-021

As senhas deverão ser armazenadas utilizando algoritmo de hash seguro (BCrypt).

---

### AUTH-022

Após o logout, o cliente deverá remover o JWT armazenado localmente.

---

# Observações

O Auth Service é responsável apenas pela identidade dos usuários.

Informações como pedidos, restaurantes, entregas e pagamentos pertencem aos seus respectivos microsserviços.

---

# Decisões Arquiteturais Relacionadas

* JWT Authentication
* Role Based Access Control (RBAC)
* BCrypt Password Hashing
* Database per Service
* Stateless Authentication
