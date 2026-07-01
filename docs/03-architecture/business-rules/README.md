# Business Rules

## Objetivo

Este diretório reúne todas as regras de negócio do FoodFlow.

As regras estão organizadas por domínio para facilitar a manutenção, rastreabilidade e evolução do sistema.

Cada regra possui um identificador único, permitindo sua referência em documentação, código, testes e discussões técnicas.

## Organização

| Documento             | Prefixo  |
| --------------------- | -------- |
| auth-rules.md         | AUTH     |
| restaurant-rules.md   | REST     |
| order-rules.md        | ORDER    |
| payment-rules.md      | PAY      |
| delivery-rules.md     | DELIVERY |
| review-rules.md       | REVIEW   |
| notification-rules.md | NOTIFY   |
| security-rules.md     | SEC      |

## Convenção

Cada regra utiliza o seguinte formato:

* AUTH-001
* REST-001
* ORDER-001
* PAY-001
* DELIVERY-001
* REVIEW-001
* NOTIFY-001
* SEC-001

## Objetivo das Regras

As regras de negócio representam o comportamento esperado da aplicação.

Durante a implementação, toda funcionalidade deverá respeitar estas regras.

Em caso de conflito entre implementação e documentação, a regra de negócio deverá ser revisada antes da alteração do código.
