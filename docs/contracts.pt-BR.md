# Contratos de dados

[README](../README.pt-BR.md)

[Exemplo sintético](../examples/contract.json)

| Campo | Tipo ilustrativo do valor JSON |
| --- | --- |
| `connector_family` | `str` |
| `operation` | `str` |
| `mode` | `str` |
| `asset_ref` | `str` |
| `authentication` | `str` |
| `capability_checked` | `bool` |

O exemplo é deliberadamente sintético e serve à documentação; não constitui esquema de produção. Valores vazios, ausentes e desconhecidos devem permanecer distintos. Validar a estrutura na entrada, normalizar preservando o significado e registrar versão e contexto de coleta dos dados derivados. Mensagens de erro não devem reproduzir credenciais ou dados pessoais.
