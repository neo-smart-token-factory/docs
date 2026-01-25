# 🗂️ Plano de Reorganização: docs → Repositórios Oficiais

**Data:** 2026-01-25  
**Objetivo:** Mover código de `temp_repos/` para repositórios oficiais e limpar `docs/`

---

## 🎯 SITUAÇÃO ATUAL

### Repositório `docs` (onde estamos)
**Propósito:** Documentação, padrões, arquitetura, ADRs
**Problema:** Contém código temporário em `temp_repos/` que deve estar em repositórios oficiais

### Repositórios Oficiais
- **smart-core:** Contratos e scripts (EVM + TON)
- **smart-ui:** Interface de usuário
- **smart-cli:** CLI tools
- **landing:** Landing page

---

## 📦 MAPEAMENTO: O QUE MOVER

### A. De `docs/temp_repos/smart-core/` → Repo oficial `smart-core`

#### Contratos TON (após validação)
```
docs/temp_repos/smart-core/contracts/ton/
├── NeoJettonFactoryV2.fc       → smart-core/contracts/ton/
├── NeoJettonMinter.fc          → smart-core/contracts/ton/
├── NeoJettonWallet.fc          → smart-core/contracts/ton/
└── opcodes.fc                  → smart-core/contracts/ton/
```

**Status:** ⚠️ **AGUARDANDO VALIDAÇÃO** - Bug ainda não resolvido

#### Scripts
```
docs/temp_repos/smart-core/scripts/
├── compile-ton-v2.js           → smart-core/scripts/
├── deploy-ton-factory-v2.js    → smart-core/scripts/
├── deploy-nsf-token.js         → smart-core/scripts/
├── debug-all-factories.js      → smart-core/scripts/debug/
├── debug-jetton-address.js     → smart-core/scripts/debug/
└── dry-run-ton.js              → smart-core/scripts/
```

**Status:** ✅ Scripts podem ser movidos (independem do bug)

#### Configuração
```
docs/temp_repos/smart-core/
├── .env.ton.example            → smart-core/ (merge com existente)
└── hardhat.config.js           → smart-core/ (verificar diferenças)
```

**Status:** ⚠️ Verificar diferenças antes de mover

### B. Outros Repositórios em `temp_repos/`

#### `smart-ui`
**Status:** 🔍 Verificar se há mudanças relevantes
**Ação:** Se houver mudanças, mover para repo oficial

#### `smart-cli`
**Status:** 🔍 Verificar se há mudanças relevantes
**Ação:** Se houver mudanças, mover para repo oficial

#### `landing`
**Status:** 🔍 Verificar se há mudanças relevantes
**Ação:** Se houver mudanças, mover para repo oficial

#### `internal-ops`
**Status:** ⚠️ Repositório privado
**Ação:** Mover para local apropriado (não público)

---

## 🧹 LIMPEZA DO REPOSITÓRIO `docs`

### Fase 1: Consolidar Documentação de Debug

#### Documentos de Sessão (consolidar)
```
docs/auditoria/
├── ANALISE_BUG_JETTON_MINTER.md           │
├── BUG_FACTORY_CORRIGIDO.md               │
├── RELATORIO_COMPLETO_BUG_JETTON_MINTER.md│ → Consolidar em:
├── SESSAO_2026-01-24_RESUMO.md            │   TON_FACTORY_COMPLETE_ANALYSIS.md
├── SESSAO_APRENDIZADO_TON_FACTORY.md      │
└── TON_FACTORY_REVISAO_TECNICA.md         │
```

**Ação:**
1. Criar `TON_FACTORY_COMPLETE_ANALYSIS.md` com:
   - Resumo executivo
   - Análise técnica consolidada
   - Solução encontrada
   - Referências aos documentos originais

2. Mover documentos detalhados para:
   ```
   docs/archive/ton-debug-sessions/2026-01-24-25/
   ├── 01-ANALISE_INICIAL.md
   ├── 02-BUG_IDENTIFICADO.md
   ├── 03-SESSAO_APRENDIZADO.md
   └── 04-CHECKPOINT_FINAL.md
   ```

#### Documentos Técnicos Permanentes (manter)
```
docs/auditoria/
├── EVM_TON_MAPPING.md              ✅ Manter
├── NOMENCLATURA_OFICIAL.md         ✅ Manter
├── TON_CHECKLIST_EXECUCAO.md       ✅ Manter
├── TON_DEPLOY_MAINNET_REPORT.md    ✅ Manter
├── TON_PLANO_IMPLEMENTACAO.md      ✅ Manter
├── TON_SUMARIO_EXECUTIVO.md        ✅ Manter
└── TON_INDEX.md                    ✅ Manter
```

### Fase 2: Remover `temp_repos/`

**Quando:** Após migrar mudanças para repositórios oficiais

```bash
# APÓS validação e migração:
rm -rf docs/temp_repos/
```

⚠️ **CUIDADO:** Verificar 2x antes de deletar!

### Fase 3: Atualizar `.gitignore`

Adicionar em `docs/.gitignore`:
```gitignore
# Repositórios temporários
temp_repos/
tmp/
*.tmp
```

---

## 📋 CHECKLIST DE MIGRAÇÃO

### Pré-Migração
- [ ] Verificar todos os arquivos em `temp_repos/`
- [ ] Identificar mudanças vs. versões oficiais
- [ ] Documentar diferenças críticas
- [ ] Fazer backup local (segurança)

### Migração `smart-core`
- [ ] Criar branch: `feature/ton-factory-v2`
- [ ] Mover contratos TON validados
- [ ] Mover scripts atualizados
- [ ] Criar pasta `scripts/debug/` para scripts de debug
- [ ] Atualizar `.env.ton.example` se necessário
- [ ] Atualizar README com instruções TON
- [ ] Testar compilação
- [ ] Testar deploy em testnet
- [ ] Abrir PR para review

