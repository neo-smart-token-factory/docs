# Nomenclatura — Padrões e Convenções

> **Documento oficial de nomenclatura do projeto**

## 🎯 Nome do Projeto

### Nome Oficial (Visual/Marketing)
**NΞØ SMART FACTORY**

- Usado em: README, documentação pública, manifestos
- Caracteres especiais permitidos: NΞØ (com símbolo especial)

### Nome Técnico (Código/Repositório)
**neo-smart-factory**

- Usado em: Pastas, arquivos, repositório Git, npm packages
- Sem caracteres especiais
- Kebab-case (minúsculas com hífen)

---

## 📁 Estrutura de Diretórios

### Padrão Atual (Mantido)
```
neo-smart-factory/
├── forge-core/      # Núcleo (contratos + scripts)
├── forge-ui/        # Interface web
├── forge-cli/       # CLI tool
├── docs/            # Documentação
├── internal-ops/    # Sistema interno
└── tokens/          # Tokens criados
```

**Justificativa**: 
- `forge-*` é um prefixo técnico interno
- Não conflita com o nome do projeto
- Mantém consistência entre módulos
- Fácil de entender: "forge" = "forjar/criar"

---

## 📦 Nomes de Pacotes NPM

### Padrão
```
neo-smart-factory-{modulo}
```

**Exemplos**:
- `neo-smart-factory-core` (não `neo-forge-core`)
- `neo-smart-factory-ui` (não `neo-forge-ui`)
- `neo-smart-factory-cli` (não `neo-forge-cli`)

**Status Atual**: ❌ Inconsistente
- `neo-forge-core` → Deve ser `neo-smart-factory-core`
- `neo-forge-ui` → Deve ser `neo-smart-factory-ui`
- `neo-forge-cli` → Deve ser `neo-smart-factory-cli`

---

## 🔧 Comando CLI

### Padrão Oficial
```bash
neo-smart-factory {comando}
```

**Exemplos**:
```bash
neo-smart-factory init
neo-smart-factory deploy
neo-smart-factory simulate
```

**Status Atual**: ✅ Corrigido
- ✅ `neo-smart-factory` (padrão aplicado)

**Alternativa Curta** (opcional):
```bash
neo {comando}  # Alias para neo-smart-factory
```

---

## 📝 Convenções de Documentação

### Quando Usar Cada Nome

| Contexto | Nome a Usar |
|----------|-------------|
| Título de documento | **NΞØ SMART FACTORY** |
| Código/arquivos | `neo-smart-factory` |
| Pastas de módulos | `forge-core/`, `forge-ui/`, `forge-cli/` |
| Comandos CLI | `neo-smart-factory` |
| Pacotes npm | `neo-smart-factory-{modulo}` |
| Variáveis de código | `neoSmartFactory` ou `NeoSmartFactory` |

---

## ✅ Status de Nomenclatura

### 1. Comando CLI
- ✅ **Corrigido**: `neo-smart-factory` (padrão aplicado)
- ✅ Todos os arquivos atualizados

### 2. Nomes de Pacotes
- ✅ **Corrigido**: `neo-smart-factory-core`
- ✅ **Corrigido**: `neo-smart-factory-ui`
- ✅ **Corrigido**: `neo-smart-factory-cli`

### 3. Referências em Documentação
- ✅ Todas as referências principais corrigidas
- ℹ️ Arquivos históricos em `docs/auditoria/` mantêm referências antigas (documentação histórica)

---

## ✅ Padrão Final

### Estrutura
```
neo-smart-factory/           # Repositório
├── forge-core/              # Módulo core (mantém nome técnico)
├── forge-ui/                # Módulo UI (mantém nome técnico)
├── forge-cli/               # Módulo CLI (mantém nome técnico)
└── ...
```

### Comandos
```bash
neo-smart-factory init
neo-smart-factory deploy
```

### Pacotes NPM
```json
{
  "name": "neo-smart-factory-core",
  "name": "neo-smart-factory-ui",
  "name": "neo-smart-factory-cli"
}
```

### Documentação
- Títulos: **NΞØ SMART FACTORY**
- Código: `neo-smart-factory`
- Módulos: `forge-core/`, `forge-ui/`, `forge-cli/` (mantém)

---

## 🔄 Status de Correção

1. ✅ Manter `forge-*` nas pastas (mantido)
2. ✅ Corrigir comandos CLI: `mello-forge` → `neo-smart-factory` (CORRIGIDO)
3. ✅ Corrigir package.json: `neo-forge-*` → `neo-smart-factory-*` (CORRIGIDO)
4. ✅ Atualizar documentação com referências corretas (CORRIGIDO)

---

**Última atualização**: v0.5.1 — IGNIÇÃO  
**Status**: ✅ Todas as correções aplicadas

