# ADR-0006 - Driver Status Model

## Status

Accepted

## Context

Inicialmente o entregador possuía apenas o campo `isOnline`.

Entretanto, esse modelo não representava corretamente todos os estados possíveis de um entregador durante sua jornada operacional.

## Decision

Substituir `isOnline` pelo enum `currentStatus`.

Valores:

- OFFLINE
- ONLINE
- BUSY
- SUSPENDED

## Consequences

### Positivas

- Modelo mais expressivo.
- Elimina ambiguidades.
- Facilita evolução futura.
- Permite novas regras de negócio sem alteração estrutural.

### Negativas

- Necessidade de validar transições entre estados.