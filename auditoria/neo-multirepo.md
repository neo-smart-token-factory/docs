# 🚀 Plano de Migração Multi-Repo — NΞØ SMART FACTORY

> **Da estrutura monorepo atual para arquitetura modular**

---

## 🎯 Objetivo

Migrar de:
```
neo-smart-factory/  (monorepo atual)
```

Para:
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

## 📅 Timeline

### Fase 1: Preparação (Semana 1)
**Objetivo:** Organizar estrutura atual e preparar separação

- [ ] Criar GitHub Organization `neosmart-factory`
- [ ] Criar repositórios vazios (privados inicialmente)
- [ ] Definir estrutura de cada repo
- [ ] Preparar scripts de migração

### Fase 2: Separação Core (Semana 2)
**Objetivo:** Separar módulos funcionais

- [ ] Migrar `forge-core/` → `smart-core`
- [ ] Migrar `forge-ui/` → `smart-ui`
- [ ] Migrar `forge-cli/` → `smart-cli`
- [ ] Testar cada repo isoladamente

### Fase 3: NPM e Integração (Semana 3)
**Objetivo:** Publicar packages e integrar

- [ ] Configurar NPM organization `@neosmart`
- [ ] Publicar `@neosmart/core` v0.5.1
- [ ] Publicar `@neosmart/ui` v0.5.1
- [ ] Publicar `nxf` v0.5.1
- [ ] Atualizar dependências entre repos

### Fase 4: Novos Módulos (Semanas 4-8)
**Objetivo:** Criar módulos planejados

- [ ] Criar `smart-dna` (v0.6.0)
- [ ] Criar `smart-oracle` (v0.6.0)
- [ ] Criar `smart-cult` (v0.7.0)
- [ ] Criar `smart-kernel` (v0.8.0)

### Fase 5: Documentação e Lançamento (Semana 9)
**Objetivo:** Documentar e tornar público

- [ ] Migrar docs para `docs/`
- [ ] Configurar docs.neosmart.factory
- [ ] Tornar repositórios públicos
- [ ] Anunciar v1.0.0

---

## 🔧 Passos Detalhados

### 1. Criar GitHub Organization

```bash
# Via GitHub web
1. Ir em: github.com/organizations/new
2. Nome: neosmart-factory
3. Email: team@neosmart.factory
4. Tipo: Open Source (Free)
```

**Configurações:**
- ✅ Two-factor authentication obrigatório
- ✅ Base permissions: Read
- ✅ Member privileges: Can create repositories

---

### 2. Criar Repositórios

```bash
# Via GitHub CLI
gh auth login
gh org create neosmart-factory

# Criar repos
gh repo create neosmart-factory/smart-core --private
gh repo create neosmart-factory/smart-ui --private
gh repo create neosmart-factory/smart-cli --private
gh repo create neosmart-factory/smart-oracle --private
gh repo create neosmart-factory/smart-cult --private
gh repo create neosmart-factory/smart-dna --private
gh repo create neosmart-factory/smart-kernel --private
gh repo create neosmart-factory/docs --public
```

---

### 3. Migrar `forge-core` → `smart-core`

**Estrutura atual:**
```
neo-smart-factory/
└── forge-core/
    ├── contracts/
    ├── scripts/
    ├── test/
    ├── templates/
    └── hardhat.config.js
```

**Nova estrutura:**
```
smart-core/
├── contracts/
├── scripts/
├── test/
├── templates/
├── hardhat.config.js
├── package.json
├── README.md
├── CHANGELOG.md
└── .github/
    └── workflows/
        └── ci.yml
```

