# FoodFlow - MVP Scope

## Objetivo

Definir o escopo da primeira versão (MVP) do FoodFlow, estabelecendo as funcionalidades que serão implementadas inicialmente e aquelas que ficarão para versões futuras.

---

# Visão do Produto

O FoodFlow é uma plataforma de delivery que conecta clientes, restaurantes e entregadores através de uma arquitetura baseada em microsserviços e eventos.

O sistema permitirá que clientes realizem pedidos online, acompanhem entregas em tempo real e avaliem a experiência após a conclusão do pedido.

---

# Funcionalidades do MVP

## Autenticação e Usuários

* Cadastro de clientes
* Cadastro de restaurantes
* Cadastro de entregadores
* Login com JWT
* Controle de permissões por perfil
* Aprovação de restaurantes
* Aprovação de entregadores

---

## Endereços

* Cadastro de múltiplos endereços
* Definição de endereço padrão
* Seleção do endereço durante o pedido

---

## Restaurantes

* Cadastro de restaurante
* Cadastro de categorias
* Cadastro de produtos
* Cadastro de horários de funcionamento
* Ativação e desativação de produtos
* Busca de restaurantes
* Busca por nome
* Busca por restaurantes abertos
* Busca por entrega grátis
* Busca por melhor avaliação
* Favoritar restaurantes

---

## Pedidos

* Criação de pedidos
* Cancelamento de pedidos
* Histórico de pedidos
* Acompanhamento de status
* Snapshot de produtos
* Snapshot de endereço de entrega

---

## Pagamentos

* Pagamento via PIX
* Pagamento via cartão de crédito
* Pagamento via cartão de débito
* Histórico de pagamentos
* Aprovação e rejeição de pagamentos

---

## Entregas

* Entregador online/offline
* Aceitação manual da entrega
* Rastreamento do status da entrega
* Confirmação de entrega por código
* Controle de ganhos do entregador

---

## Avaliações

* Avaliação do restaurante
* Avaliação do entregador
* Comentários opcionais
* Atualização das métricas por eventos Kafka

---

## Notificações

* Notificação de pedido criado
* Notificação de pagamento aprovado
* Notificação de pagamento recusado
* Notificação de pedido aceito
* Notificação de entrega iniciada
* Notificação de entrega concluída

---

# Funcionalidades da V2

* Cupons de desconto
* Promoções
* Chat entre cliente e entregador
* Geolocalização em tempo real
* QR Code para confirmação de entrega
* Programa de fidelidade

---
# Funcionalidades da V3

* Integração com gateways de pagamento reais (Stripe, Mercado Pago, PagSeguro, Asaas)
* Aplicativo mobile nativo para clientes
* Aplicativo mobile nativo para entregadores
* Sistema de recomendação de restaurantes utilizando Inteligência Artificial
* Dashboard avançado de métricas e BI
* Sistema de campanhas promocionais inteligentes
* Recomendação personalizada baseada em histórico de pedidos
* Rastreamento da entrega em tempo real via GPS
* Notificações push mobile

# Fora do Escopo

* Marketplace internacional
* Suporte multi-moeda
* Multi-idioma
* White-label para franquias

---

# Objetivos de Aprendizado

Este projeto será utilizado para aprofundar conhecimentos em:

* Java 21
* Spring Boot
* Spring Security
* JWT
* Kafka
* Microsserviços
* Docker
* Docker Compose
* MySQL
* AWS RDS
* AWS ECS
* AWS Lambda
* AWS SNS
* AWS SQS
* API Gateway
* Testcontainers
* JUnit 5
* OpenAPI/Swagger

Além da compreensão de decisões arquiteturais utilizadas em sistemas distribuídos reais.
