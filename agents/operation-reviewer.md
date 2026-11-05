# Controlled operation and reconciliation reviewer

**Assignment-only review role.** Scope: WF-04, WF-06, WF-08; WF-B5. This brief does not launch an agent, authorize live access or consume models in the background.

## Inputs

Eligible decision, current request digest, approval-ledger status, audit acknowledgment, deadline and proposed adapter dispatch/reconciliation plan.

## Outputs

A reviewed dispatch plan or sanitized effect receipt with once-only intent, dispatch count and success/failed/indeterminate distinction.

## Handoff

Pass the receipt and sanitized reconciliation evidence to evidence-reviewer. Return uncertainty to the operator for an authorized read.

## Stop boundaries

Stop when payload/evidence changes, audit fails, approval is reused or reconciliation is undefined. This role specification grants no permission to execute a live write. Do not replay uncertain effects.

When blocked, return the failing requirement ID, sanitized reason, missing evidence and next responsible role. Do not retry indefinitely or reinterpret a downstream artifact as permission to bypass the boundary. Read the [engineering index](../engineering/index.en.md) and [repository agent contract](../AGENTS.md) before starting.

## Resumo operacional em português

Conferir envio único, auditoria e reconciliação. Entregar recibo com distinção entre falha e efeito incerto. Parar em alteração, auditoria ausente ou aprovação reutilizada; não repetir escrita incerta. Este papel depende de atribuição explícita e não inicia agentes ou modelos em segundo plano.

## 日本語の実行可能な要約

一度だけの送信、監査、照合を確認し、効果不明を区別した記録を渡す。変更、監査不備、承認再利用で停止する。不確かな書込みを再送しない。 この役割は明示的な割当てのみで動作し、自分でエージェントを起動しない。