**Comandos:**
```bash
# 1. Criar novo repo local
mkdir smart-core
cd smart-core
git init

# 2. Copiar conteúdo
cp -r ../neo-smart-factory/forge-core/* .

# 3. Criar package.json
npm init -y
npm pkg set name="@neosmart/core"
npm pkg set version="0.5.1"
npm pkg set description="Smart contracts and deployment scripts for NΞØ SMART FACTORY"
npm pkg set repository="github:neosmart-factory/smart-core"
npm pkg set license="MIT"

# 4. Criar README.md
cat > README.md << 'EOF'
# 🔥 smart-core

Smart contracts and deployment scripts for NΞØ SMART FACTORY.

## Installation

```bash
npm install @neosmart/core
```

## Usage

See [documentation](https://docs.neosmart.factory).
EOF

# 5. Criar .gitignore
cat > .gitignore << 'EOF'
node_modules/
.env
.env.local
cache/
artifacts/
coverage/
typechain-types/
EOF

# 6. Commit e push
git add .
git commit -m "feat: initial commit - migrate from forge-core"
git remote add origin git@github.com:neosmart-factory/smart-core.git
git push -u origin main
```

---

### 4. Migrar `forge-ui` → `smart-ui`

**Estrutura atual:**
```
neo-smart-factory/
└── forge-ui/
    ├── landing/
    └── nuxt-app/
```

**Nova estrutura:**
```
smart-ui/
├── landing/              → React + Vite
├── nuxt-app/             → PWA Nuxt.js
├── shared/               → Componentes compartilhados
├── package.json          → Monorepo (Turborepo/pnpm)
├── README.md
└── .github/
    └── workflows/
        ├── landing-deploy.yml
        └── pwa-deploy.yml
```

**Comandos similares ao smart-core**

---

### 5. Migrar `forge-cli` → `smart-cli`

**Estrutura atual:**
```
neo-smart-factory/
└── forge-cli/
    └── commands/
```

**Nova estrutura:**
```
smart-cli/
├── bin/
│   └── nxf.js           → Executável
├── commands/
│   ├── init.js
│   ├── deploy.js
│   └── simulate.js
├── lib/
├── templates/
├── package.json
└── README.md
```

**package.json:**
```json
{
  "name": "nxf",
  "version": "0.5.1",
  "description": "CLI for NΞØ SMART FACTORY",
  "bin": {
    "nxf": "./bin/nxf.js",
    "neo-smart-factory": "./bin/nxf.js"
  },
  "keywords": ["cli", "blockchain", "polygon", "token", "factory"],
  "repository": "github:neosmart-factory/smart-cli"
}
```

---

### 6. Configurar NPM Organization

```bash
# 1. Criar org no NPM
npm login
npm org create neosmart

# 2. Publicar packages
cd smart-core
npm publish --access public

cd ../smart-ui
npm publish --access public

cd ../smart-cli
npm publish --access public
```

**Verificar:**
- https://npmjs.com/package/@neosmart/core
- https://npmjs.com/package/@neosmart/ui
- https://npmjs.com/package/nxf

---

### 7. Configurar CI/CD

**GitHub Actions para cada repo:**

**smart-core/.github/workflows/ci.yml:**
```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
      - run: npm ci
      - run: npm test
      - run: npm run coverage

  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npm run build
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{secrets.NPM_TOKEN}}
```

---

### 8. Criar Documentação

**docs/.vitepress/config.ts:**
```typescript
export default {
  title: 'NΞØ SMART FACTORY',
  description: 'Documentação oficial',
  
  themeConfig: {
    nav: [
      { text: 'Guide', link: '/guide/' },
      { text: 'API', link: '/api/' },
      { text: 'Architecture', link: '/architecture/' }
    ],
    
    sidebar: {
      '/guide/': [
        {
          text: 'Getting Started',
          items: [
            { text: 'Introduction', link: '/guide/' },
            { text: 'Quick Start', link: '/guide/quick-start' },
            { text: 'First Deploy', link: '/guide/first-deploy' }
          ]
        }
      ],
      
      '/api/': [
        {
          text: 'Packages',
          items: [
            { text: '@neosmart/core', link: '/api/core' },
            { text: '@neosmart/ui', link: '/api/ui' },
            { text: 'nxf CLI', link: '/api/cli' }
          ]
        }
      ]
    }
  }
}
```

---

## ✅ Checklist de Migração

