# Issue Template: Padronização de Nomenclatura

**Título sugerido:** `chore: Enforce 'Smart' Nomenclature (Deprecate 'Forge')`

## 🚨 Atenção: Mudança Normativa Obrigatória

Conforme decisão oficial de **2026-01-24**, a nomenclatura `FORGE` foi oficialmente **descontinuada** e substituída por `SMART` em todo o ecossistema.

Este repositório deve ser auditado e atualizado imediatamente para conformidade.

### 📄 Referência Oficial
Consulte o documento normativo: `docs/auditoria/NOMENCLATURA_OFICIAL.md`

---

## 📋 Checklist de Verificação

### 1. Código e Arquivos
-[ ] Substituir `ForgeToken` por `NeoToken` ou `SmartToken`
-[ ] Substituir `ForgeFactory` por `NeoSmartFactory` ou `NeoJettonFactory` (se TON)
-[ ] Renomear arquivos que contenham `forge` no nome
-[ ] Verificar nomes de variáveis e funções (`forgeCore`, `initForge`, etc.)

### 2. Configuração e Metadata
-[ ] `package.json`: Verificar `name` e dependências (usar `@neosmart/*`)
-[ ] `README.md`: Remover referências a "Neural Forge" ou "Forge Factory"
-[ ] Comentários de código: Atualizar TODOs e Docs internos

### 3. Branding
-[ ] Nome do Projeto: **NΞØ Smart Token Factory**
-[ ] CLI: **`nsf`** (e não `neo-smart-factory` ou `forge`)

---

## 🚫 Termos Proibidos (Search & Destroy)

Execute `grep -r "forge" .` e elimine ocorrências de:
-`forge-core`
-`forge-ui`
-`forge-cli`
-`Neural Forge`

> **Nota:** Se houver menções históricas em arquivos de CHANGELOG ou ARCHIVE, adicione uma nota de aviso no topo do arquivo informando que a terminologia é obsoleta, mas **não altere o histórico se não for estritamente necessário**.

---

**Prioridade**: Máxima 🔴
**Assignee**: Tech Lead / Maintainer
