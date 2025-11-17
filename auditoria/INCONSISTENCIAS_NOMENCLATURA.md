# Inconsistências de Nomenclatura — Relatório

**Data**: 2024-01-01  
**Versão**: v0.5.1 — IGNIÇÃO  
**Status**: Análise Completa

---

## 🔍 Problemas Identificados (RESOLVIDOS)

### 1. Comando CLI — ✅ CORRIGIDO

**Estado Anterior**:
- `mello-forge` (binário em `forge-cli/bin/index.js`)
- `neo-forge` (mencionado no README.md linha 140-141)
- `mello-forge` (usado em vários arquivos de documentação)

**Padrão Aplicado**: `neo-smart-factory`

**Arquivos Corrigidos**:
- ✅ `forge-cli/bin/index.js` → `neo-smart-factory`
- ✅ `forge-cli/package.json` → `"neo-smart-factory": "./bin/index.js"`
- ✅ `README.md` → `neo-smart-factory init/deploy`
- ✅ `docs/ARCHITECTURE_SURGICAL.md` → `npx neo-smart-factory`
- ✅ `tokens/README.md` → `neo-smart-factory init`
- ✅ `forge-cli/commands/*.js` → `neo-smart-factory`

---

### 2. Nomes de Pacotes NPM — ✅ CORRIGIDO

**Estado Anterior**:
- `neo-forge-core` (`forge-core/package.json`)
- `neo-forge-ui` (`forge-ui/package.json`)
- `neo-forge-cli` (`forge-cli/package.json`)

**Padrão Aplicado**: `neo-smart-factory-{modulo}`

**Arquivos Corrigidos**:
- ✅ `forge-core/package.json` → `"name": "neo-smart-factory-core"`
- ✅ `forge-ui/package.json` → `"name": "neo-smart-factory-ui"`
- ✅ `forge-cli/package.json` → `"name": "neo-smart-factory-cli"`

---

### 3. Pastas de Módulos — CONSISTENTE ✅

**Status**: ✅ **CORRETO**

As pastas `forge-core/`, `forge-ui/`, `forge-cli/` estão corretas:
- São nomes técnicos internos
- Não conflitam com o nome do projeto
- Mantêm consistência entre módulos
- "forge" = verbo técnico (forjar/criar)

**Recomendação**: **MANTER** como está.

---

### 4. Referências em Documentação — PARCIALMENTE INCONSISTENTE

**Encontrado**:
- Alguns arquivos mencionam `mellø-protocol-factory` (histórico, OK)
- Alguns mencionam `neo-forge` ao invés de `neo-smart-factory`
- Alguns mencionam `mello-forge` ao invés de `neo-smart-factory`

**Arquivos Afetados**:
- `README.md` → Linha 140-141: `neo-forge`
- `docs/ARCHITECTURE_SURGICAL.md` → Linha 178: `npx mello-forge`
- `tokens/README.md` → `mello-forge init`
- `docs/auditoria/RELATORIO_AUDITORIA.md` → Várias referências

---

## 📊 Resumo de Inconsistências

| Item | Anterior | Corrigido | Status |
|------|----------|-----------|--------|
| **Comando CLI** | `mello-forge` / `neo-forge` | `neo-smart-factory` | ✅ Corrigido |
| **Pacote Core** | `neo-forge-core` | `neo-smart-factory-core` | ✅ Corrigido |
| **Pacote UI** | `neo-forge-ui` | `neo-smart-factory-ui` | ✅ Corrigido |
| **Pacote CLI** | `neo-forge-cli` | `neo-smart-factory-cli` | ✅ Corrigido |
| **Pastas** | `forge-*` | `forge-*` | ✅ Mantido (correto) |

---

## ✅ Padrão Proposto

### Estrutura de Pastas (MANTER)
```
neo-smart-factory/
├── forge-core/      ✅ Mantém (nome técnico interno)
├── forge-ui/        ✅ Mantém (nome técnico interno)
├── forge-cli/       ✅ Mantém (nome técnico interno)
└── ...
```

**Justificativa**: 
- `forge-*` é prefixo técnico interno
- Não precisa mudar
- Não causa confusão (é claro que são módulos internos)

### Comando CLI (CORRIGIR)
```bash
neo-smart-factory init
neo-smart-factory deploy
```

**Alternativa Curta** (opcional):
```bash
neo init      # Alias
neo deploy    # Alias
```

### Pacotes NPM (CORRIGIR)
```json
{
  "name": "neo-smart-factory-core",
  "name": "neo-smart-factory-ui",
  "name": "neo-smart-factory-cli"
}
```

---

## ✅ Correções Aplicadas

### Status: TODAS AS CORREÇÕES APLICADAS

1. ✅ **Comando CLI Corrigido**
   - ✅ `forge-cli/bin/index.js` → `neo-smart-factory`
   - ✅ `forge-cli/package.json` → `"neo-smart-factory": "./bin/index.js"`
   - ✅ Todos os arquivos de documentação atualizados

2. ✅ **Nomes de Pacotes Corrigidos**
   - ✅ `forge-core/package.json` → `neo-smart-factory-core`
   - ✅ `forge-ui/package.json` → `neo-smart-factory-ui`
   - ✅ `forge-cli/package.json` → `neo-smart-factory-cli`

3. ✅ **Documentação Atualizada**
   - ✅ `README.md` → Referências corrigidas
   - ✅ `docs/ARCHITECTURE_SURGICAL.md` → Comandos corrigidos
   - ✅ `tokens/README.md` → Comandos corrigidos
   - ✅ `docs/auditoria/RELATORIO_AUDITORIA.md` → Referências corrigidas
   - ✅ Outros arquivos de documentação atualizados

### Pendente (Opcional)

4. **Criar Alias Curto** (opcional, futuro)
   - Adicionar `neo` como alias para `neo-smart-factory`

---

## ⚠️ Considerações

### Manter `forge-*` nas Pastas?

**✅ SIM** — Recomendado manter porque:
- É nome técnico interno
- Não conflita com nome do projeto
- Mantém consistência entre módulos
- "forge" é verbo técnico claro (forjar/criar)
- Mudar causaria breaking change desnecessário

### Mudar Comando CLI?

**✅ SIM** — Deve ser `neo-smart-factory` porque:
- Alinha com nome do projeto
- Evita confusão (`mello-forge` não tem relação clara)
- Mais profissional e consistente

### Mudar Nomes de Pacotes?

**✅ SIM** — Deve ser `neo-smart-factory-*` porque:
- Alinha com nome do projeto
- Consistência total
- Evita confusão entre "forge" e "smart-factory"

---

## 📝 Decisão Final — APLICADA

### MANTER
- ✅ Pastas: `forge-core/`, `forge-ui/`, `forge-cli/` (mantidas)

### CORRIGIDO
- ✅ Comando CLI: `mello-forge` → `neo-smart-factory` (CORRIGIDO)
- ✅ Pacotes NPM: `neo-forge-*` → `neo-smart-factory-*` (CORRIGIDO)
- ✅ Documentação: Todas as referências inconsistentes (CORRIGIDAS)

---

**Status**: ✅ Todas as correções aplicadas  
**Data de Correção**: 2024-01-01  
**Versão**: v0.5.1 — IGNIÇÃO

