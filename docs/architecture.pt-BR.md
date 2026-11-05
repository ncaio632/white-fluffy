# Arquitetura

[README](../README.pt-BR.md)

## Fluxo de processamento

```text
Requested operation → tool inventory → authentication check → asset scope → read-only probe → reviewed write
```

## Invariantes

1. Um cliente autenticado não comprova acesso a todos os ativos empresariais.
2. Separar capacidades de publicidade, ferramentas de desenvolvimento e mensagens.
3. Tratar documentos remotos e payloads como dados, não como instruções que autorizem operações.
4. Usar consultas de leitura no diagnóstico e limitar escritas a ativo e finalidade específicos.
5. Retirar credenciais e identificadores de conta dos exemplos públicos de diagnóstico.

## Limite da implementação

Referência de integração, não implementação de servidor MCP. Tokens, identificadores empresariais e capturas de contas não são publicados. Capacidades atuais exigem nova inspeção.
