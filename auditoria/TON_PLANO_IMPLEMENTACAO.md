# Plano de Implementação — TON Factory V1.0

**Data**: 2026-01-24  
**Base**: Revisão Técnica Completa  
**Objetivo**: Preparar contratos TON para testnet deployment  
**Timeline Estimado**: 3-4 semanas até testnet, 8-10 semanas até mainnet

---

## 🎯 Objetivo Geral

Levar a implementação TON do estado atual (**compilado, não testado**) até **production-ready** seguindo as melhores práticas da rede TON.

---

## 📋 Status Atual (Checkpoint)

### ✅ Completo

- Compilação bem-sucedida de todos os contratos
- Standards compliance (TEP-74, TEP-64, TEP-89)
- Arquitetura V2-ready
- Documentation técnica completa
- Prior art registry estabelecida

### ⚠️ Em Falta (Blockers)

- **Testes automatizados** (crítico)
- **Testnet deployment** (crítico)
- **Auditoria externa** (recomendado)
- **User documentation** (importante)

### 💡 Melhorias Identificadas

- Rate limiting para public mint
- Multi-bridge support
- Pausable functionality
- Dynamic fee adjustment

---

## 🚀 Roadmap de Implementação

### FASE 1: Testing Foundation (Semana 1-2)

**Objetivo**: Criar infraestrutura de testes robusta.

#### 1.1 Setup de Ambiente
```bash
# Criar diretório de testes
mkdir -p smart-core/tests/ton

# Instalar dependências
npm install --save-dev \
  @ton/sandbox \
  @ton/test-utils \
  @ton/core \
  @ton/crypto \
  jest \
  ts-jest
```

**Deliverable**:

- [ ] Jest configurado
- [ ] TON Sandbox setup
- [ ] Helpers de teste criados

---

#### 1.2 Unit Tests - NeoJettonMinter

**Arquivo**: `tests/ton/NeoJettonMinter.spec.ts`

**Casos de Teste**:

```typescript
describe('NeoJettonMinter', () => {
  describe('Initialization', () => {
    test('Should deploy with correct initial state')
    test('Should set admin correctly')
    test('Should initialize v2_extra with correct params')
    test('Should have zero initial supply')
  })

  describe('Owner Mint', () => {
    test('Should mint tokens when called by owner')
    test('Should reject mint from non-owner')
    test('Should respect max supply cap')
    test('Should increment total supply correctly')
    test('Should deploy user wallet on first mint')
  })

  describe('Public Mint', () => {
    test('Should public mint when enabled')
    test('Should reject when disabled')
    test('Should require correct payment')
    test('Should refund excess payment')
    test('Should respect max supply')
    test('Should mint correct amount')
    test('Should accumulate TON in contract')
  })

  describe('Bridge Mint', () => {
    test('Should mint when called by bridge')
    test('Should reject from non-bridge address')
    test('Should respect max supply')
    test('Should emit correct events')
  })

  describe('Admin Operations', () => {
    test('Should withdraw accumulated TON')
    test('Should change admin')
    test('Should update metadata')
    test('Should toggle public mint')
    test('Should reject non-admin operations')
  })

  describe('Edge Cases', () => {
    test('Should handle max supply exactly')
    test('Should handle zero mint amount')
    test('Should handle concurrent mints')
    test('Should handle wallet deploy failures gracefully')
  })
})
```

**Deliverable**:

- [ ] 25+ unit tests implementados
- [ ] Coverage mínimo: 85%
- [ ] CI/CD integration

---

#### 1.3 Unit Tests - NeoJettonWallet

**Arquivo**: `tests/ton/NeoJettonWallet.spec.ts`

**Casos de Teste**:

```typescript
describe('NeoJettonWallet', () => {
  describe('Initialization', () => {
    test('Should deploy with correct owner')
    test('Should link to correct minter')
    test('Should have zero initial balance')
  })

  describe('Transfer', () => {
    test('Should transfer tokens between wallets')
    test('Should reject insufficient balance')
    test('Should reject from non-owner')
    test('Should handle forward amount correctly')
    test('Should send transfer notification when requested')
    test('Should deploy destination wallet if not exists')
  })

  describe('Burn', () => {
    test('Should burn tokens')
    test('Should notify minter of burn')
    test('Should reject burn over balance')
    test('Should update total supply in minter')
  })

  describe('Edge Cases', () => {
    test('Should handle zero transfer')
    test('Should handle self-transfer')
    test('Should handle bounce from invalid destination')
    test('Should handle gas edge cases')
  })
})
```

**Deliverable**:

- [ ] 15+ unit tests implementados
- [ ] Coverage mínimo: 80%

---

#### 1.4 Integration Tests

**Arquivo**: `tests/ton/Integration.spec.ts`

**Casos de Teste**:

