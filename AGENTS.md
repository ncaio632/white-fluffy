# Agent work contract — white-fluffy

This repository is a public engineering reference. Read [the engineering index](engineering/index.en.md), the requirements, contracts and validation guide before changing artifacts. Existing public notes are historical context; the new engineering package is a proposed specification unless a separate measured evidence record says otherwise. Preserve older documentation; create a new revision rather than silently replacing a delivered design.

Work only on explicitly assigned tasks. The four briefs in `agents/` are review roles, not executable agents or permission grants. Do not self-launch, spawn follow-up agents, run periodic models or create background model usage. An operator or supervising workflow must assign each role and handoff explicitly. Ordinary native automation is an implementation topic, not enabled by these files.

Use synthetic fixtures. Do not read private archives, copy private history, expose credentials, actual account identifiers, contact details, business records, screenshots or workstation paths in public material. Do not change destinations, publish, push Git refs or execute account writes based on this file. A current explicit user instruction and destination-specific review remain required for those actions.

Keep schema validation separate from semantic evaluation and execution evidence. Every new JSON fixture needs a row in `contracts/validation-cases.json`; schema-valid semantic negatives use `valid: true` and document their expected runtime error. Every English engineering guide needs pt-BR and Japanese counterparts, which may be clearly labeled actionable summaries. Keep locale indexes linked to all added artifacts. A role must report a stop boundary rather than skip an earlier failed gate.

Português: atribuições explícitas, exemplos sintéticos, sem autoexecução ou modelos em segundo plano. Validar estrutura, semântica e evidência separadamente; manter os três idiomas.

日本語: 明示的な担当割当てと合成例のみを使い、自動起動やバックグラウンドモデル実行をしない。構造、意味、実測を分け、三言語の索引を維持する。
