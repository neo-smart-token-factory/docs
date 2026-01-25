# Revisão Técnica — NΞØ Factory TON V1.0

**Data da Revisão**: 2026-01-24  
**Versão Analisada**: V1.0 (V2-Ready Architecture)  
**Commit Base**: `69bfe6cc19fc4c139c88f85d00870cb35cf0e252`  
**Revisor**: Mellø + AI Agent  
**Status**: ✅ Compilado | ⚠️ Pendente Deployment Testnet

---

## 📋 Sumário Executivo

### Status Geral

- ✅ **Compilação**: Bem-sucedida com `@ton-community/func-js` v0.6.2
- ✅ **Compliance**: TEP-74, TEP-64, TEP-89 conformes
- ✅ **Arquitetura**: Factory + Minter + Wallet (padrão TON)
- ⚠️ **Segurança**: Revisão interna completa, auditoria externa recomendada
- ⚠️ **Deployment**: Pendente (testnet first)

### Inovações Principais

1. **Public Mint** nativo (pagamento em TON)
2. **Bridge Integration** para cross-chain
3. **Max Supply** enforcement no contrato
4. **Sovereign Factory Pattern** (V2-ready desde V1)

---

## 🏗️ Arquitetura Detalhada

### 1. Factory Contract (`NeoJettonFactory.fc`)

**Responsabilidade**: Fábrica soberana de Jettons com inicialização V2-ready.

#### Storage Layout

```func
admin_address: MsgAddress           # Administrador da factory
jetton_minter_code: ^Cell          # Template do Minter
jetton_wallet_code: ^Cell          # Template do Wallet
treasury_address: MsgAddress        # Endereço do tesouro para fees
```

#### Operações Suportadas

| Op-Code | Operação | Acesso | Status |
|---------|----------|--------|--------|
| `0x61caf729` | `deploy_jetton` | Public | ✅ |
| `0x3` | `change_admin` | Admin | ✅ |
| `0x48087794` | `withdraw` | Admin | ✅ |

#### Validações Implementadas

- ✅ Pagamento mínimo para deploy
- ✅ Validação de admin antes de operações críticas
- ✅ Inicialização de Minter com código imutável
- ✅ Passagem correta de `v2_extra` params

**Pontos de Atenção**:

- ⚠️ **Fee Structure**: Não há mecanismo de ajuste dinâmico de fee para deploy
- ⚠️ **Rate Limiting**: Ausência de proteção contra spam de deploys
- ℹ️ **Upgrade Path**: Factory é imutável, novos features requerem nova factory

---

### 2. Minter Contract (`NeoJettonMinter.fc`)

**Responsabilidade**: Contrato master por token, controla lógica de mint/burn/metadata.

#### Storage Layout (V2 Extended)

```func
total_supply: Coins                 # Supply circulante atual
admin: MsgAddress                   # Admin do token
content: ^Cell                      # Metadata TEP-64
jetton_wallet_code: ^Cell          # Template de wallet

# V2 Extra Cell
v2_extra: ^Cell
    ├─ max_supply: Coins           # ✅ Hard cap enforcement
    ├─ mint_price: Coins           # ✅ Preço do public mint
    ├─ mint_amount: Coins          # ✅ Quantidade por mint tx
    ├─ public_mint_enabled: Int1   # ✅ Toggle de public mint
    ├─ bridge_minter: MsgAddress   # ✅ Bridge autorizada
    └─ minters_dict: Dict          # ✅ Multi-minter support
```

#### Operações Suportadas

| Op-Code | Operação | Acesso | Validações |
|---------|----------|--------|------------|
| `0x15` | `mint` | Owner | ✅ Max supply, admin check |
| `0x4f3c7069` | `public_mint` | Public | ✅ Payment, supply cap, enabled flag |
| `0x69680373` | `bridge_mint` | Bridge | ✅ Sender == bridge, supply cap |
| `0x595f07bc` | `burn` | Owner | ✅ Balance check no wallet |
| `0x4` | `change_content` | Admin | ✅ Admin check |
| `0x48087794` | `withdraw` | Admin | ✅ Admin check, balance available |

#### Fluxo de Public Mint

```text
1. User envia mensagem com `public_mint` + payment em TON
2. Contrato valida:
   - public_mint_enabled == true
   - msg_value >= mint_price
   - total_supply + mint_amount <= max_supply
3. Se válido:
   - Incrementa total_supply
   - Deploy/credita wallet do usuário
   - Retém TON no contrato para posterior withdraw
4. Se inválido:
   - Reject com bounce (TON devolvido)
```

