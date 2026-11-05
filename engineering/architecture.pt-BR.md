# Arquitetura e máquina de estados

**Resumo operacional; interfaces completas em [inglês](architecture.en.md). Não descreve servidor implantado.**

Separe `InventoryAdapter`, `CredentialBroker`, `GrantResolver`, `EffectClassifier`, `BoundaryEvaluator`, `ApprovalLedger`, `Dispatcher` e `AuditSink`. O avaliador recebe observações e política e devolve uma decisão sem executar ferramentas. O broker resolve a referência de credencial em ambiente privado. O classificador usa um mapeamento local revisado, vinculado ao digest do descritor; uma dica remota de somente leitura não é prova suficiente.

```text
NEW -> INVENTORY_CHECKED -> AUTHENTICATED -> ASSET_AUTHORIZED -> CLASSIFIED
CLASSIFIED -> READY (leitura)
CLASSIFIED -> AWAITING_APPROVAL -> APPROVED -> READY (escrita)
READY -> AUDIT_RECORDED -> DISPATCHING -> SUCCEEDED | FAILED | INDETERMINATE
qualquer etapa anterior ao envio -> BLOCKED
```

Cada transição exige uma condição registrada. Antes do envio, confira novamente sessão, principal, validade e revisão da permissão. Consuma a aprovação atomicamente com o registro da intenção; falha de auditoria anterior ao envio bloqueia escrita. Uma queda após registrar intenção exige reconciliação, pois o consumo da aprovação não comprova o efeito.

Se houver timeout após enviar escrita, registre `DISPATCH_UNKNOWN`; faça leitura autorizada para reconciliar. Não reenviar ao reiniciar. Um novo ativo ou payload exige nova aprovação. Retenha observações anteriores por referência e saneie exportações públicas. O primeiro erro segue a ordem das fronteiras; desconhecido e negado continuam distintos.
