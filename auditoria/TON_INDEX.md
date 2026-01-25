# Documentação TON — NEØ Smart Factory

**Status:** Implementação ativa  
**Última Atualização:** 2026-01-25

---

## 📚 Documentos Disponíveis

### 🎯 Padrões e Mapeamentos

**[EVM_TON_MAPPING.md](./EVM_TON_MAPPING.md)** ⭐⭐⭐  
*Mapeamento de paridade EVM ↔ TON*

- Comparação funcionalidade por funcionalidade
- NeoTokenV2.sol vs NeoJettonMinter.fc
- Storage equivalente
- Limitações conhecidas
- Checklist de conformidade
- **Uso:** Garantir paridade completa entre chains

**[NOMENCLATURA_OFICIAL.md](./NOMENCLATURA_OFICIAL.md)** ⭐  
*Padrão oficial de nomenclatura (SSOT)*

- `smart-*` (correto) vs `forge-*` (obsoleto)
- CLI: `nxf` (correto) vs `neo-smart-factory` (obsoleto)
- NPM organization: `@neosmart`
- Checklist de conformidade
- **Uso:** Referência obrigatória para novos documentos/código

### 📊 Status Atual

**[factory-status.md](./factory-status.md)**  
*Status geral da NΞØ Factory (EVM + TON)*

- Core funcional multichain
- Roadmap atual
- Métricas atuais
- Limitações conhecidas

---

## 🗂️ Código e Implementação

### Repositório smart-core

Todo o código TON está no repositório oficial:

**URL:** [github.com/neo-smart-token-factory/smart-core](https://github.com/neo-smart-token-factory/smart-core)

**Estrutura:**
```
smart-core/
├── contracts/ton/
│   ├── NeoJettonFactory.fc
│   ├── NeoJettonFactoryV2.fc
│   ├── NeoJettonMinter.fc
│   ├── NeoJettonWallet.fc
│   └── README.md (documentação técnica)
└── scripts/
    ├── compile-ton-v2.js
    ├── deploy-ton-factory-v2.js
    └── debug/ (ferramentas de debug)
```

**Branch ativa:** `feat/ton-factory-v2`

---

## 🔗 Links Úteis

### Documentação Oficial TON
- [TON Documentation](https://docs.ton.org)
- [TEP-74 (Jetton Standard)](https://github.com/ton-blockchain/TEPs/blob/master/text/0074-jettons-standard.md)
- [TEP-64 (Token Metadata)](https://github.com/ton-blockchain/TEPs/blob/master/text/0064-token-data-standard.md)
- [TonScan Testnet](https://testnet.tonscan.org)

### Repositórios NEØ
- [docs](https://github.com/neo-smart-token-factory/docs) - Este repositório
- [smart-core](https://github.com/neo-smart-token-factory/smart-core) - Contratos e scripts
- [smart-ui](https://github.com/neo-smart-token-factory/smart-ui) - Interface
- [landing](https://github.com/neo-smart-token-factory/landing) - Landing page

---

## 📝 Notas

- **Documentação técnica detalhada:** Ver `smart-core/contracts/ton/README.md`
- **Scripts e ferramentas:** Ver `smart-core/scripts/` e `smart-core/scripts/debug/`
- **Issues e bugs:** GitHub Issues em [smart-core](https://github.com/neo-smart-token-factory/smart-core/issues)
- **Roadmap e planejamento:** Ver `docs/strategy/`

---

**Versão:** 2.0 (Simplificada)  
**Princípio:** Menos é mais — apenas o essencial
