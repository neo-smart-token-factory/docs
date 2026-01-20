# Changelog

Todas as mudanças notáveis neste projeto serão documentadas neste arquivo.

---

## 🛣️ Roadmap — Transparência Radical

> **Status**: v0.5.1 — IGNIÇÃO (Base sólida, expansão necessária)  
> **Filosofia**: Transparência total sobre o que funciona, o que está em desenvolvimento e o que vem a seguir.

### Versões Planejadas

| Versão | Nome | Tema | Entrega Estimada | Status |
|--------|------|------|-----------------|--------|
| **v0.6.0** | **ORÁCULO** | Inteligência e refinamento | **Fev 2025** | 🔨 Em planejamento |
| **v0.7.0** | **CULT** | Narrativa e documentos | **Mar 2025** | 📋 Planejado |
| **v0.8.0** | **KERNEL** | Automação total | **Abr 2025** | 📋 Planejado |
| **v1.0.0** | **IGNIÇÃO COMPLETA** | Sistema coeso | **Q2 2025** | 🎯 Objetivo |

---

### v0.6.0 — ORÁCULO (Fev 2025)

**Foco**: Inteligência e refinamento

**O que será entregue**:
- ✅ `forge-oracle/` — Sistema de questionamento inteligente
  - Integração com LLM (GPT-4/Claude)
  - Heurísticas de antifragilidade
  - Árvore de decisão para refinamento
  - Questionamento interativo pré-deploy
- ✅ `forge-dna/` completo — Schema avançado
  - Campos `archetype`, `energy`, `ecosystem`
  - Configuração de `infrastructure`
  - Flags `extras` (marketplace, landing, etc.)
  - Validação completa de DNA

**Por que é importante**:  
O Oracle eleva a qualidade dos tokens criados, identificando pontos cegos e fortalecendo a arquitetura antes do deploy.

---

### v0.7.0 — CULT (Mar 2025)

**Foco**: Narrativa e documentos

**O que será entregue**:
- ✅ `forge-cult/` — Geração automática de documentos
  - Gerador de manifesto
  - Gerador de whitepaper
  - Gerador de pitch deck
  - Templates de narrativa
- ✅ Expansão do sistema de rituais
  - Configuração de rituais por token
  - Templates de rituais de comunidade

**Por que é importante**:  
Cada token precisa de narrativa forte. O CULT automatiza a criação de documentos essenciais.

---

### v0.8.0 — KERNEL (Abr 2025)

**Foco**: Automação total

**O que será entregue**:
- ✅ Kernel TypeScript — Pipeline automatizado
  - Script `forge.ts` que orquestra tudo
  - Integração entre todos os módulos
  - Deploy one-click completo
  - Geração automática de UI por token
- ✅ Separação de `forge-deployer/`
  - Módulo dedicado de deploy
  - Pipeline ritualizado

**Por que é importante**:  
O Kernel transforma a experiência de "vários comandos" para "um clique, um ecossistema completo".

---

### v1.0.0 — IGNIÇÃO COMPLETA (Q2 2025)

**Foco**: Sistema coeso e completo

**O que será entregue**:
- ✅ Todos os módulos integrados
- ✅ Pipeline completo automatizado
- ✅ Documentação completa
- ✅ Testes end-to-end
- ✅ Performance otimizada

**Por que é importante**:  
A versão 1.0 representa o cumprimento completo do manifesto: uma fábrica descentralizada completa e funcional.

---

## 📋 Histórico de Versões

### [0.5.3] - 2026-01-20 — MULTICHAIN FOUNDATION

**Status**: ✅ Implementado — Arquitetura Multichain & AA-Ready

#### Adicionado
- **NeoTokenV2.sol** — Evolução do NeoTokenBase para o ecossistema moderno
  - ✅ **ERC20Permit (EIP-2612)**: Transações gasless via assinaturas off-chain
  - ✅ **Bridge Minter Role**: Sistema autorizado para mint cross-chain
  - ✅ **Supply Cap Imutável**: `MAX_SUPPLY` constante de 1 bilhão de tokens
  - ✅ **Anti-bot Integrado**: Mapping `hasPublicMinted` (1 mint por wallet)
  - ✅ **Eventos Completos**: `PublicMinted(minter, amount, pricePaid)` e `BridgeMinted(to, amount)`
  - ✅ **View Function**: `getContractInfo()` retorna status completo do contrato
  - ✅ **Função de Emergência**: `resetPublicMint(address)` para casos edge

