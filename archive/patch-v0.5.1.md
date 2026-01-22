# Patch v0.5.1 — IGNIÇÃO

## Data: 2024-01-01

## Mudanças Principais

### Estrutura Reorganizada

- ✅ Criação de `forge-core/` — Núcleo Hardhat + Polygon
- ✅ Criação de `forge-ui/` — Interface web
- ✅ Criação de `forge-cli/` — Ferramenta CLI
- ✅ Criação de `docs/` — Documentação centralizada
- ✅ Criação de `tokens/` — Tokens criados

### Novos Componentes

#### forge-core
- Contrato `NeoTokenBase.sol` — Base purificada (do erc20-token-generator)
- Contrato `IgnitionToken.sol` — Token de ignição v0.5.1 (herda de NeoTokenBase)
- Scripts de deploy, verificação e simulação
- Configuração Polygon-ready
- Templates de contratos

#### forge-ui
- Formulário oficial de criação de tokens
- Preview de deploy
- Interface Next.js

#### forge-cli
- Comando `init` — Inicializar novo token
- Comando `deploy` — Deploy de tokens
- Interface interativa

### Melhorias

- Configuração Polygon completa
- Suporte a Amoy testnet
- Scripts de verificação automática
- Templates reutilizáveis
- Documentação reorganizada

## Breaking Changes

- Estrutura de pastas reorganizada
- Contratos movidos para `forge-core/contracts/`
- Scripts movidos para `forge-core/scripts/`

## Próximos Passos

- [ ] Expandir forge-ui com simulador visual
- [ ] Adicionar mais comandos ao CLI
- [ ] Criar testes completos
- [ ] Documentar casos de uso avançados

---

**Versão**: v0.5.1  
**Codename**: IGNIÇÃO  
**Status**: Production Ready

