# ADR-001 - Simulação de Pagamentos

## Status

Accepted

## Contexto

O FoodFlow necessita de um fluxo de pagamento para permitir a continuidade do ciclo de vida dos pedidos.

Integrações reais com gateways como Stripe, Mercado Pago ou PagSeguro adicionariam complexidade significativa ao projeto.

## Alternativas Consideradas

### Opção 1

Integração com gateway real.

### Opção 2

Pagamento simulado.

## Decisão

Utilizar pagamento simulado na primeira versão do sistema.

## Consequências

### Positivas

- Menor complexidade
- Desenvolvimento mais rápido
- Foco em microsserviços
- Foco em Kafka
- Foco em AWS

### Negativas

- Não representa uma integração financeira real
- Necessidade de evolução futura