# Mapeamento: Estrutura Atual vs Proposta Futura

> **Guia de referência rápida**

---

## 📊 Tabela de Mapeamento

| Aspecto | Estrutura Atual (v0.5.1) | Proposta Futura (Multi-Repo) |
|---------|--------------------------|------------------------------|
| **Tipo** | Monorepo | Multi-repo (8 repositórios) |
| **GitHub** | `neo-smart-factory` (repo único) | `neosmart-factory/*` (org com 8 repos) |
| **Pastas** | `forge-core/`, `forge-ui/`, `forge-cli/` | `smart-core/`, `smart-ui/`, `smart-cli/` |
| **CLI** | `neo-smart-factory` | `nxf` (com `neo-smart-factory` como alias) |
| **NPM Scope** | `neo-smart-factory-*` | `@neosmart/*` |
| **Pacotes** | `neo-smart-factory-core`<br>`neo-smart-factory-ui`<br>`neo-smart-factory-cli` | `@neosmart/core`<br>`@neosmart/ui`<br>`nxf` ou `@neosmart/cli` |
| **Status** | ✅ Implementado | 🔜 Planejado |

---

## 🔄 Mapeamento de Módulos

### Core Layer

| Atual | Futuro | Status |
|-------|--------|--------|
| `forge-core/` | `smart-core/` | ✅ Migração planejada |
| `forge-core/contracts/` | `smart-core/contracts/` | ✅ Mesma estrutura |
| `forge-core/scripts/` | `smart-core/scripts/` | ✅ Mesma estrutura |

### Interface Layer

| Atual | Futuro | Status |
|-------|--------|--------|
| `forge-ui/` | `smart-ui/` | ✅ Migração planejada |
| `forge-ui/landing/` | `smart-ui/landing/` | ✅ Mesma estrutura |
| `forge-ui/nuxt-app/` | `smart-ui/nuxt-app/` | ✅ Mesma estrutura |
| `forge-cli/` | `smart-cli/` | ✅ Migração planejada |

### Intelligence Layer (Futuro)

| Atual | Futuro | Status |
|-------|--------|--------|
| `internal-ops/scripts/ecosystem-simulator.js` | `smart-oracle/` | 🔨 A ser criado |
| `internal-ops/scripts/marketing-engine.js` | `smart-cult/` | 🔨 A ser criado |

### Data Layer (Futuro)

| Atual | Futuro | Status |
|-------|--------|--------|
| `internal-ops/tokens/template.json` | `smart-dna/` | 🔨 A ser criado |

### Orchestration Layer (Futuro)

| Atual | Futuro | Status |
|-------|--------|--------|
| N/A (comandos separados) | `smart-kernel/` | 🔜 Planejado |

---

## 📦 Mapeamento de Pacotes NPM

### Atual (v0.5.1)

```json
{
  "name": "neo-smart-factory-core",
  "name": "neo-smart-factory-ui",
  "name": "neo-smart-factory-cli"
}
```

### Proposto (Futuro)

```json
{
  "name": "@neosmart/core",
  "name": "@neosmart/ui",
  "name": "nxf",
  "name": "@neosmart/oracle",
  "name": "@neosmart/cult",
  "name": "@neosmart/dna",
  "name": "@neosmart/kernel"
}
```

---

## 🔧 Mapeamento de Comandos CLI

### Atual (v0.5.1)

```bash
neo-smart-factory init
neo-smart-factory deploy
```

### Proposto (Futuro)

```bash
nxf init          # Comando principal
nxf deploy        # Comando principal
# ou
neo-smart-factory init    # Alias
neo-smart-factory deploy  # Alias
```

---

## 📁 Mapeamento de Estrutura GitHub

### Atual (v0.5.1)

```
github.com/kauntdewn1/neo_smart_factory
└── (monorepo)
    ├── forge-core/
    ├── forge-ui/
    ├── forge-cli/
    └── ...
```

### Proposto (Futuro)

```
github.com/neosmart-factory/
├── smart-core/
├── smart-ui/
├── smart-cli/
├── smart-oracle/
├── smart-cult/
├── smart-dna/
├── smart-kernel/
└── docs/
```

---

## ⚠️ Decisões Pendentes

### 1. Nomenclatura de Módulos

**Opção A**: Manter `forge-*` mesmo em multi-repo
- ✅ Consistência com estrutura atual
- ✅ Não causa breaking change
- ❌ Menos "limpo" que `smart-*`

**Opção B**: Migrar para `smart-*` no multi-repo
- ✅ Nomes mais curtos e claros
- ✅ Alinha com nome do projeto
- ❌ Requer renomeação completa

**Recomendação**: Decidir antes de iniciar migração.

---

### 2. Comando CLI

**Opção A**: Manter `neo-smart-factory`
- ✅ Consistente com nome do projeto
- ✅ Já padronizado
- ❌ Mais longo que `nxf`

**Opção B**: Migrar para `nxf` com alias
- ✅ Mais curto e rápido
- ✅ Pode manter `neo-smart-factory` como alias
- ❌ Requer mudança de hábito

**Recomendação**: Manter `neo-smart-factory` como principal, `nxf` como alias opcional.

---

### 3. NPM Scope

**Opção A**: Manter `neo-smart-factory-*`
- ✅ Consistente com nome do projeto
- ✅ Já padronizado
- ❌ Mais longo

**Opção B**: Migrar para `@neosmart/*`
- ✅ Mais curto e profissional
- ✅ Alinha com GitHub org
- ❌ Requer criação de org NPM

**Recomendação**: Migrar para `@neosmart/*` quando criar GitHub org.

---

## 📅 Timeline de Decisões

| Decisão | Prazo | Status |
|---------|-------|--------|
| Nomenclatura de módulos | Antes de v0.6.0 | ⏳ Pendente |
| Comando CLI (`nxf` vs `neo-smart-factory`) | Antes de v0.6.0 | ⏳ Pendente |
| NPM Scope (`@neosmart` vs `neo-smart-factory-*`) | Antes de migração | ⏳ Pendente |

---

## 📝 Notas

- Os documentos em `analise-conclusao/` são **propostas futuras**, não realidade atual
- A estrutura atual (`forge-*`, `neo-smart-factory`) está funcionando e padronizada
- Qualquer migração deve ser planejada cuidadosamente para evitar breaking changes
- Recomenda-se manter compatibilidade retroativa durante transição

---

**Última atualização**: 2024-01-01  
**Versão**: v0.5.1 — IGNIÇÃO

