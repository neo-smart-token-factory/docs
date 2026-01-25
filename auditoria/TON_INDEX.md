# Índice — Documentação TON Factory

**Criado**: 2026-01-24  
**Escopo**: Revisão completa e plano de implementação TON  
**Status**: ✅ Revisão completa | ⏸️ Aguardando aprovação

---

## 📚 Documentos Disponíveis

### 🎯 Início Rápido

**1. [TON_SUMARIO_EXECUTIVO.md](./TON_SUMARIO_EXECUTIVO.md)** ⭐  
*Leia este primeiro!*

- Overview executivo
- Score card (7.5/10)
- O que está completo vs faltando
- Recomendação e decisão
- **Tempo de leitura**: 5-7 minutos

---

### 📋 Planejamento

**2. [TON_CHECKLIST_EXECUCAO.md](./TON_CHECKLIST_EXECUCAO.md)**  
*Checklist dia-a-dia para execução*

- 60 dias de atividades (4 fases)
- Validation criteria por etapa
- Go/No-Go checkpoints
- Blocker tracking
- **Uso**: Acompanhamento diário do progresso

**3. [TON_PLANO_IMPLEMENTACAO.md](./TON_PLANO_IMPLEMENTACAO.md)**  

*Roadmap estratégico completo

- 4 fases detalhadas (Testing, Testnet, Audit, Mainnet)
- Casos de teste especificados
- Deployment procedures
- Success metrics
- Budget breakdown ($30k-$45k)
- **Uso**: Planejamento estratégico

---

### 🔍 Técnico Detalhado

**4. [TON_FACTORY_REVISAO_TECNICA.md](./TON_FACTORY_REVISAO_TECNICA.md)**  

*Análise técnica profunda dos contratos

- Arquitetura (Factory, Minter, Wallet)
- Storage layout completo
- Op-codes registry (12 operações)
- Security analysis
- Gas costs estimados
- Comparação EVM vs TON
- Limitações conhecidas
- Recomendações técnicas
- **Uso**: Referência técnica, code review

---

### 📜 Registros e Padrões

**5. [NOMENCLATURA_OFICIAL.md](./NOMENCLATURA_OFICIAL.md)** ⭐  
*Padrão oficial de nomenclatura (SSOT)*

- `smart-*` (correto) vs `forge-*` (obsoleto)
- CLI: `nxf` (correto) vs `neo-smart-factory` (obsoleto)
- NPM organization: `@neosmart`
- Checklist de conformidade
- **Uso**: Referência obrigatória para novos documentos/código

**6. [EVM_TON_MAPPING.md](./EVM_TON_MAPPING.md)** ⭐⭐⭐  
*Mapeamento de paridade EVM ↔ TON*

- Comparação funcionalidade por funcionalidade
- NeoTokenV2.sol vs NeoJettonMinter.fc
- Storage equivalente
- Limitações conhecidas
- Checklist de conformidade
- **Uso**: Garantir paridade completa entre chains

**7. [TON_DEPLOY_MAINNET_REPORT.md](./TON_DEPLOY_MAINNET_REPORT.md)** ⭐⭐⭐  
*Relatório oficial de deploy na TON Mainnet*

- Factory deployed e ativa
- Address: `EQAqoO4t8NKfjXQ1mEeBwqqjEON6zwECv-haaX__pGp_C2ZM`
- Validações completas
- Checklist de aprovação
- **Status: ✅ APROVADO & ATIVO**

**8. [factory-status.md](./factory-status.md)**  
*Status geral da NΞØ Factory (EVM + TON)*

- Core funcional multichain
- Roadmap v0.5.3 → v1.0
- Métricas atuais
- Limitações

**9. [NEO_TON_V1_IMPLEMENTATION.md](../registro/release/technical/NEO_TON_V1_IMPLEMENTATION.md)**  
*Registry oficial da implementação TON V1*

- Prior art documentation
- Commit: `69bfe6cc`
- Standards compliance (TEP-74/64/89)
- License: CC BY-NC-ND 4.0
- Build artifacts

---

### 🔍 Debug e Análise Técnica

**10. [SESSAO_APRENDIZADO_TON_FACTORY.md](./SESSAO_APRENDIZADO_TON_FACTORY.md)** ⭐⭐⭐ **IMPORTANTE!**  
*Sessão de aprendizado sobre bug na Factory*

- Análise do código oficial TON (109 bits)
- Diferença Factory vs Minter direto
- Hipóteses de root cause
- Próximos passos detalhados
- Recursos de aprendizado
- **Status: 🔍 Bug identificado, solução em andamento**

**11. [CHECKPOINT_TON_FACTORY_2026-01-25.md](./CHECKPOINT_TON_FACTORY_2026-01-25.md)** ⭐⭐⭐ **NOVO!**  
*Checkpoint para retomar trabalho*

- Descoberta crucial (109 bits confirmado)
- Hipóteses ativas
- 3 opções de próximos passos (A, B, C)
- Checklist completo para próxima sessão
- Mapeamento de migração código → repos oficiais
- **Uso: Retomar trabalho exatamente do ponto atual**

**12. [PLANO_REORGANIZACAO.md](./PLANO_REORGANIZACAO.md)** ⭐⭐ **NOVO!**  
*Plano de migração e limpeza do repositório*

- Mapeamento: temp_repos/ → repositórios oficiais
- Consolidação da documentação
- Checklist de migração
- Cronograma sugerido
- Regras de segurança
- **Uso: Guia para reorganização após validação**

---

## 🗺️ Fluxo de Leitura Recomendado

### Para Mellø (Decisão Estratégica)

