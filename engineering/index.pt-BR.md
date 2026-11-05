# Engenharia — white-fluffy

**Estado: especificação proposta e contratos sintéticos. Não há runtime público nem resultado medido de conexão, backup ou recuperação neste pacote.** Os guias em português e japonês são resumos acionáveis; o texto completo está em inglês. A documentação anterior em `docs/` permanece preservada.

Leia requisitos, arquitetura, procedimento, backlog e validação. Esquema, semântica e execução são camadas distintas. Papéis em `agents/` só atuam por atribuição explícita; não iniciam processos ou modelos automaticamente.

[English](index.en.md) · [Português](index.pt-BR.md) · [日本語](index.ja.md)

- [Requisitos](requirements.pt-BR.md) · [English](requirements.en.md) · [pt-BR](requirements.pt-BR.md) · [日本語](requirements.ja.md)
- [Arquitetura e estados](architecture.pt-BR.md) · [English](architecture.en.md) · [pt-BR](architecture.pt-BR.md) · [日本語](architecture.ja.md)
- [Procedimento completo](runbook.pt-BR.md) · [English](runbook.en.md) · [pt-BR](runbook.pt-BR.md) · [日本語](runbook.ja.md)
- [Backlog e aceite](backlog.pt-BR.md) · [English](backlog.en.md) · [pt-BR](backlog.pt-BR.md) · [日本語](backlog.ja.md)
- [Rastreabilidade e validação](validation.pt-BR.md) · [English](validation.en.md) · [pt-BR](validation.pt-BR.md) · [日本語](validation.ja.md)

## Contracts / Contratos / 契約

- [Contract semantics and hashing](../contracts/README.md)
- [Machine-readable validation cases](../contracts/validation-cases.json)
- [operation-envelope.schema.json](../contracts/operation-envelope.schema.json)
- [decision-receipt.schema.json](../contracts/decision-receipt.schema.json)

## Fixtures / Exemplos / 合成例

- [Fixture guide](../examples/engineering/README.md)
- [valid-read.json](../examples/engineering/valid-read.json)
- [valid-write.json](../examples/engineering/valid-write.json)
- [invalid-missing-asset.json](../examples/engineering/invalid-missing-asset.json)
- [invalid-approval-binding.json](../examples/engineering/invalid-approval-binding.json)
- [invalid-asset-denied.json](../examples/engineering/invalid-asset-denied.json)
- [valid-receipt.json](../examples/engineering/valid-receipt.json)

## Roles / Papéis / 役割

- [Repository agent contract](../AGENTS.md)
- [Capability and inventory reviewer](../agents/capability-reviewer.md)
- [Authentication and asset authorization reviewer](../agents/authorization-reviewer.md)
- [Controlled operation and reconciliation reviewer](../agents/operation-reviewer.md)
- [Validation and public evidence reviewer](../agents/evidence-reviewer.md)

## Limits / Limites / 制限

English: the validation matrix is a plan. Record measured results separately with revision, environment and case IDs. No network or production security guarantee is implied.

Português: a matriz é planejada; medições exigem revisão, ambiente e casos identificados. Não implica garantia de rede ou produção.

日本語: 検証表は計画である。実測は改訂・環境・ケースIDと別途記録し、ネットワークや本番安全性を保証しない。
