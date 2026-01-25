# Nomenclatura Oficial — NΞØ Smart Token Factory

**Data de Padronização**: 2026-01-24  
**Versão**: v0.5.3 (Multi-repo Ativo)  
**Status**: ✅ **OFICIAL E OBRIGATÓRIO**

---

## 🎯 Nomenclatura Correta

### Repositórios GitHub

**Organization**: [`neo-smart-token-factory`](https://github.com/neo-smart-token-factory)

| ✅ CORRETO | ❌ OBSOLETO | Status |
|------------|-------------|--------|
| `smart-core` | `forge-core` | 🟢 Ativo |
| `smart-ui` | `forge-ui` | 🟢 Ativo |
| `smart-cli` | `forge-cli` | 🟢 Ativo |
| `internal-ops` | N/A | 🟢 Ativo |
| `docs` | N/A | 🟢 Ativo |
| `smart-oracle` | `forge-oracle` | 🔨 Planejado (v0.6.0) |
| `smart-dna` | `forge-dna` | 🔨 Planejado (v0.6.0) |
| `smart-cult` | `forge-cult` | 🔨 Planejado (v0.7.0) |
| `smart-kernel` | `forge-kernel` | 🔨 Planejado (v0.8.0) |

---

## 📦 NPM Packages

**Organization**: `@neosmart`

| Package | Comando CLI | Descrição |
|---------|-------------|-----------|
| `@neosmart/core` | N/A | Contratos e scripts |
| `@neosmart/ui` | N/A | Componentes UI |
| `nxf` ou `@neosmart/cli` | `nxf` | CLI universal |
| `@neosmart/oracle` | N/A | Sistema LLM (futuro) |
| `@neosmart/dna` | N/A | Schema e validação (futuro) |
| `@neosmart/cult` | N/A | Narrativa (futuro) |
| `@neosmart/kernel` | N/A | Orquestrador (futuro) |

---

## 🏷️ Branding e Nomes

### Nome Completo
**NΞØ Smart Token Factory**

Variações aceitas:
- NΞØ SMART FACTORY
- neo-smart-token-factory (GitHub, lowercase)
- @neosmart (NPM, lowercase)

### Símbolo
**NΞØ** (com Epsilon grego `Ξ`)

Não usar:
- ❌ NEO (sem símbolo)
- ❌ NEØ (sem Epsilon)
- ❌ NEO (apenas maiúsculas sem símbolo)

---

## 🔧 CLI Universal

### Nome do Executável
**`nxf`** (NEO eXecution Framework)

Comandos principais:
```bash
nxf init          # Scaffold de projeto
nxf deploy        # Deploy multichain
nxf simulate      # Simulação de ecossistema
nxf verify        # Verificação em explorer
```

Não usar:
- ❌ `neo-smart-factory` (obsoleto)
- ❌ `forge` (obsoleto)
- ❌ `nsf` (nunca foi oficial)

---

## 📂 Estrutura de Diretórios

### Em Repositórios
```text
smart-core/
├── contracts/      # Contratos Solidity/FunC
├── scripts/        # Scripts de deploy
├── test/           # Testes automatizados
└── templates/      # Templates reutilizáveis

smart-ui/
├── components/     # Componentes React/Next.js
├── pages/          # Páginas da aplicação
├── public/         # Assets estáticos
└── styles/         # Design system

smart-cli/
├── bin/            # Executável nxf
├── commands/       # Comandos CLI
├── utils/          # Utilidades
└── templates/      # Templates de scaffold
```

---

## 🌐 URLs e Domínios

### Planejados
- `neosmart.factory` (principal)
- `docs.neosmart.factory` (documentação)
- `app.neosmart.factory` (aplicação web)
- `api.neosmart.factory` (API, se aplicável)

### GitHub
- `github.com/neo-smart-token-factory` (organization)
- `github.com/neo-smart-token-factory/smart-core`
- `github.com/neo-smart-token-factory/smart-ui`
- `github.com/neo-smart-token-factory/smart-cli`
- `github.com/neo-smart-token-factory/docs`

---

## 📝 Convenções de Código

### Contratos Solidity
```solidity
// ✅ CORRETO
contract NeoTokenV2 { }
contract ManualBridge { }

// ❌ ERRADO
contract ForgeToken { }
contract NeoFactory { }  // Usar NeoJettonFactory para TON
```

### Contratos TON (FunC)
```func
;; ✅ CORRETO
() NeoJettonFactory::deploy_jetton(...) { }
() NeoJettonMinter::mint(...) { }
() NeoJettonWallet::transfer(...) { }

;; ❌ ERRADO
() ForgeFactory::deploy(...) { }
```

### JavaScript/TypeScript
```typescript
// ✅ CORRETO
import { NeoTokenV2 } from '@neosmart/core';
import { deployMultichain } from '@neosmart/core/scripts';

// ❌ ERRADO
import { ForgeToken } from 'forge-core';
```

---

## 🗂️ Git Commits

### Prefixos Recomendados
```bash
feat:     Nova feature
fix:      Correção de bug
docs:     Documentação
refactor: Refatoração
test:     Testes
chore:    Manutenção
perf:     Performance
```

### Exemplos
```bash
# ✅ CORRETO
git commit -m "feat(smart-core): add TON jetton factory"
git commit -m "fix(smart-cli): correct nxf deploy command"
git commit -m "docs: update NOMENCLATURA_OFICIAL"

# ❌ ERRADO
git commit -m "feat(forge-core): new feature"
git commit -m "update stuff"
```

---

## 🚫 Nomenclatura OBSOLETA (Não Usar)

### Repositórios Obsoletos
- ❌ `forge-core`
- ❌ `forge-ui`
- ❌ `forge-cli`
- ❌ `forge-oracle`
- ❌ `forge-dna`
- ❌ `forge-cult`
- ❌ `forge-kernel`

### CLI Obsoleto
- ❌ `neo-smart-factory` (comando antigo)
- ❌ `forge` (nunca foi oficial)

### Organização Obsoleta
- ❌ `neo-forge-factory` (nunca existiu)
- ❌ Qualquer variação com "forge"

---

## ✅ Checklist de Conformidade

Ao criar novos documentos, código ou conteúdo:

- [ ] Usar `smart-*` para repositórios (não `forge-*`)
- [ ] Usar `nxf` para CLI (não `neo-smart-factory`)
- [ ] Usar `@neosmart` para NPM packages
- [ ] Usar `NΞØ` com Epsilon grego no branding
- [ ] Verificar links GitHub apontam para `neo-smart-token-factory` org
- [ ] Verificar imports usam `@neosmart` scoped packages
- [ ] Verificar documentação não tem referências obsoletas

---

## 🔍 Como Buscar Referências Obsoletas

```bash
# No repositório docs
cd "/Users/nettomello/CODIGOS/NEO SMART TOKEN/docs"

# Buscar referências obsoletas
grep -r "forge-cli" .
grep -r "forge-ui" .
grep -r "forge-core" .
grep -r "neo-smart-factory init" .  # CLI obsoleto

# Buscar em arquivo específico
grep "forge-" auditoria/factory-status.md
```

---

## 📊 Migração Histórica

### v0.5.0 e anteriores
- Nomenclatura `forge-*` era usada internamente
- CLI era `neo-smart-factory`
- Organização não estava pública

### v0.5.1 - v0.5.2
- Transição para nomenclatura `smart-*`
- CLI ainda era `neo-smart-factory`
- Organização criada: `neo-smart-token-factory`

### v0.5.3 (atual)
- ✅ Nomenclatura `smart-*` padronizada
- ✅ CLI unificada: `nxf`
- ✅ NPM organization: `@neosmart`
- ✅ Multi-repo ativo e público

---

## 📞 Responsabilidade

**Owner**: Mellø (Architecture Lead)

**Enforcement**:
- Code reviews devem verificar nomenclatura
- PRs com nomenclatura obsoleta devem ser rejeitados
- Documentação deve ser atualizada em batch se encontrado inconsistências

**Atualizações**:
- Este documento é a fonte única de verdade (SSOT)
- Mudanças requerem aprovação de Mellø
- Versão deve ser incrementada a cada update

---

## 🔄 Log de Mudanças

| Data | Versão | Mudança | Autor |
|------|--------|---------|-------|
| 2026-01-24 | 1.0 | Documento inicial criado | AI Agent + Mellø |
| 2026-01-24 | 1.0 | Padronização `smart-*` vs `forge-*` | AI Agent + Mellø |

---

**Status**: ✅ **OFICIAL E OBRIGATÓRIO**  
**Enforcement**: **IMEDIATO**  
**Última Atualização**: 2026-01-24  
**Versão do Documento**: 1.0

---

*NΞØ Smart Token Factory — Nomenclatura Oficial v1.0*