```text
1. NOMENCLATURA_OFICIAL.md (2 min - validar padrão)
   ↓
2. TON_SUMARIO_EXECUTIVO.md (5 min)
   ↓
3. Decisão: Opção A, B, ou C?
   ↓
4. Se aprovado: Review TON_CHECKLIST_EXECUCAO.md (10 min)
```

### Para Dev Lead (Implementação)

```text
1. NOMENCLATURA_OFICIAL.md (padrão obrigatório)
   ↓
2. TON_SUMARIO_EXECUTIVO.md (overview)
   ↓
3. TON_FACTORY_REVISAO_TECNICA.md (deep dive)
   ↓
4. TON_PLANO_IMPLEMENTACAO.md (roadmap)
   ↓
5. TON_CHECKLIST_EXECUCAO.md (execution)
```

### Para QA/Security (Validação)

```text
1. TON_FACTORY_REVISAO_TECNICA.md (security section)
   ↓
2. TON_PLANO_IMPLEMENTACAO.md (test cases)
   ↓
3. TON_CHECKLIST_EXECUCAO.md (validation steps)
```

---

## 📊 Status por Documento

```text
================================================================
DOCUMENTO                           STATUS  DATA
================================================================
TON_SUMARIO_EXECUTIVO.md            ✅ OK   2026-01-24
TON_CHECKLIST_EXECUCAO.md           ✅ OK   2026-01-24
TON_PLANO_IMPLEMENTACAO.md          ✅ OK   2026-01-24
TON_FACTORY_REVISAO_TECNICA.md      ✅ OK   2026-01-24
TON_DEPLOY_MAINNET_REPORT.md        ✅ OK   2026-01-24
NOMENCLATURA_OFICIAL.md             ✅ OK   2026-01-24
EVM_TON_MAPPING.md                  ✅ OK   2026-01-24
factory-status.md                   ✅ ATU  2026-01-24
----------------------------------------------------------------
SESSAO_APRENDIZADO_TON_FACTORY.md   ✅ OK   2026-01-25
CHECKPOINT_TON_FACTORY_2026-01-25.md ✅ OK   2026-01-25
PLANO_REORGANIZACAO.md              ✅ OK   2026-01-25
TON_INDEX.md                        ✅ ATU  2026-01-25
================================================================
Owner: AI Agent
Last Update: 2026-01-25 (Debug Session)
================================================================
```

---

## 🎯 Próximos Passos

### 🔥 URGENTE: Resolver Bug Factory (2026-01-26)

**Status:** 🔍 Bug identificado, solução em andamento

**Ver:** [CHECKPOINT_TON_FACTORY_2026-01-25.md](./CHECKPOINT_TON_FACTORY_2026-01-25.md)

- [ ] Escolher estratégia (A, B ou C):
  - **A** 🏆 Usar TON Minter oficial primeiro (recomendado)
  - **B** ⚡ Factory minimalista (teste rápido)
  - **C** 🔍 Debug profundo (adicionar get methods)
- [ ] Validar solução no testnet
- [ ] Testar criação de Jetton Minter
- [ ] Documentar solução final

### Após Resolver Bug

**Ver:** [PLANO_REORGANIZACAO.md](./PLANO_REORGANIZACAO.md)

- [ ] Migrar código de `temp_repos/` → `smart-core` oficial
- [ ] Consolidar documentação de debug
- [ ] Limpar repositório `docs`
- [ ] Remover `temp_repos/` (após validação)
- [ ] Atualizar README dos repositórios oficiais

### Aguardando Decisão Estratégica

- [ ] Mellø review do sumário executivo
- [ ] Aprovar roadmap TON (Opção A/B/C)
- [ ] Aprovar budget (se Opção A)

---

## 📁 Estrutura de Diretórios

```text
docs/
└── auditoria/
    ├── TON_INDEX.md ← VOCÊ ESTÁ AQUI
    ├── TON_SUMARIO_EXECUTIVO.md
    ├── TON_CHECKLIST_EXECUCAO.md
    ├── TON_PLANO_IMPLEMENTACAO.md
    ├── TON_FACTORY_REVISAO_TECNICA.md
    ├── NOMENCLATURA_OFICIAL.md ← Padrão obrigatório
    └── factory-status.md

docs/registro/release/technical/
└── NEO_TON_V1_IMPLEMENTATION.md

(assumindo) smart-core/contracts/ton/
├── NeoJettonFactory.fc
├── NeoJettonMinter.fc
└── NeoJettonWallet.fc
```

---

## 🔗 Links Relacionados

### Internal

- [Architecture](../architecture/architecture.md)
- [Roadmap Tech](../strategy/roadmap-tech.md)
- [Prior Art Index](../registro/release/public/00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22.md)

### External

- [TON Documentation](https://docs.ton.org)
- [TEP-74 (Jetton Standard)](https://github.com/ton-blockchain/TEPs/blob/master/text/0074-jettons-standard.md)
- [TEP-64 (Token Metadata)](https://github.com/ton-blockchain/TEPs/blob/master/text/0064-token-data-standard.md)
- [TonScan Testnet](https://testnet.tonscan.org)

---

## 📝 Changelog

| Data | Versão | Mudança | Autor |
|------|--------|---------|-------|
| 2026-01-24 | 1.0 | Criação inicial | AI Agent |
| 2026-01-25 | 1.1 | Adicionados docs de debug session + checkpoint + plano reorganização | AI Agent |

---

## 📞 Suporte

**Questões sobre documentação**:

- GitHub Issues: [neo-smart-token-factory/docs](https://github.com/neo-smart-token-factory/docs/issues)
- Discord: #ton-implementation

**Questões técnicas**:

- Dev Team: [contact]
- Architecture: Mellø

---

**Última Atualização**: 2026-01-25  
**Versão do Índice**: 1.1  
**Status**: ✅ Completo e pronto para uso | 🔍 Debug session ativa