#### Melhorado
- **Segurança do `withdraw()`**: Migrado de `transfer()` para `call{}` (padrão moderno)
- **Validações Reforçadas**: Zero address checks em `bridgeMint()` e `setBridgeMinter()`
- **Documentação Inline**: NatSpec completo em todas as funções públicas
- **Mensagens de Erro**: Strings descritivas para melhor debugging

#### Arquitetura
- **Account Abstraction Ready**: Suporte nativo para Smart Wallets (Coinbase, Safe, Argent)
- **Multichain Ready**: Preparado para LayerZero, Wormhole, Axelar
- **Indexação Otimizada**: Eventos estruturados para The Graph e Dune Analytics
- **Frontend-Friendly**: `getContractInfo()` simplifica integração com dApps

#### Compatibilidade
- OpenZeppelin Contracts v5.0
- Solidity ^0.8.20
- EVM-compatible chains (Ethereum, Polygon, Base, Arbitrum, Optimism)

#### Decisões Técnicas
- Ver `docs/DECISION_LOG.md` → ADR-004 para justificativa completa
- Ver `docs/NEOTOKENV2.md` para documentação técnica detalhada

---

### [0.5.1] - 2024-01-01 — IGNIÇÃO

**Status**: ✅ Estável — Base funcional

#### Adicionado
- Estrutura completa de produção (`forge-core/`, `forge-ui/`, `forge-cli/`)
- Contrato `IgnitionToken.sol` (herda de `NeoTokenBase`)
- Contrato `NeoTokenBase.sol` (base purificada)
- Scripts de deploy, verificação e simulação
- Interface web básica (React + Tailwind landing + Nuxt.js PWA)
- CLI tool (`neo-smart-factory init/deploy`)
- Templates de contratos (`token.sol.template`)
- Sistema interno de operações (`internal-ops/`)
- Simulador de ecossistemas (`NEO::simulate`)
- Documentação completa reorganizada
- Suporte completo a Polygon e Amoy testnet
- Padronização de nomenclatura (`neo-smart-factory`)

#### Mudado
- Reorganização completa da estrutura de pastas
- Configuração Hardhat otimizada para Polygon
- Documentação movida para `docs/`
- Comando CLI: `mello-forge` → `neo-smart-factory`
- Pacotes NPM: `neo-forge-*` → `neo-smart-factory-*`

#### Corrigido
- Configurações de rede
- Scripts de deploy
- Inconsistências de nomenclatura

#### Limitações Conhecidas
- ⚠️ Oracle não implementado (v0.6.0)
- ⚠️ DNA incompleto (campos básicos apenas)
- ⚠️ CULT parcial (marketing engine básico)
- ⚠️ Kernel não automatizado (comandos separados)

---

### [0.5.0] - 2024-01-01

#### Adicionado
- Contrato `NeoSmartFactory.sol`
- Módulos de tokens (ERC20, ERC721)
- Sistema de vesting (`NeoVesting.sol`)
- Sistema de recompensas e badges (`NeoRewards.sol`)
- Internal Ops App
- Mini-Simulador de Ecossistemas

---

## 🔄 Processo de Versionamento

### Convenções
- **Versão MAJOR** (1.0.0): Mudanças incompatíveis
- **Versão MINOR** (0.6.0): Novas funcionalidades compatíveis
- **Versão PATCH** (0.5.1): Correções e melhorias

### Nomes de Versões
Cada versão tem um nome temático relacionado ao manifesto:
- **IGNIÇÃO** (v0.5.x) — Base funcional
- **ORÁCULO** (v0.6.x) — Inteligência
- **CULT** (v0.7.x) — Narrativa
- **KERNEL** (v0.8.x) — Automação
- **IGNIÇÃO COMPLETA** (v1.0.0) — Sistema coeso

---

## ⚠️ Transparência sobre Estimativas

**Importante**: As datas estimadas são **projeções baseadas em desenvolvimento ativo**. Podem mudar baseado em:
- Feedback da comunidade
- Prioridades técnicas
- Recursos disponíveis
- Complexidade descoberta durante desenvolvimento

**Compromisso**: Manteremos este roadmap atualizado e transparente sobre mudanças.

---

**Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/)**

---

### 👤 Autoria

**Project Lead**: NODE NEØ  
**Email**: neo@neoprotocol.space  
**Web3 Identity**: neoprotocol.eth  
**NEØ PROTOCOL**: https://neoprotocol.space  
[![GitHub](https://img.shields.io/badge/GitHub-neo--smart--token--factory-181717?style=flat&logo=github)](https://github.com/neo-smart-token-factory)

> *Expand until silence becomes structure.*
