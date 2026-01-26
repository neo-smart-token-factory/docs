# Lista de Verificação para Inicialização de Repositório (Bootstrap)

Use esta lista sempre que um novo repositório for criado dentro da organização `neo-smart-token-factory`.

## 1. Configuração Inicial
-[ ] Inicializar com um `README.md` (seguindo o template da organização).
-[ ] Adicionar o arquivo de `LICENSE` padrão.
-[ ] Adicionar `.gitignore` específico para a stack tecnológica (Node, Go, Solidity, etc.).
-[ ] Definir a visibilidade do repositório (Privado por padrão, a menos que seja estratégico).

## 2. Configuração de Governança
-[ ] Habilitar "Protect main branch".
-[ ] Marcar "Require pull request reviews before merging".
-[ ] Marcar "Require status checks to pass before merging".
-[ ] Marcar "Require signed commits".
-[ ] Marcar "Include administrators" nas regras de proteção.

## 3. Integração de Fluxo de Trabalho (Workflow)
-[ ] Copiar `.github/workflows/docs-guard.yml` da referência em `docs`.
-[ ] Copiar `.github/workflows/scope-guard.yml`.
-[ ] Copiar `.github/workflows/license-guard.yml`.
-[ ] Configurar `build-and-test.yml` para a linguagem/framework específica do repositório.

## 4. Documentação e Etiquetas (Labels)
-[ ] Criar o arquivo básico `CONTRIBUTING.md`.
-[ ] Configurar etiquetas do GitHub (ex: `bug`, `feat`, `breaking-change`, `ADR-required`, `documentation`).
-[ ] Adicionar uma pasta `docs/` para detalhes técnicos específicos do repositório.

## 5. Segurança e Acesso
-[ ] Configurar Dependabot (`.github/dependabot.yml`).
-[ ] Atribuir pelo menos dois mantenedores com acesso de Admin/Escrita.
-[ ] Habilitar funcionalidades de segurança avançada do GitHub (se disponíveis para o repo).