```typescript
describe('Full Flow Integration', () => {
  test('Deploy Factory -> Deploy Jetton -> Public Mint -> Transfer -> Burn')
  test('Multi-user scenario (10+ users)')
  test('Max supply hit scenario')
  test('Admin operations workflow')
  test('Bridge mint + user transfer flow')
  test('Gas cost validation')
  test('Storage rent lifecycle')
})
```

**Deliverable**:

- [ ] 7+ integration tests
- [ ] Performance benchmarks documentados

---

### FASE 2: Testnet Deployment (Semana 3-4)

**Objetivo**: Validar contratos em ambiente real.

#### 2.1 Deployment Scripts

**Arquivo**: `scripts/ton/deploy-testnet.ts`

```typescript
// Features necessárias:
- Deploy factory to testnet
- Configure admin multisig
- Set treasury address
- Deploy test jetton
- Validate deployment
- Generate deployment report
```

**Deliverable**:

- [ ] Script de deploy automatizado
- [ ] Validação pós-deploy
- [ ] Rollback mechanism

---

#### 2.2 Testnet Validation

**Checklist**:

- [ ] Deploy factory em testnet.toncenter.com
- [ ] Criar 3+ tokens de teste diferentes:
  - Token A: Public mint enabled, baixo max supply (10k)
  - Token B: Public mint disabled, alto max supply (1M)
  - Token C: Bridge integration test
- [ ] Executar 50+ public mints por token
- [ ] Simular 100+ transfers entre wallets
- [ ] Testar burn de múltiplos usuários
- [ ] Validar admin operations (withdraw, metadata update)
- [ ] Monitorar gas costs reais vs estimados
- [ ] Stress test (hit max supply, concurrent operations)

**Deliverable**:

- [ ] Deployment report com addresses
- [ ] Gas cost real documentation
- [ ] Edge case findings documentados

---

#### 2.3 Monitoring Setup

**Tools**:

- TonScan API integration
- Custom event listener
- Alerting system

**Métricas**:

- Total deploys
- Public mint volume
- Transfer count
- Gas costs average
- Failed transactions

**Deliverable**:

- [ ] Dashboard básico
- [ ] Alertas configurados

---

### FASE 3: Auditoria e Hardening (Semana 5-8)

**Objetivo**: Garantir segurança para mainnet.

#### 3.1 Security Review

**Internal**:

- [ ] Code review completo (2+ devs)
- [ ] Security checklist TON-specific
- [ ] Attack vector analysis

**External**:

- [ ] Contratar auditoria (CertiK, Hacken, ou similar)
- [ ] Providenciar documentação completa
- [ ] Acompanhar findings
- [ ] Implementar fixes críticos

**Deliverable**:

- [ ] Internal review report
- [ ] External audit report
- [ ] Fix log documentado

---

#### 3.2 Improvements Implementation

**Based on Audit Findings**:

**Prioritização**:

1. **Critical**: Fix imediato, re-deploy testnet
2. **High**: Fix antes de mainnet
3. **Medium**: Fix ou documentar workaround
4. **Low**: Adicionar ao backlog V2

**Deliverable**:

- [ ] Patch release se necessário
- [ ] Updated test suite
- [ ] Re-deployment em testnet

---

#### 3.3 Documentation Finalization

**User Documentation**:

- [ ] How to deploy a token (CLI)
- [ ] How to public mint
- [ ] How to transfer/burn
- [ ] FAQ para usuários

**Developer Documentation**:

- [ ] Contract architecture deep dive
- [ ] Op-codes reference
- [ ] Integration guide
- [ ] Gas optimization tips

**Operator Documentation**:

- [ ] Deployment playbook
- [ ] Monitoring guide
- [ ] Incident response plan

**Deliverable**:

- [ ] docs/ completo e revisado
- [ ] Video tutorials (opcional)

---

### FASE 4: Mainnet Preparation (Semana 9-10)

**Objetivo**: Preparar infraestrutura para production.

#### 4.1 Infrastructure Setup

**Admin Wallets**:

- [ ] Configurar multisig 3-of-5 para factory admin
- [ ] Configurar multisig 2-of-3 para treasury
- [ ] Documentar key management procedures
- [ ] Backup e recovery process

**Monitoring**:

- [ ] Production monitoring stack
- [ ] Alerting configurado
- [ ] On-call rotation definida

**Deliverable**:

- [ ] Infrastructure as Code
- [ ] Runbook completo

---

#### 4.2 Mainnet Deployment

**Pre-Deploy Checklist**:

- [ ] Audit report publicado
- [ ] Tests passing (100%)
- [ ] Testnet validation completa (2+ semanas)
- [ ] Documentation completa
- [ ] Multisigs configurados
- [ ] Monitoring ready
- [ ] Team alignment

**Deploy Steps**:

1. Deploy factory to mainnet
2. Verify contract code on TonScan
3. Transfer admin para multisig
4. Deploy primeiro token oficial (NEØ)
5. Execute smoke tests
6. Public announcement

**Deliverable**:
- [ ] Mainnet addresses publicados
- [ ] Verification links
- [ ] Launch announcement

