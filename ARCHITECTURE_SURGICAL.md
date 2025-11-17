# Arquitetura Cirúrgica — NΞØ SMART FACTORY

> **Descrição cirúrgica do que cada bloco faz**

## 🎯 Visão Geral

A NΞØ SMART FACTORY é dividida em **5 blocos cirúrgicos**, cada um com função específica e bem definida.

---

## 1. `forge-core/` — O Motor Interno

**Função**: Motor interno da fábrica

**Conteúdo**:
```
forge-core/
├── contracts/          # Contratos inteligentes
│   ├── NeoTokenBase.sol      # Base purificada
│   ├── IgnitionToken.sol     # Token de ignição
│   └── ...
├── scripts/            # Scripts de deploy e operação
│   ├── deploy.js
│   ├── simulate.js
│   └── verify.js
├── test/               # Testes automatizados
│   └── ignition.test.js
├── templates/          # Templates reutilizáveis
│   ├── token.sol.template
│   └── manifest.template.md
├── hardhat.config.js   # Configuração Hardhat
└── package.json
```

**Responsabilidades**:
- ✅ Contratos base (NeoTokenBase, IgnitionToken)
- ✅ Scripts de deploy e verificação
- ✅ Testes automatizados
- ✅ Templates para geração
- ✅ Configuração Hardhat (Polygon-ready)

**Este é o bloco que você clona, purifica e padroniza.**

**Base Original**: https://github.com/Smart-Contracts-Solutions/erc20-token-generator

---

## 2. `forge-cli/` — O Ritual de Criação

**Função**: Interface e cérebro operacional

**Comandos**:
```bash
npx neo-smart-factory init      # Inicializar novo token
npx neo-smart-factory deploy    # Deploy de token
```

**Estrutura**:
```
forge-cli/
├── bin/
│   └── index.js         # Executável principal
├── commands/
│   ├── init.js          # Comando init
│   └── deploy.js        # Comando deploy
└── package.json
```

**Responsabilidades**:
- ✅ Interface de linha de comando
- ✅ Cérebro operacional (orquestra criação)
- ✅ Pipeline automatizador
- ✅ Validação de inputs
- ✅ Geração de configurações

**Fluxo**:
1. `init` → Cria estrutura do token
2. `deploy` → Executa deploy via Hardhat
3. Gera arquivos de configuração
4. Valida antes de executar

---

## 3. `forge-ui/` — Mini dApp Gerado Automaticamente

**Função**: Interface web gerada para cada token

**Quando você cria um token, a Forge gera**:
```
tokens/nome-do-token/
├── ui/
│   ├── landing/        # Mini landing page
│   ├── mint/           # Página de mint
│   └── info/           # Página de informações
```

**Estrutura Base**:
```
forge-ui/
├── landing/            # Landing page principal (React + Tailwind)
├── nuxt-app/           # PWA App (Nuxt.js)
│   ├── pages/
│   │   ├── index.vue   # Formulário de criação
│   │   ├── simulator.vue
│   │   └── preview.vue
│   └── components/
└── README.md
```

**Responsabilidades**:
- ✅ Landing page principal
- ✅ Formulário de criação de tokens
- ✅ Preview de tokens
- ✅ Simulador de ecossistemas
- ✅ Geração automática de UI por token

**É simples, MAS fundamental.**

---

## 4. `docs/` — Inteligência Armazenada

**Função**: Documentação e conhecimento

**Conteúdo**:
```
docs/
├── manifesto.md              # Visão e valores
├── architecture.md            # Arquitetura técnica
├── patch-v0.5.1.md          # Notas do patch
├── changelog.md              # Histórico de mudanças
├── BASE_REPOSITORY.md        # Base técnica
└── ARCHITECTURE_SURGICAL.md  # Este arquivo
```

**Responsabilidades**:
- ✅ Arquitetura documentada
- ✅ Visão e estratégia
- ✅ Etapas de desenvolvimento
- ✅ Especificações técnicas
- ✅ Integração futura com NΞØ Protocol

**É onde você documenta para não repetir trabalho.**

---

## 5. `tokens/` — Onde Cada Novo Token Vive

**Função**: Histórico vivo da fábrica

**Estrutura por Token**:
```
tokens/
└── nome-do-token/
    ├── contracts/           # Contratos do token
    ├── scripts/             # Scripts específicos
    ├── docs/                # Documentação do token
    ├── ui/                  # UI gerada (landing, mint, info)
    ├── manifesto.md         # Manifesto do token
    └── deploy-info.json     # Informações do deploy
```

**Responsabilidades**:
- ✅ Armazenar cada token criado
- ✅ Manter histórico completo
- ✅ Documentação por token
- ✅ UI gerada por token
- ✅ Informações de deploy

**É o histórico vivo da sua fábrica.**

---

## 🔄 Fluxo Completo de Criação

### Passo 1: Inicialização
```bash
npx neo-smart-factory init
```
- Cria estrutura em `tokens/nome-do-token/`
- Gera configurações
- Prepara templates

### Passo 2: Configuração
- Edita `.env` com dados do token
- Configura tokenômica
- Define narrativa

### Passo 3: Simulação
```bash
NEO::simulate NOME_DO_TOKEN
```
- Valida segurança
- Verifica tokenômica
- Simula 7 dias
- Gera veredito

### Passo 4: Deploy
```bash
npx neo-smart-factory deploy
```
- Deploy via `forge-core/scripts/deploy.js`
- Verificação automática
- Salvamento de informações

### Passo 5: Geração de UI
- Gera `tokens/nome-do-token/ui/`
- Landing page personalizada
- Página de mint
- Página de informações

---

## 🎯 Interdependências

```
forge-core/  →  Motor (base técnica)
     ↓
forge-cli/   →  Interface (orquestra criação)
     ↓
tokens/      →  Resultado (cada token criado)
     ↓
forge-ui/    →  Interface (UI gerada por token)
     ↓
docs/        →  Inteligência (documenta tudo)
```

---

## 📊 Resumo Cirúrgico

| Bloco | Função | Input | Output |
|-------|--------|-------|--------|
| `forge-core/` | Motor interno | Config | Contratos deployados |
| `forge-cli/` | Ritual de criação | Comandos | Estrutura de token |
| `forge-ui/` | Mini dApp | Token config | UI gerada |
| `docs/` | Inteligência | Conhecimento | Documentação |
| `tokens/` | Histórico | Token criado | Estrutura completa |

---

**Cada bloco tem função cirúrgica específica. Nenhum bloco faz o trabalho do outro.**

*NΞØ SMART FACTORY v0.5.1 — IGNIÇÃO*

