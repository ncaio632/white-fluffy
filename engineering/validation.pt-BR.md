# Rastreabilidade e validação

**Resumo acionável; matriz completa em [inglês](validation.en.md). Casos de execução estão planejados, sem evidência de conexão real.**

| Casos | Requisitos / resultado esperado |
|---|---|
| WF-T01–T02 | WF-01/07: ferramenta ausente ou evidência antiga bloqueia, zero envios. |
| WF-T03–T05 | WF-02/03: distinguir autenticação desconhecida, login necessário e ativo negado; divergência de principal/família/operação bloqueia. |
| WF-T06–T07 | WF-04/07: aprovação ausente, divergente, expirada ou usada bloqueia. |
| WF-T08 | WF-05: instruções na resposta não ampliam autoridade. |
| WF-T09–T10 | WF-06/08: timeout após escrita fica indeterminado; canários não vazam. |
| WF-T11–T12 | WF-04/08: canonicalização estável e limites de prazo/tamanho/tentativas comprovados. |

Os exemplos `valid-read` e `valid-write` passam na estrutura; não comprovam autoridade. `invalid-missing-asset` deve falhar no esquema. `invalid-approval-binding` e `invalid-asset-denied` passam no esquema, mas rejeitam semanticamente com `APPROVAL_MISMATCH` e `ASSET_DENIED`. O recibo válido demonstra incerteza de escrita, não sucesso. Use relógio sintético `2030-01-01T00:01:00Z`.

Para cada execução registre caso, revisão, política, ambiente, relógio, digest, esperado, observado, número de envios, recibo e revisor. Identifique versão do validador e checagem de formato de datas. Separe: validação estrutural, testes semânticos e testes de integração autorizados. Falha, ignorado e não executado nunca equivalem a aprovado. Não exporte credenciais ou identificadores privados para demonstrar os testes.