**Pontos Fortes**:

- ✅ Enforcement de max supply em todas as operações de mint
- ✅ Separação clara de roles (owner/bridge/public)
- ✅ Proteção contra re-entrancy via actor model TON
- ✅ Metadata imutável após deploy (exceto via admin)

**Pontos de Atenção**:

- ⚠️ **Mint Amount Fixed**: `mint_amount` não é ajustável após deploy (requer re-deploy)
- ⚠️ **Bridge Trust**: Apenas 1 bridge address permitido (não suporta multi-bridge nativo)
- ⚠️ **Public Mint Toggle**: Uma vez desabilitado, não há mecanismo de re-enable sem admin
- ℹ️ **Gas Costs**: Estimado ~0.05 TON por mint (testar em testnet para confirmar)

---

### 3. Wallet Contract (`NeoJettonWallet.fc`)

**Responsabilidade**: Contrato individual por usuário/token, gerencia balance e transferências.

#### Storage Layout (TEP-74)

```func
balance: Coins                      # Saldo do token
owner: MsgAddress                   # Dono da wallet
jetton_master: MsgAddress          # Minter pai
jetton_wallet_code: ^Cell          # Self-code para transfers
```

### Operações Suportadas

| Op-Code | Operação | Acesso | Validações |
|---------|----------|--------|------------|
| `0xf8a7ea5` | `transfer` | Owner | ✅ Balance, forward amount |
| `0x178d4519` | `internal_transfer` | System | ✅ Sender verification |
| `0x595f07bc` | `burn` | Owner | ✅ Balance check |

#### Fluxo de Transfer
```text
1. User envia `transfer` da sua wallet
2. Source wallet verifica:
   - msg sender == owner
   - balance >= transfer amount + fees
3. Source wallet debita balance e envia `internal_transfer` para dest wallet
4. Dest wallet credita balance e envia `transfer_notification` (se solicitado)
```

**Pontos Fortes**:
- ✅ TEP-74 compliance total
- ✅ Notificações opcionais de transfer
- ✅ Gas optimization (storage rent mínimo)

**Pontos de Atenção**:
- ℹ️ **Forward Amount**: User deve prover TON suficiente para criar dest wallet se não existir
- ℹ️ **Bounce Handling**: Transfers com destino inválido retornam para source (safe)

---

## 🔒 Análise de Segurança

### Vetores de Ataque Revisados

#### ✅ Mitigados
1. **Re-entrancy**: Não aplicável no modelo actor TON
2. **Integer Overflow**: FunC tem overflow checks nativos
3. **Unauthorized Mint**: Role-based access control implementado
4. **Supply Manipulation**: Max supply enforced em todas as paths

#### ⚠️ Atenção Necessária
1. **Admin Key Management**:
   - Factory admin controla withdraw de fees acumulados
   - Minter admin controla metadata e mint toggle
   - **Recomendação**: Usar multisig wallet para admins críticos

2. **Bridge Security**:
   - Bridge address é trusted (não há oracle de validação)
   - **Recomendação**: Auditoria do bridge contract antes de set

3. **Public Mint DoS**:
   - Não há rate limiting por usuário
   - **Impacto**: User pode esgotar supply rapidamente se mint_amount for alto
   - **Recomendação**: Implementar cooldown per-address ou cap per-user

4. **Gas Griefing**:
   - Operações custam gas do sender (não do contrato)
   - **Impacto**: Baixo, mas user pode perder TON em tx failed
   - **Recomendação**: Validação client-side antes de enviar tx

### Conformidade com Standards

#### TEP-74 (Jetton Standard)
- ✅ Transfer message format
- ✅ Notification callbacks
- ✅ Balance queries
- ✅ Burn implementation

#### TEP-64 (Token Metadata)
- ✅ On-chain metadata (name, symbol, decimals)
- ✅ Off-chain URI support
- ✅ JSON schema compliance

#### TEP-89 (Discovery)
- ✅ `get_wallet_address(owner)` implemented
- ✅ `get_jetton_data()` implemented
- ✅ Supply queries available

**Status**: ✅ **Fully compliant**

---

## 📊 Análise de Gas Costs

### Estimativas (Testnet Validation Pending)