### Preparação
- [ ] GitHub Organization criada
- [ ] Repos vazios criados
- [ ] NPM Organization criada
- [ ] Domínios configurados

### Repositórios Core
- [ ] `smart-core` migrado e testado
- [ ] `smart-ui` migrado e testado
- [ ] `smart-cli` migrado e testado
- [ ] Packages publicados no NPM

### Integração
- [ ] Dependencies entre repos configuradas
- [ ] CI/CD configurado
- [ ] Testes de integração passando

### Novos Módulos
- [ ] `smart-dna` criado (v0.6.0)
- [ ] `smart-oracle` criado (v0.6.0)
- [ ] `smart-cult` criado (v0.7.0)
- [ ] `smart-kernel` criado (v0.8.0)

### Documentação
- [ ] `docs/` migrado
- [ ] VitePress configurado
- [ ] docs.neosmart.factory online
- [ ] Todos os módulos documentados

### Público
- [ ] Repos públicos
- [ ] Anúncio no Twitter
- [ ] Post no Discord
- [ ] v1.0.0 lançado

---

## 🐛 Problemas Comuns e Soluções

### Problema 1: Dependencies Circulares

**Sintoma:** `smart-cli` depende de `smart-core`, que depende de `smart-cli`

**Solução:**
```bash
# Usar peer dependencies
# smart-cli/package.json
{
  "peerDependencies": {
    "@neosmart/core": "^0.5.0"
  }
}
```

### Problema 2: Versões Desalinhadas

**Sintoma:** `smart-kernel` requer versões incompatíveis

**Solução:**
```bash
# Usar ranges semver consistentes
# smart-kernel/package.json
{
  "dependencies": {
    "@neosmart/core": "^0.5.0",
    "@neosmart/oracle": "^0.6.0"
  }
}
```

### Problema 3: Monorepo Local para Dev

**Sintoma:** Difícil testar múltiplos repos simultaneamente

**Solução:**
```bash
# Usar npm link ou pnpm workspace
mkdir neosmart-workspace
cd neosmart-workspace

git clone git@github.com:neosmart-factory/smart-core.git
git clone git@github.com:neosmart-factory/smart-cli.git

cd smart-core && npm link
cd ../smart-cli && npm link @neosmart/core
```

---

## 📊 Métricas de Sucesso

### Técnicas
- [ ] 100% dos testes passando em cada repo
- [ ] Coverage > 80% em repos core
- [ ] CI/CD verde em todos os repos
- [ ] Packages publicados no NPM

### Documentação
- [ ] README completo em cada repo
- [ ] API docs gerada automaticamente
- [ ] Exemplos práticos em todos os módulos

### Comunidade
- [ ] 10+ stars no GitHub (primeiro mês)
- [ ] 50+ downloads NPM (primeira semana)
- [ ] 5+ contributors externos (3 meses)

---

## 🎓 Boas Práticas

### Commits
```bash
# Formato Conventional Commits
feat(core): add vesting support
fix(cli): resolve env loading
docs(oracle): update API reference
chore(deps): bump hardhat to v2.19
```

### Releases
```bash
# Usar semantic-release ou np
cd smart-core
npx np patch   # 0.5.1 -> 0.5.2
npx np minor   # 0.5.2 -> 0.6.0
npx np major   # 0.6.0 -> 1.0.0
```

### Changelogs
Cada repo mantém seu `CHANGELOG.md`:
```markdown
# Changelog

## [0.5.1] - 2024-11-17

### Added
- Initial release
- ERC20 contracts
- Deploy scripts

### Fixed
- Gas estimation bug
```

---

## 📞 Suporte Durante Migração

**Para dúvidas:**
- 💬 Discord: #migration-help
- 📧 Email: migration@neosmart.factory
- 🐙 GitHub Discussions

**Reuniões:**
- Segunda-feira: Planning (1h)
- Quarta-feira: Review (30min)
- Sexta-feira: Demo (1h)

---

*NΞØ SMART FACTORY — Plano de Migração v0.5.1*  
*Última atualização: 17 de Novembro de 2025*