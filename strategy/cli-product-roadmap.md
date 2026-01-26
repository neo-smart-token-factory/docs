# Plano Estratégico: Roadmap da CLI como Produto

## Posicionamento
O CLI `nsf` (NΞØ Smart Factory) não é apenas uma ferramenta; é o **Centro de Comando para Operadores Web3**. Ele está posicionado entre a simplicidade de uma UI e o poder de scripts puros, oferecendo "Operações Cirúrgicas" para gerenciamento de tokens.

## Proposta de Valor Principal
-**A Mentalidade "Doctor":** Em vez de adivinhar por que uma implantação falhou ou por que o gas está alto, a CLI diagnostica e corrige.
-**Velocidade para Produção:** Vá dos metadados ao contrato verificado em menos de 2 minutos.
-**Saúde do Ecossistema:** Uma visão única de todos os repositórios e seu status de sincronização.

## Fronteiras entre Gratuito e Pago
-**Nível Gratuito:**
  - Verificações básicas do `doctor`.
  - Visualizações do ecossistema em modo somente leitura.
  - Implantação manual em rede única.
-**Nível Pago (Pro):**
  - Reparos avançados (Correção automática via `doctor`).
  - Implantações em lote em vários esquemas.
  - Scripts de integração CI/CD premium.
  - Acesso prioritário a RPC.

## Conjunto de Funcionalidades Iniciais (Foco no "Doctor")
O comando `doctor` é o gerador de leads.
-**Fase 0 - Check-up de Saúde:** Verifica se o ambiente está pronto (ENVs, Chaves, RPCs).
-**Fase 1 - Verificação de Contrato:** Verifica o status da implantação vs. configuração.
-**Fase 2 - Sincronização de Reparo:** Automatiza a reconciliação do estado de `ops-sync`.

## Roadmap por Fases

### Fase 1: AGORA (Fundamentos e Diagnóstico)
-[ ] Estabilizar o comando `doctor` para a saúde do ecossistema.
-[ ] Implementar `ops-view` para mostrar o Dashboard (estado de operações internas) no terminal.
-[ ] Colocar placeholders "Pro" (exibindo funcionalidades que exigem licença).

### Fase 2: PRÓXIMO (Operações Cirúrgicas)
-[ ] Implementar "Implantações Cirúrgicas" (implantar módulos específicos sem rodar a factory completa).
-[ ] Integração com API do Etherscan/Blockscout para gatilhos de verificação automatizados.
-[ ] Primeira versão do sistema de "Gerenciamento de Licenças".

### Fase 3: DEPOIS (Automação e Escala)
-[ ] "Modo Watcher": A CLI permanece aberta e monitora gas/contratos, executando gatilhos automaticamente.
-[ ] Gerenciamento de equipe multi-usuário para comandos da CLI.
-[ ] Integração com IA (AgentKit) para operações autônomas.