| Operação | Computation | Storage Rent | Total (TON) | Notas |
|----------|-------------|--------------|-------------|-------|
| Deploy Jetton | ~0.05 | ~0.15 | **~0.20** | Inclui deploy de minter + init storage |
| Public Mint | ~0.01 | ~0.04 | **~0.05** + mint_price | Pode incluir deploy de wallet |
| Transfer | ~0.008 | ~0.02 | **~0.028** | Wallet já existe |
| Transfer (New Dest) | ~0.012 | ~0.05 | **~0.062** | Deploy de dest wallet |
| Burn | ~0.008 | ~0.02 | **~0.028** | Notificação para minter |

**Otimizações Implementadas**:
- ✅ Storage layout compacto (usa Cell refs eficientemente)
- ✅ Operações comuns otimizadas (transfer path direto)
- ✅ Metadata em off-chain URI (reduz on-chain storage)

**Recomendações**:
- ⚠️ Testar em testnet para confirmar custos reais
- ℹ️ Documentar custos no frontend para UX transparente

---

## 🚀 Deployment Readiness

### Checklist Pré-Deploy

#### Compilação
- ✅ FunC source válido
- ✅ BOC artifacts gerados
- ✅ Hash verification implementado
- ✅ Git commit registry

#### Testes
- ⚠️ **Unit tests**: Não identificados no repositório
- ⚠️ **Integration tests**: Não identificados
- ⚠️ **Testnet deployment**: Pendente
- ⚠️ **Load testing**: Não realizado

**CRÍTICO**: Implementar suite de testes antes de mainnet.

#### Segurança
- ✅ Internal review completed
- ⚠️ **External audit**: Recomendado (não realizado)
- ⚠️ **Bug bounty**: Não configurado
- ✅ License clara (CC BY-NC-ND 4.0)

#### Documentação
- ✅ Technical registry complete
- ✅ Op-codes documented
- ✅ Storage layout specified
- ⚠️ **User guides**: Não criados
- ⚠️ **Developer docs**: Parcial

### Roadmap de Deploy Recomendado

```text
FASE 1: Validação Técnica (1-2 semanas)
├─ [ ] Implementar unit tests (NeoJettonMinter, NeoJettonWallet)
├─ [ ] Implementar integration tests (deploy -> mint -> transfer -> burn)
├─ [ ] Deploy em testnet local (TON Sandbox)
└─ [ ] Validar gas costs reais

FASE 2: Testnet Público (2-3 semanas)
├─ [ ] Deploy em testnet.toncenter.com
├─ [ ] Criar 5+ tokens de teste
├─ [ ] Simular public mint load (100+ users)
├─ [ ] Testar edge cases (max supply hit, admin ops)
└─ [ ] Monitorar storage rent e gas usage

FASE 3: Auditoria (3-4 semanas)
├─ [ ] Contratar auditoria externa (CertiK, Hacken, ou similar)
├─ [ ] Fix critical/high issues
├─ [ ] Re-deploy testnet após fixes
└─ [ ] Publicar audit report

FASE 4: Mainnet (após aprovação)
├─ [ ] Configurar multisig admin wallets
├─ [ ] Deploy factory em mainnet
├─ [ ] Deploy primeiro token oficial (NEØ)
├─ [ ] Ativar monitoring e alerts
└─ [ ] Launch marketing + documentation
```

---

## 🔄 Comparação com Implementações EVM

### Paridade de Features

| Feature | EVM (Polygon) | TON (Current) | Status |
|---------|---------------|---------------|--------|
| Public Mint | ✅ | ✅ | ✅ Parity |
| Bridge Mint | ✅ | ✅ | ✅ Parity |
| Max Supply | ✅ | ✅ | ✅ Parity |
| Burn | ✅ | ✅ | ✅ Parity |
| Metadata | ✅ | ✅ | ✅ Parity (TEP-64) |
| Pausable | ✅ | ⚠️ Partial | ⚠️ Não há pause global |
| Upgradeable | ⚠️ Proxy | ❌ Immutable | ℹ️ TON design choice |
| Multi-Bridge | ✅ | ⚠️ Limited | ⚠️ Apenas 1 bridge address |

### Diferenças Arquiteturais

#### EVM
```solidity
// Centralizado: 1 contrato, N balances
mapping(address => uint256) balances;
```

#### TON
```func
// Descentralizado: N contratos (1 wallet per user)
each wallet = separate contract with storage
```

**Implicações**:
- ✅ TON: Melhor sharding e paralelização
- ⚠️ TON: Gas costs mais altos para primeira interação
- ✅ EVM: Gas costs previsíveis
- ⚠️ EVM: Bottleneck em contratos populares

