# Backlog e critérios de aceite

**Resumo acionável de planejamento; detalhes em [inglês](backlog.en.md). Nenhum item é declarado concluído.**

| Item | Entrega / aceite mínimo |
|---|---|
| WF-B1 | Parser e canonicalização: rejeitar campos/chaves inválidos; ordem equivalente gera mesmo digest. |
| WF-B2 | Observadores: inventário parcial, antigo ou de outra sessão bloqueia; credenciais não aparecem nos recibos. |
| WF-B3 | Avaliador de permissões: login válido com ativo negado ou desconhecido produz zero envios; testar cada dimensão separadamente. |
| WF-B4 | Mapeamento de efeitos e ledger: efeito desconhecido, aprovação expirada, divergente ou reutilizada bloqueiam. |
| WF-B5 | Envio e reconciliação: timeout após efeito simulado fica indeterminado; reinício não repete escrita. |
| WF-B6 | Diagnóstico e qualificação: canários secretos não aparecem nos registros; cada ferramenta tem descritor e autorização testados. |

Implemente nessa ordem, com B2 dependendo de B1 e assim por diante. Antes de piloto real, defina relógio confiável, validade das observações, identidade do aprovador e auditoria durável. Antes de escrita, execute os negativos de aprovação e documente uma leitura de reconciliação; sem ela, mantenha escrita desabilitada.

Os quatro papéis em `agents/` revisam capacidade, autorização, operação e evidência. Eles recebem entregas explícitas; não iniciam execução ou concedem acesso por conta própria. Mudança na canonicalização exige nova versão e invalida aprovações pendentes. Publique apenas evidências medidas da revisão testada, sem preencher lacunas com material privado.