---

#### 4.3 Post-Launch

**Week 1**:
- [ ] Monitor 24/7
- [ ] Responder a issues rapidamente
- [ ] Coletar feedback

**Week 2-4**:
- [ ] Analyze usage patterns
- [ ] Optimize based on real data
- [ ] Plan V1.1 improvements

**Deliverable**:
- [ ] Post-launch report
- [ ] Lessons learned doc

---

## 🛠️ Melhorias Planejadas (V1.1+)

### High Priority
1. **Rate Limiting para Public Mint**
   - Implementar cooldown per-address
   - Cap per-user configurable
   - **Effort**: 3-5 dias
   - **Impact**: Previne supply drain

2. **Multi-Bridge Support**
   - Substituir single address por dict
   - Oracle de validação
   - **Effort**: 5-7 dias
   - **Impact**: Suporta múltiplos bridges

3. **Pausable Functionality**
   - Emergency pause toggle
   - Admin-only, reversível
   - **Effort**: 2-3 dias
   - **Impact**: Circuit breaker para crises

### Medium Priority
4. **Dynamic Fee Adjustment**
   - Mint price ajustável via governance
   - Min/max bounds
   - **Effort**: 3-4 dias
   - **Impact**: Adaptabilidade de mercado

5. **Enhanced Metadata**
   - Suporte a mais campos TEP-64
   - Logo on-chain
   - **Effort**: 2-3 dias
   - **Impact**: Melhor integração com wallets

### Low Priority (V2)
6. **DAO Governance**
7. **Fee Distribution para Holders**
8. **NFT Hybrid Support**

---

## 📊 Métricas de Sucesso

### Technical Metrics
- ✅ Test coverage >= 85%
- ✅ Zero critical issues no audit
- ✅ Gas costs dentro do esperado (±10%)
- ✅ 99.9% uptime em testnet (2 semanas)

### Business Metrics
- 🎯 10+ tokens deployados em testnet
- 🎯 100+ usuários únicos testando
- 🎯 1000+ transações em testnet
- 🎯 Community feedback positivo

### Operational Metrics
- 🔧 Incident response < 1 hora
- 🔧 Documentation completeness score >= 90%
- 🔧 Team confidence level: High

---

## 💰 Estimativa de Custos

### Development
- Testes (80h): $8,000
- Testnet ops (40h): $4,000
- Documentation (30h): $3,000
- **Subtotal**: $15,000

### External Services
- Auditoria externa: $15,000 - $30,000
- Testnet TON: ~100 TON (~$250)
- Mainnet deploy: ~50 TON (~$125)
- **Subtotal**: $15,375 - $30,375

### **Total Estimado**: $30,000 - $45,000

---

## 🚦 Go/No-Go Criteria

### Para Testnet Deployment
- ✅ Unit tests >= 85% coverage
- ✅ Integration tests passing
- ✅ Internal security review OK

### Para Mainnet Deployment
- ✅ Testnet validation >= 2 semanas
- ✅ External audit com zero critical issues
- ✅ Documentation completa
- ✅ Multisigs configurados
- ✅ Monitoring operational
- ✅ Team consensus

---

## 📅 Timeline Visual

```text
SEMANA 1-2: TESTING
├─ Unit Tests (Minter)
├─ Unit Tests (Wallet)
├─ Integration Tests
└─ CI/CD Setup

SEMANA 3-4: TESTNET
├─ Deploy Scripts
├─ Testnet Deployment
├─ Validation & Monitoring
└─ Gas Cost Analysis

SEMANA 5-8: AUDIT
├─ Internal Review
├─ External Audit
├─ Fixes Implementation
└─ Documentation

SEMANA 9-10: MAINNET
├─ Infrastructure Setup
├─ Mainnet Deploy
├─ Launch
└─ Post-Launch Support
```

---

## 🤝 Responsabilidades

### Core Team
- **Mellø**: Architecture review, final approval
- **Dev Lead**: Implementation, code review
- **QA Lead**: Test design, validation
- **DevOps**: Infrastructure, monitoring

### External
- **Auditor**: Security review
- **Community**: Beta testing em testnet

---

## 📞 Support & Escalation

### Issues Tracking
- GitHub Issues para bugs
- Discord para community support
- Private channel para security issues

### Escalation Path
1. **Dev Team** (< 4h response)
2. **Lead Dev** (< 2h response)
3. **Mellø** (< 1h response para critical)

---

## ✅ Conclusão

Este plano leva a implementação TON de **compilado** para **production-ready** em **8-10 semanas** seguindo as melhores práticas da rede TON.

**Próximo passo imediato**: Iniciar FASE 1.1 (Setup de Testes)

**Aprovação necessária**: Mellø sign-off antes de cada fase

---

**Criado por**: AI Agent + Mellø  
**Data**: 2026-01-24  
**Status**: ⚠️ Aguardando aprovação para iniciar  
**Versão**: 1.0