---

## 📈 Roadmap V2 Features

### Planejado (Não Implementado Ainda)

1. **DAO Governance Integration**
   - Voting power baseado em token balance
   - Proposal creation/execution on-chain
   - **Status**: Conceitual

2. **Advanced Fee Distribution**
   - Fee sharing para holders (staking-like)
   - Dynamic fee adjustment via governance
   - **Status**: Conceitual

3. **Cross-Chain Bridge Expansion**
   - Suporte multi-bridge (não apenas 1 address)
   - Oracle de validação para cross-chain mints
   - **Status**: Conceitual

4. **NFT Metadata Extensions**
   - Hybrid fungible/semi-fungible tokens
   - Per-token metadata overrides
   - **Status**: Não planejado para V1

### V2-Ready desde V1
- ✅ Storage layout com `v2_extra` cell
- ✅ Extensibilidade via `minters_dict`
- ✅ Bridge integration hooks

**Nota**: Contratos são imutáveis. V2 requer novo deploy com migration path.

---

## ⚠️ Limitações Conhecidas

### Técnicas
1. **Fixed Mint Amount**: Não ajustável após deploy
2. **Single Bridge**: Apenas 1 bridge address suportado nativamente
3. **No Rate Limiting**: Public mint pode ser esgotado rapidamente
4. **No Upgrade Path**: Imutável (requer re-deploy para updates)

### Operacionais
1. **Testnet Validation**: Não realizado ainda
2. **Gas Costs**: Estimados, não confirmados
3. **Load Testing**: Não realizado
4. **User Documentation**: Incompleta

### Legais
1. **License Restriction**: CC BY-NC-ND 4.0 (não permite modificações sem permissão)
2. **Patent Status**: Prior art estabelecida, mas não há patente defensiva

---

## ✅ Recomendações Finais

### Críticas (Antes de Mainnet)
1. ⚠️ **Implementar suite de testes** (unit + integration)
2. ⚠️ **Deploy e validar em testnet** (mínimo 2 semanas)
3. ⚠️ **Auditoria externa** (recomendado)
4. ⚠️ **Configurar multisig** para admin wallets

### Importantes
1. ℹ️ Documentar gas costs reais após testnet
2. ℹ️ Criar user guides e developer docs
3. ℹ️ Implementar monitoring e alerts para mainnet
4. ℹ️ Considerar bug bounty program

### Nice-to-Have
1. 💡 Rate limiting para public mint
2. 💡 Multi-bridge support
3. 💡 Dynamic fee adjustment
4. 💡 Pausable functionality (circuit breaker)

---

## 📊 Score Card Final

| Categoria | Score | Status |
|-----------|-------|--------|
| **Compilação** | 10/10 | ✅ Perfeito |
| **Standards Compliance** | 10/10 | ✅ TEP-74/64/89 |
| **Arquitetura** | 9/10 | ✅ Sólida, V2-ready |
| **Segurança (Internal)** | 8/10 | ✅ Boa, audit needed |
| **Gas Optimization** | 8/10 | ✅ Bom, testar real costs |
| **Testing** | 3/10 | ⚠️ Crítico: faltam testes |
| **Documentation** | 7/10 | ✅ Boa técnica, falta user docs |
| **Deployment Readiness** | 5/10 | ⚠️ Testnet needed |

**Overall**: **7.5/10** — Sólido tecnicamente, mas requer testes e validação antes de mainnet.

---

## 📝 Próximos Passos

### Imediato (Esta Semana)
1. [ ] Criar suite de unit tests para Minter
2. [ ] Criar suite de unit tests para Wallet
3. [ ] Implementar integration test (full flow)

### Curto Prazo (2 Semanas)
1. [ ] Deploy em testnet local (TON Sandbox)
2. [ ] Deploy em testnet público
3. [ ] Validar gas costs reais
4. [ ] Criar user documentation

### Médio Prazo (1 Mês)
1. [ ] Contratar auditoria externa
2. [ ] Fix issues do audit
3. [ ] Preparar mainnet deploy
4. [ ] Configurar monitoring

---

**Status**: ✅ **Pronto para continuar implementação**  
**Blocker**: ⚠️ **Testes devem ser criados antes de testnet deploy**  
**Aprovação para Testnet**: ⚠️ **Condicionada a testes básicos**

---

**Revisado por**: Mellø + AI Agent  
**Data**: 2026-01-24  
**Próxima Revisão**: Após testnet deployment  
**Versão do Documento**: 1.0
