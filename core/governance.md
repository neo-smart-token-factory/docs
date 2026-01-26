# Protocolo NΞØ: Visão Geral da Governança

## Propósito da Governança
A governança no Protocolo NΞØ foi projetada para garantir a integridade técnica, segurança e consistência em todos os repositórios da organização. À medida que o ecossistema escala, essas regras evitam a "entropia técnica" e garantem que cada contribuição atenda aos altos padrões exigidos para uma infraestrutura Web3 pronta para produção.

## Por que os Workflows existem
Os fluxos de trabalho (workflows) são a aplicação automatizada da nossa cultura de desenvolvimento. Eles servem para:
-**Garantir a Reprodutibilidade:** Toda mudança deve passar pelo mesmo processo rigoroso de verificação.
-**Manter a Paridade da Documentação:** Código e documentação nunca devem se distanciar.
-**Padronizar a Qualidade:** Seja um contrato inteligente no `smart-core` ou um componente de UI no `smart-ui`, o nível mínimo de qualidade é imposto.
-**Fornecer Auditabilidade:** Um rastro claro de PRs, revisões e aprovações de CI é essencial para auditorias de segurança e transparência.

## Do que eles protegem
-**Corrupção por Push Direto:** Prevenção de alterações acidentais ou não autorizadas na branch `main`.
-**Builds Quebrados:** Garantir que nenhum PR seja mesclado se quebrar a compilação ou os testes.
-**Lacunas de Documentação:** Impedir mudanças de código que não sejam refletidas na `docs` ou na documentação interna do repositório.
-**Deriva de Licença:** Garantir que a postura legal e de código aberto (ou fechado) da organização permaneça consistente.
-**Desvio Arquitetural:** Garantir que as mudanças estejam alinhadas com os Registros de Decisão Arquitetural (ADR).

## O que NÃO é automatizado intencionalmente
-**Lógica de Aprovação:** Um humano DEVE sempre revisar e aprovar um Pull Request. Não confiamos em bots para aprovações finais de arquitetura ou segurança.
-**Decisões de Merge:** Não usamos "Auto-Merge". O ato final de mesclar continua sendo uma decisão humana consciente.
-**Detecção de Bugs Complexos:** Enquanto o CI captura falhas de sintaxe e testes, falhas de lógica e segurança exigem revisão humana especializada.
-**Direção Estratégica:** Os workflows impõem *como* construímos, não *o que* construímos.
