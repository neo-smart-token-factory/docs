# Linha de Base de Workflow do Repositório

Esta linha de base se aplica a TODOS os repositórios dentro da organização `neo-smart-token-factory`:
-`docs` (Público)
-`smart-ui` (Público)
-`landing` (Privado)
-`smart-cli` (Privado)
-`smart-core` (Privado)
-`internal-ops` (Privado)

## 1. Regras de Proteção de Branch
-**Branch:** `main` (e `master`, se aplicável).
-**Sem Pushes Diretos:** Todas as alterações devem ser enviadas via Pull Request.
-**Exigir Commits Assinados:** Todas as contribuições devem ser assinadas criptograficamente.
-**Exigir Histórico Linear:** Preferência por merges do tipo rebase ou squash para manter o histórico limpo.

## 2. Requisitos de Pull Request (PR)
-**Revisores Obrigatórios:** Pelo menos uma aprovação humana (mantenedor) é necessária.
-**Verificações de Status:** Todos os fluxos de trabalho de CI (definidos em `ci-workflows-spec.md`) devem passar.
-**Issues Vinculadas:** Cada PR deve estar vinculado a pelo menos uma issue ou referência de ADR.
-**Template de Descrição:** Deve incluir "O que mudou", "Por que" e "Testes realizados".

## 3. Disciplina de Commit (Conventional Commits)
Todos os commits devem seguir a especificação [Conventional Commits](<https://www.conventionalcommits.org/>):
-`<tipo>[escopo opcional]: <descrição>`
-Tipos: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`.
-*Exemplo:* `feat(cli): adiciona diagnóstico de comando doctor para conectividade rpc`

## 4. Guarda de Documentação (Docs Guard)
-Qualquer PR que modifique arquivos de código (`src/`, `lib/`, etc.) deve ser verificado quanto às alterações correspondentes em arquivos `docs/` ou `.md` dentro do repositório.
-Se uma funcionalidade for adicionada sem documentação, o PR será marcado como "Incompleto".

## 5. Guarda de Escopo (Scope Guard)
-Caminhos protegidos (por exemplo, `.github/workflows/`, `security/`, `licenses/`) exigem atenção explícita.
-Alterações nestes caminhos devem disparar alertas/revisões adicionais.
