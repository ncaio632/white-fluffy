# Estratégia de validação

[README](../README.pt-BR.md)

| Cenário | Comportamento esperado |
| --- | --- |
| Authenticated but unauthorized | Relatar falha de escopo separadamente do login |
| Unavailable tool | Interromper a operação em vez de presumir capacidade |
| Remote instruction payload | Não executar texto de instrução retornado como dado |
| Write operation | Exigir ativo e efeito pretendido explícitos |

## Política de evidência

Registrar revisão, ambiente, classe de entrada, resultado esperado e observado para cada verificação executada. Separar cenários planejados de resultados medidos. Testes do backup privado e verificações desta documentação não certificam prontidão do produto, resultados de campanhas ou segurança de produção.
