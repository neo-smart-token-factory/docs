# 📦 Repositórios Necessários — NΞØ SMART FACTORY

> **Lista completa de repositórios para migração multi-repo**

> **✅ GitHub Organization**: [`neo-smart-token-factory`](https://github.com/neo-smart-token-factory)

---

## 🎯 Repositórios a Criar

### Total: **8 repositórios**

---

## 📦 Repositórios Core (Prioridade ALTA)

### 1. `smart-core`

**Status**: ✅ Migrar de `forge-core/`  
**GitHub**: `neo-smart-token-factory/smart-core`  
**NPM**: `@neosmart/core`  
**Descrição**: Contratos inteligentes, scripts de deploy, templates

**Conteúdo atual**:

- `forge-core/contracts/` → `smart-core/contracts/`
- `forge-core/scripts/` → `smart-core/scripts/`
- `forge-core/test/` → `smart-core/test/`
- `forge-core/templates/` → `smart-core/templates/`

---

### 2. `smart-ui`
**Status**: ✅ Migrar de `forge-ui/`  
**GitHub**: `neo-smart-token-factory/smart-ui`  
**NPM**: `@neosmart/ui`  
**Descrição**: Interface visual, PWA, landing page

**Conteúdo atual**:
- `forge-ui/landing/` → `smart-ui/landing/`
- `forge-ui/nuxt-app/` → `smart-ui/nuxt-app/`

---

### 3. `smart-cli`
**Status**: ✅ Migrar de `forge-cli/`  
**GitHub**: `neo-smart-token-factory/smart-cli`  
**NPM**: `nxf` ou `@neosmart/cli`  
**Descrição**: CLI universal

**Conteúdo atual**:
- `forge-cli/bin/` → `smart-cli/bin/`
- `forge-cli/commands/` → `smart-cli/commands/`

---

## 🧠 Repositórios de Inteligência (Prioridade MÉDIA)

### 4. `smart-oracle`
**Status**: 🔨 Criar novo (v0.6.0)  
**GitHub**: `neo-smart-token-factory/smart-oracle`  
**NPM**: `@neosmart/oracle`  
**Descrição**: Sistema de refinamento via LLM

**Conteúdo base**:
- `internal-ops/scripts/ecosystem-simulator.js` (inspiração)
- Novo código TypeScript

---

### 5. `smart-cult`
**Status**: 🔨 Criar novo (v0.7.0)  
**GitHub**: `neo-smart-token-factory/smart-cult`  
**NPM**: `@neosmart/cult`  
**Descrição**: Geração de narrativa e documentos

**Conteúdo base**:
- `internal-ops/scripts/marketing-engine.js` (inspiração)
- Novo código TypeScript

---

## 📊 Repositórios de Dados (Prioridade MÉDIA)

### 6. `smart-dna`
**Status**: 🔨 Criar novo (v0.6.0)  
**GitHub**: `neo-smart-token-factory/smart-dna`  
**NPM**: `@neosmart/dna`  
**Descrição**: Schema JSON, validação, templates

**Conteúdo base**:
- `internal-ops/tokens/template.json` (inspiração)
- Novo código TypeScript + JSON Schema

---

## 🎛️ Repositórios de Orquestração (Prioridade BAIXA)

### 7. `smart-kernel`
**Status**: 🔜 Criar novo (v0.8.0)  
**GitHub**: `neo-smart-token-factory/smart-kernel`  
**NPM**: `@neosmart/kernel`  
**Descrição**: Orquestrador central, pipeline completo

**Conteúdo**: Novo código TypeScript

---

## 📚 Repositórios de Documentação (Prioridade ALTA)

### 8. `docs`
**Status**: ✅ Migrar de `docs/`  
**GitHub**: `neo-smart-token-factory/docs`  
**URL**: `docs.neosmart.factory`  
**Descrição**: Documentação centralizada

**Conteúdo atual**:
- `docs/` → `docs/` (mesma estrutura)

---

## 📋 Checklist de Criação

### GitHub Organization: `neo-smart-token-factory`

**Repositórios Core (Criar AGORA)**:
- [ ] `neo-smart-token-factory/smart-core` (privado inicialmente)
- [ ] `neo-smart-token-factory/smart-ui` (privado inicialmente)
- [ ] `neo-smart-token-factory/smart-cli` (privado inicialmente)
- [ ] `neo-smart-token-factory/docs` (público)

**Repositórios Futuros (Criar quando necessário)**:
- [ ] `neo-smart-token-factory/smart-oracle` (v0.6.0)
- [ ] `neo-smart-token-factory/smart-cult` (v0.7.0)
- [ ] `neo-smart-token-factory/smart-dna` (v0.6.0)
- [ ] `neo-smart-token-factory/smart-kernel` (v0.8.0)

---

## 🔧 Comandos GitHub CLI

```bash
# 1. Criar GitHub Organization (via web)
# github.com/organizations/new
# Nome: neo-smart-token-factory

# 2. Criar repositórios Core
gh repo create neo-smart-token-factory/smart-core --private --description "Smart contracts and deployment scripts"
gh repo create neo-smart-token-factory/smart-ui --private --description "UI interface, PWA, landing page"
gh repo create neo-smart-token-factory/smart-cli --private --description "CLI universal (nxf)"
gh repo create neo-smart-token-factory/docs --public --description "Documentation"

# 3. Criar repositórios Futuros (quando necessário)
gh repo create neo-smart-token-factory/smart-oracle --private --description "LLM-based refinement system"
gh repo create neo-smart-token-factory/smart-cult --private --description "Narrative and document generation"
gh repo create neo-smart-token-factory/smart-dna --private --description "DNA schema and validation"
gh repo create neo-smart-token-factory/smart-kernel --private --description "Orchestrator and pipeline"
```

---

## 📦 NPM Organization

**Organization**: `@neosmart`  
**Criar via**: npmjs.com/org/create

**Packages a publicar**:
- `@neosmart/core`
- `@neosmart/ui`
- `nxf` (ou `@neosmart/cli`)
- `@neosmart/oracle` (futuro)
- `@neosmart/cult` (futuro)
- `@neosmart/dna` (futuro)
- `@neosmart/kernel` (futuro)

---

## 🎯 Priorização

### Fase 1 (AGORA - Semana 1-2)

1. ✅ Criar GitHub Organization `neo-smart-token-factory`
2. ✅ Criar `smart-core` (privado)
3. ✅ Criar `smart-ui` (privado)
4. ✅ Criar `smart-cli` (privado)
5. ✅ Criar `docs` (público)

### Fase 2 (Futuro - v0.6.0)

6. 🔨 Criar `smart-oracle` (quando iniciar desenvolvimento)
7. 🔨 Criar `smart-dna` (quando iniciar desenvolvimento)

### Fase 3 (Futuro - v0.7.0)

8. 🔨 Criar `smart-cult` (quando iniciar desenvolvimento)

### Fase 4 (Futuro - v0.8.0)

9. 🔜 Criar `smart-kernel` (quando iniciar desenvolvimento)

---

## 📝 Notas Importantes

1. **Nomenclatura**: Os documentos propõem `smart-*`, mas a estrutura atual usa `forge-*`. Decidir antes de criar.

2. **Visibilidade**: Repositórios Core podem começar privados até estarem prontos.

3. **NPM**: Criar organization `@neosmart` antes de publicar packages.

4. **Docs**: Pode ser público desde o início.

---

**Última atualização**: 2024-01-01  
**Versão**: v0.5.1 — IGNIÇÃO

