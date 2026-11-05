# ADR 001 — Limites e diagnóstico de integrações MCP

[README](../README.pt-BR.md)

## Contexto

Estrutura de referência técnica que separa capacidade do conector, autenticação, escopo dos ativos e operações empresariais.

## Decisão

Modelar estado da conexão e autorização do ativo como verificações separadas.

## Consequências

O diagnóstico precisa relatar mais estados, mas permite atribuir falhas a capacidade, credenciais ou escopo.

## Limite da evidência

Referência de integração, não implementação de servidor MCP. Tokens, identificadores empresariais e capturas de contas não são publicados. Capacidades atuais exigem nova inspeção.
