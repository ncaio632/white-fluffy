# Procedimento completo de operação

**Resumo acionável; procedimento detalhado em [inglês](runbook.en.md). Não pressupõe ferramentas conectadas.**

1. Registre revisão, política, ambiente e caso. Use adaptador isolado e contador de envios; rejeite chaves JSON duplicadas e campos desconhecidos.
2. Selecione família, ferramenta, operação e ativo. Confirme o efeito pelo mapeamento confiável. Sem classificação, pare com `EFFECT_UNKNOWN`.
3. Colete inventário completo da sessão e digest do descritor. Após reconectar, descubra novamente. Inventário parcial não prova ausência.
4. Autentique por referência privada; registre apenas status e principal sintético. Consulte permissão do mesmo principal, família, ativo e operação. Desconhecido não permite leitura de diagnóstico.
5. Execute os exemplos com relógio artificial `2030-01-01T00:01:00Z`. Uma leitura real exige todas as fronteiras e limite mínimo de dados.
6. Para escrita, apresente ativo, propósito, operação, digest e validade. Obtenha aprovação específica por fluxo autorizado e verifique a autoridade do aprovador. Alterar payload exige nova aprovação.
7. Revalide, consuma aprovação uma vez, persista intenção e envie uma vez. Timeout após envio gera estado indeterminado; reconcilie por leitura autorizada, sem repetição automática.
8. Feche com esperado, observado, número de envios e recibos saneados. Preserve falhas e casos não executados.

Mudança de sessão, credencial ou permissão invalida decisões pendentes. Se auditoria falhar antes do envio, bloqueie; após o envio, preserve intenção e escale a reconciliação. Sem prova do efeito, mantenha incerteza. Não há chamadas periódicas a modelos nem operação autônoma implícita neste procedimento.
