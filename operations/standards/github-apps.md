# Aplicativos e Integrações do GitHub

Para manter a governança em toda a organização, as seguintes integrações são obrigatórias ou recomendadas.

## 1. Aplicativos Obrigatórios
-**GitHub Actions:** Nosso executor principal de CI/CD.
-**Dependabot:** Atualizações automáticas de dependências e alertas de segurança. Deve ser configurado para abrir PRs para patches de segurança imediatamente.
-**Codecov (ou similar):** Para rastrear e aplicar limites de cobertura de teste (especialmente para `smart-core` e `smart-cli`).

## 2. Aplicativos Recomendados
-**Snyk:** Varredura profunda de vulnerabilidades para dependências e imagens de contêiner.
-**Integração Linear / Jira:** Para sincronizar Pull Requests com tarefas de gerenciamento de projeto.
-**Integração Slack/Discord:** Para alertas em tempo real sobre PRs e falhas de CI.

## 3. Problemas que esses Aplicativos Resolvem
-**Degradação de Dependências:** O Dependabot garante que não estamos construindo sobre bibliotecas desatualizadas ou vulneráveis.
-**Visibilidade:** As integrações garantem que a equipe não precise ficar checando o GitHub manualmente; a informação é enviada para onde trabalhamos.
-**Métricas de Qualidade:** O Codecov fornece uma métrica objetiva para "Quanto desta mudança está realmente testada?".

## 4. O que NÃO deve ser instalado
-**Bots de Auto-Merge:** Qualquer bot que mescle PRs automaticamente sem um clique humano é estritamente proibido.
-**Linters de Terceiros não Verificados:** Use apenas ferramentas de segurança bem conhecidas e validadas pela comunidade.
-**"Revisores de IA" Genéricos:** Até que sejam especificamente validados, comentários de PR gerados por IA devem ser usados como auxílio, não como bloqueadores ou aprovações autoritativas.
-**Acesso público a metadados de Repos Privados:** Qualquer aplicativo que exija permissões excessivas para dados de repositórios privados sem um benefício claro.
