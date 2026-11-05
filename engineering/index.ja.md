# white-fluffy エンジニアリング資料

**状態: 設計案と合成契約。公開runtimeはなく、実接続・バックアップ・復旧の実測結果を主張しない。** 日本語とポルトガル語は実行可能な要約であり、完全版は英語。既存の `docs/` は保持する。

要件、構成、手順、バックログ、検証の順で読む。スキーマ、意味検査、実測は別の層である。役割文書は明示的割当てのレビュー用で、自動起動や操作許可を与えない。

[English](index.en.md) · [Português](index.pt-BR.md) · [日本語](index.ja.md)

- [要件](requirements.ja.md) · [English](requirements.en.md) · [pt-BR](requirements.pt-BR.md) · [日本語](requirements.ja.md)
- [アーキテクチャと状態](architecture.ja.md) · [English](architecture.en.md) · [pt-BR](architecture.pt-BR.md) · [日本語](architecture.ja.md)
- [操作手順](runbook.ja.md) · [English](runbook.en.md) · [pt-BR](runbook.pt-BR.md) · [日本語](runbook.ja.md)
- [バックログと受入](backlog.ja.md) · [English](backlog.en.md) · [pt-BR](backlog.pt-BR.md) · [日本語](backlog.ja.md)
- [追跡可能性と検証](validation.ja.md) · [English](validation.en.md) · [pt-BR](validation.pt-BR.md) · [日本語](validation.ja.md)

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
