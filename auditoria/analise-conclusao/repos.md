# 📁 Repositórios Oficiais — NΞØ SMART FACTORY

> **⚠️ DOCUMENTO DE PLANEJAMENTO FUTURO**  
> Este documento descreve o **catálogo de repositórios multi-repo planejado** para versões futuras.  
> **Estrutura atual (v0.5.1)**: Monorepo único (`neo-smart-factory`)  
> **Veja**: [Nomenclatura](../../NOMENCLATURA.md) para estrutura atual | [Plano de Migração](plano-migr.md) para execução

---

## 🎯 Catálogo do Ecossistema Modular (Proposta Futura)

---

## 🎯 Visão Geral

A NΞØ SMART FACTORY é composta por **8 repositórios independentes**, cada um com sua responsabilidade específica.

Você pode usar:
- **Um módulo isolado** (ex: apenas `smart-core` para contratos)
- **Conjunto de módulos** (ex: `smart-cli` + `smart-core` para deploy)
- **Sistema completo** (via `smart-kernel` quando disponível)

---

## 📦 Repositórios Core

### 🔥 smart-core

**Contratos inteligentes, scripts de deploy, templates**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/smart-core`](https://github.com/neo-smart-token-factory/smart-core) |
| **NPM** | [`@neosmart/core`](https://npmjs.com/package/@neosmart/core) |
| **Versão** | v0.5.1 |
| **Status** | ✅ Ativo |
| **Linguagem** | Solidity, JavaScript |
| **Licença** | MIT |

**Features:**
- ✅ Contratos ERC20 base
- ✅ Deploy automatizado (Polygon)
- ✅ Verificação no Polygonscan
- ✅ Templates customizáveis
- ✅ Testes unitários

**Instalação:**
```bash
npm install @neosmart/core
```

**Uso:**
```bash
git clone https://github.com/neo-smart-token-factory/smart-core.git
cd smart-core
npm install
npm run deploy:polygon
```

**Dependências:**
- Hardhat
- OpenZeppelin
- Ethers.js

---

### 🎨 smart-ui

**Interface visual, PWA, landing page**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/smart-ui`](https://github.com/neo-smart-token-factory/smart-ui) |
| **NPM** | [`@neosmart/ui`](https://npmjs.com/package/@neosmart/ui) |
| **Versão** | v0.5.1 |
| **Status** | ✅ Ativo |
| **Linguagem** | Vue.js, React, TypeScript |
| **Licença** | MIT |

**Features:**
- ✅ Landing page (React + Vite)
- ✅ PWA App (Nuxt.js)
- ✅ Formulário de criação
- ✅ Preview de tokens
- ✅ Simulador básico

**Live Demo:**
- Landing: [neosmart.factory](https://neosmart.factory)
- PWA: [app.neosmart.factory](https://app.neosmart.factory)

**Instalação:**
```bash
npm install @neosmart/ui
```

**Uso:**
```bash
git clone https://github.com/neo-smart-token-factory/smart-ui.git
cd smart-ui/landing
npm install
npm run dev
```

**Dependências:**
- Vue.js / React
- Nuxt.js
- Tailwind CSS
- Vite

---

### ⚡ smart-cli

**CLI universal (nxf)**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/smart-cli`](https://github.com/neo-smart-token-factory/smart-cli) |
| **NPM** | [`nxf`](https://npmjs.com/package/nxf) ou [`@neosmart/cli`](https://npmjs.com/package/@neosmart/cli) |
| **Versão** | v0.5.1 |
| **Status** | ✅ Ativo |
| **Linguagem** | JavaScript/TypeScript |
| **Licença** | MIT |

**Features:**
- ✅ `nxf init` — Cria estrutura
- ✅ `nxf deploy` — Deploy automático
- ✅ `nxf simulate` — Validação pré-deploy
- ✅ `nxf status` — Status do projeto

**Instalação:**
```bash
npm install -g nxf
```

**Uso:**
```bash
nxf init meu-token
cd tokens/meu-token
nxf deploy
```

**Dependências:**
- Commander.js
- Inquirer
- Chalk

---

## 🧠 Repositórios de Inteligência

### 🔮 smart-oracle

**Sistema de refinamento via LLM**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/smart-oracle`](https://github.com/neo-smart-token-factory/smart-oracle) |
| **NPM** | [`@neosmart/oracle`](https://npmjs.com/package/@neosmart/oracle) |
| **Versão** | v0.6.0 (planejado) |
| **Status** | 🔨 Em desenvolvimento |
| **Linguagem** | TypeScript |
| **Licença** | MIT |

**Features Planejadas:**
- 🔨 Questionamento inteligente
- 🔨 Refinamento de DNA via GPT-4
- 🔨 Heurísticas de antifragilidade
- 🔨 Detecção de pontos cegos
- 🔨 Sugestões contextuais

**Previsão:** Fevereiro 2025

**API Planejada:**
```typescript
import { Oracle } from '@neosmart/oracle'

const oracle = new Oracle({ provider: 'gpt-4' })
const refined = await oracle.refine(dna)
```

**Dependências:**
- OpenAI SDK
- Anthropic SDK
- Zod (validação)

---

### 📖 smart-cult

**Geração de narrativa e documentos**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/smart-cult`](https://github.com/neo-smart-token-factory/smart-cult) |
| **NPM** | [`@neosmart/cult`](https://npmjs.com/package/@neosmart/cult) |
| **Versão** | v0.7.0 (planejado) |
| **Status** | 🔨 Em desenvolvimento |
| **Linguagem** | TypeScript |
| **Licença** | MIT |

**Features Planejadas:**
- 🔨 Geração de Manifesto
- 🔨 Geração de Whitepaper
- 🔨 Geração de Pitch Deck
- 🔨 Rituais de comunidade
- 🔨 Conteúdo de marketing

**Previsão:** Março 2025

**API Planejada:**
```typescript
import { Cult } from '@neosmart/cult'

const cult = new Cult()
const manifesto = await cult.generateManifesto(dna)
const whitepaper = await cult.generateWhitepaper(dna)
```

**Dependências:**
- Template engines
- LLM SDKs
- Markdown processors

---

## 📊 Repositórios de Dados

### 🧬 smart-dna

**Schema JSON, validação, templates**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/smart-dna`](https://github.com/neo-smart-token-factory/smart-dna) |
| **NPM** | [`@neosmart/dna`](https://npmjs.com/package/@neosmart/dna) |
| **Versão** | v0.6.0 (planejado) |
| **Status** | 🔨 Em desenvolvimento |
| **Linguagem** | TypeScript, JSON Schema |
| **Licença** | MIT |

**Features Planejadas:**
- 🔨 Schema completo do DNA
- 🔨 Validação via Zod
- 🔨 Templates (minimal, complete)
- 🔨 Exemplos práticos
- 🔨 Type definitions (TypeScript)

**Previsão:** Fevereiro 2025

**API Planejada:**
```typescript
import { DNA } from '@neosmart/dna'

const dna = DNA.parse(jsonData)
const isValid = DNA.validate(dna)
const template = DNA.templates.minimal
```

**Dependências:**
- Zod
- JSON Schema
- AJV

---

## 🎛️ Repositórios de Orquestração

### 🎛️ smart-kernel

**Orquestrador central, pipeline completo**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/smart-kernel`](https://github.com/neo-smart-token-factory/smart-kernel) |
| **NPM** | [`@neosmart/kernel`](https://npmjs.com/package/@neosmart/kernel) |
| **Versão** | v0.8.0 (planejado) |
| **Status** | 🔜 Planejado |
| **Linguagem** | TypeScript |
| **Licença** | MIT |

**Features Planejadas:**
- 🔜 Pipeline completo automatizado
- 🔜 "One-click deployment"
- 🔜 Orquestração de módulos
- 🔜 Workflows customizáveis
- 🔜 Monitoramento

**Previsão:** Abril 2025

**API Planejada:**
```typescript
import { Kernel } from '@neosmart/kernel'

const kernel = new Kernel()
await kernel.forge({
  dna: './token.json',
  mode: 'oneclick',
  network: 'polygon'
})
```

**Dependências:**
- Todos os módulos acima
- Workflow engines

---

## 📚 Repositórios de Documentação

### 📚 docs

**Documentação centralizada do ecossistema**

| | |
|---|---|
| **GitHub** | [`neo-smart-token-factory/docs`](https://github.com/neo-smart-token-factory/docs) |
| **URL** | [docs.neosmart.factory](https://docs.neosmart.factory) |
| **Versão** | v0.5.1 |
| **Status** | ✅ Ativo |
| **Tecnologia** | VitePress / Docusaurus |
| **Licença** | CC BY 4.0 |

**Conteúdo:**
- ✅ Getting Started
- ✅ Guias de uso
- ✅ Referência de API
- ✅ Arquitetura
- ✅ FAQs
- ✅ Exemplos

**Instalação:**
```bash
git clone https://github.com/neo-smart-token-factory/docs.git
cd docs
npm install
npm run dev
```

**Dependências:**
- VitePress
- Markdown

---

## 🛠️ Scripts Auxiliares

### Clonar Todos os Repositórios

**Script automático (futuro):**
```bash
npx nxf clone-all
```

**Manual (agora):**
```bash
# Core
git clone https://github.com/neo-smart-token-factory/smart-core.git
git clone https://github.com/neo-smart-token-factory/smart-ui.git
git clone https://github.com/neo-smart-token-factory/smart-cli.git

# Intelligence (quando disponível)
git clone https://github.com/neo-smart-token-factory/smart-oracle.git
git clone https://github.com/neo-smart-token-factory/smart-cult.git

# Data & Orchestration (quando disponível)
git clone https://github.com/neo-smart-token-factory/smart-dna.git
git clone https://github.com/neo-smart-token-factory/smart-kernel.git

# Docs
git clone https://github.com/neo-smart-token-factory/docs.git
```

---

## 📊 Status Dashboard

| Repositório | Versão | Status | Testes | Coverage | Issues Abertas |
|-------------|--------|--------|--------|----------|----------------|
| smart-core | v0.5.1 | ✅ | ✅ Passando | 85% | 3 |
| smart-ui | v0.5.1 | ✅ | ✅ Passando | 70% | 5 |
| smart-cli | v0.5.1 | ✅ | ✅ Passando | 90% | 2 |
| smart-oracle | - | 🔨 | - | - | - |
| smart-cult | - | 🔨 | - | - | - |
| smart-dna | - | 🔨 | - | - | - |
| smart-kernel | - | 🔜 | - | - | - |
| docs | v0.5.1 | ✅ | N/A | N/A | 1 |

---

## 🔗 Links Rápidos

### GitHub Organization
🐙 [github.com/neo-smart-token-factory](https://github.com/neo-smart-token-factory)

### NPM Organization
📦 [npmjs.com/org/neosmart](https://npmjs.com/org/neosmart)

### Websites
- 🌐 [neosmart.factory](https://neosmart.factory) — Landing
- 📱 [app.neosmart.factory](https://app.neosmart.factory) — PWA
- 📚 [docs.neosmart.factory](https://docs.neosmart.factory) — Docs

### Comunidade
- 💬 [Discord](https://discord.gg/neosmart)
- 🐦 [Twitter/X](https://twitter.com/neosmart_factory)
- 💼 [LinkedIn](https://linkedin.com/company/neo-smart-token-factory)

---

## 🤝 Contribuindo

Cada repositório tem seu próprio `CONTRIBUTING.md`, mas o fluxo geral é:

1. **Fork** o repositório
2. **Clone** seu fork
3. **Crie branch**: `git checkout -b feature/minha-feature`
4. **Commit**: `git commit -m 'feat: adiciona minha feature'`
5. **Push**: `git push origin feature/minha-feature`
6. **Pull Request** no GitHub

**Leia mais:**
- [CONTRIBUTING.md](./CONTRIBUTING.md)
- [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)

---

## 📞 Contato

**Geral:**
- 📧 team@neosmart.factory

**Repositórios específicos:**
- smart-core: core@neosmart.factory
- smart-oracle: oracle@neosmart.factory
- Documentação: docs@neosmart.factory

**Reportar bugs/vulnerabilidades:**
- 🔒 security@neosmart.factory

---

## 📈 Roadmap

### Q4 2024
- [x] Separar `smart-core`
- [x] Separar `smart-ui`
- [x] Separar `smart-cli`
- [ ] Publicar no NPM

### Q1 2025
- [ ] Criar `smart-oracle` (v0.6.0)
- [ ] Expandir `smart-dna` (v0.6.0)
- [ ] Criar `smart-cult` (v0.7.0)

### Q2 2025
- [ ] Criar `smart-kernel` (v0.8.0)
- [ ] Lançar v1.0.0 (sistema completo)

---

## ⚖️ Licenças

**Código:**
- MIT License (todos os repositórios)

**Documentação:**
- CC BY 4.0 (Creative Commons)

**Marca:**
- NΞØ SMART FACTORY™ é marca registrada

---

*NΞØ SMART FACTORY — Catálogo de Repositórios v0.5.1*  
*Última atualização: 17 de Novembro de 2025*