### Migração Outros Repos (se aplicável)
- [ ] `smart-ui`: Verificar e mover mudanças
- [ ] `smart-cli`: Verificar e mover mudanças
- [ ] `landing`: Verificar e mover mudanças

### Limpeza `docs`
- [ ] Consolidar documentação de debug
- [ ] Criar `TON_FACTORY_COMPLETE_ANALYSIS.md`
- [ ] Mover sessões detalhadas para `archive/`
- [ ] Atualizar `TON_INDEX.md` com nova organização
- [ ] Verificar links quebrados
- [ ] Remover `temp_repos/` (após validação)
- [ ] Atualizar `.gitignore`
- [ ] Commit e push

### Pós-Migração
- [ ] Verificar todos os repositórios oficiais
- [ ] Testar builds em cada repo
- [ ] Atualizar documentação de contribuição
- [ ] Notificar equipe das mudanças

---

## 🗺️ ESTRUTURA FINAL DESEJADA

### Repositório `docs` (limpo)
```
docs/
├── .github/                    ← Workflows de validação
├── architecture/               ← Arquitetura e ADRs
│   ├── adr/
│   ├── specs/
│   └── nomenclature.md
├── auditoria/                  ← Análises consolidadas
│   ├── TON_FACTORY_COMPLETE_ANALYSIS.md  ← Novo documento principal
│   ├── TON_INDEX.md
│   └── ... (documentos permanentes)
├── archive/                    ← Histórico
│   └── ton-debug-sessions/     ← Sessões detalhadas arquivadas
│       └── 2026-01-24-25/
├── branding/                   ← Identidade visual
├── core/                       ← Conceitos fundamentais
├── ecosystem/                  ← Ecossistema
├── operations/                 ← Guias operacionais
├── registro/                   ← Propriedade intelectual
├── strategy/                   ← Estratégia de produto
├── INDEX.md
├── ORGANIZATION.md
└── README.md
```

### Repositório `smart-core` (atualizado)
```
smart-core/
├── contracts/
│   ├── ton/                    ← Contratos TON
│   │   ├── NeoJettonFactoryV2.fc
│   │   ├── NeoJettonMinter.fc
│   │   ├── NeoJettonWallet.fc
│   │   └── opcodes.fc
│   └── ... (contratos EVM)
├── scripts/
│   ├── ton/                    ← Scripts TON organizados
│   │   ├── compile-ton-v2.js
│   │   ├── deploy-ton-factory-v2.js
│   │   └── deploy-nsf-token.js
│   ├── debug/                  ← Scripts de debug
│   │   ├── debug-all-factories.js
│   │   └── debug-jetton-address.js
│   └── ... (scripts EVM)
├── .env.ton.example
├── hardhat.config.js
└── README.md                   ← Atualizado com instruções TON
```

---

## ⚠️ REGRAS DE SEGURANÇA

### Antes de Deletar `temp_repos/`

✅ **VERIFICAR:**
1. Todos os arquivos importantes foram migrados
2. Commits foram feitos nos repositórios oficiais
3. Testes passaram nos repositórios oficiais
4. Backup local foi feito (segurança extra)

❌ **NÃO DELETAR SE:**
- Houver arquivos não migrados
- Commits não foram feitos
- Testes falharam
- Há dúvidas sobre algum arquivo

### Proteção NEØ

**Lembrar:** Repositório `docs` tem arquitetura protegida.

✅ **PERMITIDO:**
- Adicionar documentos nas pastas existentes
- Modificar conteúdo de documentos
- Criar subpastas dentro das pastas aprovadas

❌ **NÃO PERMITIDO:**
- Modificar estrutura de pastas raiz
- Renomear pastas principais
- Reorganizar arquitetura sem autorização

---

## 📅 CRONOGRAMA SUGERIDO

### Fase 1: Validação (1-2 dias)
- Resolver bug TON Factory
- Validar contratos no testnet
- Testar scripts de deploy

### Fase 2: Migração (1 dia)
- Mover código para `smart-core`
- Criar PRs nos repos oficiais
- Review e merge

### Fase 3: Limpeza (meio dia)
- Consolidar documentação em `docs`
- Arquivar sessões de debug
- Remover `temp_repos/`

### Fase 4: Validação Final (meio dia)
- Verificar todos os repos
- Testar builds
- Atualizar documentação

---

## 🎯 PRÓXIMAS AÇÕES

### Segunda-feira (2026-01-26)
1. **Resolver bug TON Factory** (ver `CHECKPOINT_TON_FACTORY_2026-01-25.md`)
2. **Validar solução** no testnet
3. **Começar migração** se validação for bem-sucedida

### Terça-feira (2026-01-27)
1. **Migrar código** para `smart-core`
2. **Consolidar documentação**
3. **Limpar `docs/`**

### Quarta-feira (2026-01-28)
1. **Review final**
2. **Merge PRs**
3. **Atualizar documentação pública**

---

## 📚 REFERÊNCIAS

- **Checkpoint Técnico:** `CHECKPOINT_TON_FACTORY_2026-01-25.md`
- **Organização NEØ:** `ORGANIZATION.md`
- **Nomenclatura Oficial:** `auditoria/NOMENCLATURA_OFICIAL.md`

---

**Status:** 📋 Plano Definido  
**Próximo Passo:** Resolver bug TON Factory  
**Documento:** Referência para reorganização

---

*Plano criado por: Cursor AI Agent*  
*Data: 2026-01-25 (Sábado)*
