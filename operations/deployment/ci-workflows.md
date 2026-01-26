# Especificação de Fluxos de Trabalho de CI

Cada repositório na organização deve implementar os seguintes fluxos de trabalho do GitHub Actions (ou equivalentes).

## 1. Guarda de Documentação (Docs Guard)
-**Verificação:** Escaneia o diff em busca de alterações no código.
-**Critério:** Se arquivos `.js`, `.ts`, `.sol` ou `.go` forem alterados, verifica se algum arquivo `.md` no repositório ou no repositório central de `docs` foi atualizado no mesmo contexto.
-**Quando:** No Pull Request.
-**Condição de Falha:** Falha crítica se o código mudar significativamente sem atualizações na documentação.

## 2. Guarda de Escopo (Scope Guard)
-**Verificação:** Monitora alterações em caminhos restritos (ex: configurações de CI, protocolos centrais).
-**Critério:** Prevenir modificação não autorizada ou acidental de arquivos críticos para a governança.
-**Quando:** No Pull Request.
-**Condição de Falha:** Falha crítica se caminhos restritos forem modificados sem uma label específica de "Admin Override" ou aprovação dupla.

## 3. Guarda de Licença (License Guard)
-**Verificação:** Escaneia cabeçalhos de licença em novos arquivos e verifica arquivos `package.json` / `LICENSE`.
-**Critério:** Todos os arquivos devem ter o cabeçalho de licença apropriado da organização.
-**Quando:** No Pull Request e Push para Main.
-**Condição de Falha:** Falha crítica se licenças incompatíveis forem introduzidas ou se faltarem cabeçalhos.

## 4. Guarda de Build/Test (Específico por Repositório)
-**Verificação:** Executa `npm run build`, `npm test` ou equivalente.
-**Critério:** Tolerância zero para erros de compilação ou falhas nos testes.
-**Quando:** No Pull Request e em cada Push.
-**Condição de Falha:** Falha crítica em qualquer código de saída diferente de 0.

## 5. Verificação de Referência ADR (Guarda de Arquitetura)
-**Verificação:** Escaneia a descrição do PR em busca de referências a `ADR` (Registros de Decisão Arquitetural).
-**Critério:** Se um PR for marcado como `refactor` ou `feat` (major), ele DEVE referenciar um ID de ADR do repositório de `docs`.
-**Quando:** No Pull Request.
-**Condição de Falha:** Aviso/Falha leve para alterações menores; Falha crítica para grandes mudanças arquiteturais sem ADR.

## 6. Varredura de Segurança (Lint & Audit)
-**Verificação:** Executa `npm audit`, `eslint` ou linters focados em segurança (ex: Slither para `smart-core`).
-**Critério:** Sem vulnerabilidades críticas ou erros de linting de alto nível.
-**Quando:** No Pull Request.
-**Condição de Falha:** Falha crítica em caso de vulnerabilidades críticas detectadas.
