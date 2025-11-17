# Índice da Documentação — NΞØ SMART FACTORY

> **Navegação rápida para toda a documentação do projeto**

---

## 📚 Documentação Principal

### Visão e Estratégia
- **[Manifesto](manifesto.md)** — Visão, valores e missão do projeto
- **[Changelog](changelog.md)** — Histórico completo de mudanças

### Arquitetura
- **[Arquitetura Técnica](architecture.md)** — Arquitetura técnica detalhada dos contratos
- **[Arquitetura Cirúrgica](ARCHITECTURE_SURGICAL.md)** — Descrição cirúrgica de cada bloco do sistema
- **[Base Repository](BASE_REPOSITORY.md)** — Base técnica purificada (erc20-token-generator)
- **[Nomenclatura](NOMENCLATURA.md)** — Padrões e convenções de nomenclatura

### Versões e Patches
- **[Patch v0.5.1 — IGNIÇÃO](patch-v0.5.1.md)** — Notas do patch de ignição

---

## 🔍 Auditoria e Histórico

### Auditoria
- **[Relatório de Auditoria](auditoria/RELATORIO_AUDITORIA.md)** — Comparação modelo inicial vs implementação atual
- **[Modelo Inicial Conceitual](auditoria/MODELO_INICIAL_CONCEITUAL.md)** — Modelo mental e visão inicial (brainstorm)
- **[Estrutura — Validação](auditoria/STRUCTURE_VALIDACAO.md)** — Checklist de validação da estrutura v0.5.1

---

## 🎯 Documentação por Módulo

### forge-core
- Ver `forge-core/README.md` (se existir)
- Contratos: `forge-core/contracts/`
- Scripts: `forge-core/scripts/`
- Testes: `forge-core/test/`

### forge-ui
- **[forge-ui/README.md](../forge-ui/README.md)** — Documentação da interface web
- Landing: `forge-ui/landing/README.md`
- Nuxt App: `forge-ui/nuxt-app/README.md`

### forge-cli
- Ver `forge-cli/package.json` para comandos
- Comandos: `forge-cli/commands/`

### internal-ops
- **[README](../internal-ops/README.md)** — Visão geral do sistema interno
- **[Comandos](../internal-ops/COMMANDS.md)** — Guia completo de comandos
- **[Uso](../internal-ops/USAGE.md)** — Como usar o sistema interno
- **[Simulador de Ecossistemas](../internal-ops/ECOSYSTEM_SIMULATOR.md)** — Documentação do simulador

### tokens
- **[README](../tokens/README.md)** — Estrutura e formato de tokens criados

---

## 🗂️ Estrutura de Documentação

```
docs/
├── INDEX.md                          ← Este arquivo
├── manifesto.md                      ← Visão e valores
├── architecture.md                   ← Arquitetura técnica
├── ARCHITECTURE_SURGICAL.md         ← Arquitetura cirúrgica
├── BASE_REPOSITORY.md               ← Base técnica
├── NOMENCLATURA.md                  ← Padrões de nomenclatura
├── patch-v0.5.1.md                  ← Patch notes
├── changelog.md                     ← Histórico
└── auditoria/
    ├── RELATORIO_AUDITORIA.md       ← Relatório de auditoria
    ├── INCONSISTENCIAS_NOMENCLATURA.md ← Inconsistências (resolvidas)
    ├── MODELO_INICIAL_CONCEITUAL.md ← Modelo inicial (brainstorm)
    └── STRUCTURE_VALIDACAO.md       ← Validação estrutura
```

---

## 🚀 Início Rápido

1. **Novo no projeto?** → Comece pelo [Manifesto](manifesto.md)
2. **Quer entender a arquitetura?** → Leia [Arquitetura Cirúrgica](ARCHITECTURE_SURGICAL.md)
3. **Quer ver o que mudou?** → Veja [Changelog](changelog.md)
4. **Quer entender a base técnica?** → Leia [Base Repository](BASE_REPOSITORY.md)
5. **Quer usar o sistema interno?** → Veja [Comandos](../internal-ops/COMMANDS.md)
6. **Quer entender nomenclatura?** → Veja [Nomenclatura](NOMENCLATURA.md)

---

## 📝 Convenções

- **Documentação principal**: `docs/*.md`
- **Auditoria/Histórico**: `docs/auditoria/*.md`
- **Documentação de módulos**: `{modulo}/README.md`
- **Templates**: `{modulo}/templates/*.md`

---

**Última atualização**: v0.5.1 — IGNIÇÃO  
**Mantido por**: NΞØ Protocol

