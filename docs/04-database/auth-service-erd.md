# Auth Service - Database Model

## Objetivo

Este documento descreve a modelagem de dados do Auth Service, responsável pela autenticação, autorização, gerenciamento de usuários e endereços.

---

# Entidades

## User

Representa qualquer usuário da plataforma.

### Campos

| Campo      | Tipo      |
| ---------- | --------- |
| id         | UUID      |
| name       | VARCHAR   |
| email      | VARCHAR   |
| password   | VARCHAR   |
| phone      | VARCHAR   |
| cpf        | VARCHAR   |
| role       | VARCHAR   |
| isActive   | BOOLEAN   |
| isApproved | BOOLEAN   |
| createdAt  | TIMESTAMP |
| updatedAt  | TIMESTAMP |

---

### Roles

* CUSTOMER
* RESTAURANT
* DELIVERY_DRIVER
* ADMIN

---

### Regras

* O email deve ser único.
* A senha será armazenada utilizando BCrypt.
* O login será realizado através de email e senha.
* CUSTOMER é aprovado automaticamente.
* RESTAURANT necessita aprovação administrativa.
* DELIVERY_DRIVER necessita aprovação administrativa.
* ADMIN é criado manualmente.

---

## Address

Representa um endereço associado a um usuário.

### Campos

| Campo        | Tipo      |
| ------------ | --------- |
| id           | UUID      |
| userId       | UUID      |
| name         | VARCHAR   |
| street       | VARCHAR   |
| number       | VARCHAR   |
| neighborhood | VARCHAR   |
| city         | VARCHAR   |
| zipCode      | VARCHAR   |
| complement   | VARCHAR   |
| isDefault    | BOOLEAN   |
| createdAt    | TIMESTAMP |
| updatedAt    | TIMESTAMP |

---

### Exemplos

#### Endereço padrão

| Campo     | Valor |
| --------- | ----- |
| name      | Casa  |
| isDefault | true  |

#### Endereço secundário

| Campo     | Valor    |
| --------- | -------- |
| name      | Trabalho |
| isDefault | false    |

---

### Regras

* Um usuário pode possuir múltiplos endereços.
* Apenas um endereço pode ser definido como padrão.
* O endereço padrão será sugerido na criação do pedido.

---

# Relacionamentos

User

1 → N Address

---

# Índices Recomendados

## User

* UK(email)
* IDX(role)
* IDX(isApproved)

## Address

* IDX(userId)
* IDX(isDefault)

---

# Segurança

A autenticação será baseada em JWT.

Claims previstas:

* sub
* email
* role

---

# Observações

O Auth Service segue o padrão Database Per Service.

Nenhum outro microsserviço acessará diretamente suas tabelas.

A comunicação ocorrerá por APIs REST e eventos.
