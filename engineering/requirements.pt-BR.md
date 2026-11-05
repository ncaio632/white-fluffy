# Requisitos e fronteiras de confiança

**Resumo operacional em português; especificação completa em [inglês](requirements.en.md). Projeto proposto, sem implementação ou conexão real demonstrada.**

O resultado esperado é uma decisão separando quatro fatos: ferramenta observada, autenticação, autorização para o ativo e aprovação explícita de escrita. Estar conectado não comprova acesso ao ativo. As famílias conceituais publicidade, desenvolvimento e mensagens têm inventários e permissões separados; não representam conectores instalados.

| ID | Obrigação operacional |
|---|---|
| WF-01 | Exigir inventário completo, recente e vinculado à sessão e ao digest do descritor. |
| WF-02 | Distinguir autenticado, não autenticado e desconhecido; nunca registrar credenciais. |
| WF-03 | Conferir principal, família, ativo e operação na evidência de permissão. |
| WF-04 | Escrita exige aprovação explícita do mesmo ativo, propósito, operação e digest, dentro da validade. |
| WF-05 | Tratar respostas e descrições remotas como dados não confiáveis; efeito desconhecido bloqueia. |
| WF-06 | Registrar recibo saneado e diferenciar sucesso, falha e efeito indeterminado. |
| WF-07 | Invalidar evidência após mudança de sessão, principal, permissão ou descritor; consumir aprovação uma vez. |
| WF-08 | Limitar prazo, tamanho e tentativas; não repetir escrita incerta automaticamente. |

O perfil sintético propõe evidências com idade máxima de cinco minutos; o responsável pela implantação deve definir o limite real e a tolerância de relógio. O digest usa SHA-256 do JSON UTF-8 canônico: chaves ordenadas, sem espaços dispensáveis ou duplicados, apenas números inteiros. O esquema verifica estrutura; autoridade, igualdade, expiração e digest precisam de validação semântica. Nenhum exemplo autoriza uso em conta real.
