# Checklist de Execução — TON Factory Implementation

**Status**: 🔴 Aguardando início  
**Última Atualização**: 2026-01-24  
**Owner**: Mellø + Dev Team

---

## 🎯 Como Usar Este Checklist

1. ✅ = Completo e validado
2. 🔨 = Em progresso
3. ⏸️ = Bloqueado (dependência)
4. 🔴 = Não iniciado

**Regra**: Marcar como ✅ apenas após validation + review.

---

## 📦 FASE 1: Testing Foundation

### Semana 1 — Setup

#### Dia 1: Environment Setup
- [ ] 🔴 Criar branch `feat/ton-testing`
- [ ] 🔴 Instalar dependências de teste:
  ```bash
  cd smart-core
  npm install --save-dev @ton/sandbox @ton/test-utils jest ts-jest
  ```
- [ ] 🔴 Configurar `jest.config.js`
- [ ] 🔴 Criar `tests/ton/` directory structure
- [ ] 🔴 Setup helper functions em `tests/ton/helpers.ts`

**Validation**: `npm test` deve rodar sem erros (mesmo sem testes ainda).

---

#### Dia 2-3: Minter Unit Tests (Parte 1)
- [ ] 🔴 Implementar testes de **Initialization**:
  - [ ] Deploy with correct state
  - [ ] Admin set correctly
  - [ ] V2 params initialized
  - [ ] Zero initial supply
- [ ] 🔴 Implementar testes de **Owner Mint**:
  - [ ] Mint by owner succeeds
  - [ ] Non-owner rejected
  - [ ] Max supply respected
  - [ ] Supply increments correctly
  - [ ] Wallet deployed on first mint

**Validation**: 9/25 unit tests passing, coverage ~30%.

---

#### Dia 4-5: Minter Unit Tests (Parte 2)
- [ ] 🔴 Implementar testes de **Public Mint**:
  - [ ] Mint when enabled
  - [ ] Reject when disabled
  - [ ] Payment validation
  - [ ] Refund excess
  - [ ] Max supply check
  - [ ] Amount correct
- [ ] 🔴 Implementar testes de **Bridge Mint**:
  - [ ] Bridge mint succeeds
  - [ ] Non-bridge rejected
  - [ ] Supply cap

**Validation**: 18/25 unit tests passing, coverage ~60%.

---

### Semana 2 — Complete Testing

#### Dia 6-7: Minter Unit Tests (Parte 3)
- [ ] 🔴 Implementar testes de **Admin Operations**:
  - [ ] Withdraw TON
  - [ ] Change admin
  - [ ] Update metadata
  - [ ] Toggle public mint
  - [ ] Reject non-admin
- [ ] 🔴 Implementar testes de **Edge Cases**:
  - [ ] Max supply exact hit
  - [ ] Zero amounts
  - [ ] Concurrent mints
  - [ ] Wallet deploy failures

**Validation**: 25/25 minter tests passing, coverage >= 85%.

---

#### Dia 8-9: Wallet Unit Tests
- [ ] 🔴 Implementar testes de **Initialization**:
  - [ ] Deploy with owner
  - [ ] Link to minter
  - [ ] Zero balance
- [ ] 🔴 Implementar testes de **Transfer**:
  - [ ] Transfer between wallets
  - [ ] Insufficient balance rejected
  - [ ] Non-owner rejected
  - [ ] Forward amount handling
  - [ ] Transfer notification
  - [ ] Dest wallet deploy
- [ ] 🔴 Implementar testes de **Burn**:
  - [ ] Burn tokens
  - [ ] Notify minter
  - [ ] Over-balance rejected
  - [ ] Supply update
- [ ] 🔴 Implementar testes de **Edge Cases**:
  - [ ] Zero transfer
  - [ ] Self-transfer
  - [ ] Bounce handling
  - [ ] Gas edge cases

**Validation**: 15/15 wallet tests passing, coverage >= 80%.

---

#### Dia 10: Integration Tests
- [ ] 🔴 Implementar **Full Flow Test**:
  - [ ] Factory deploy
  - [ ] Jetton deploy
  - [ ] Public mint
  - [ ] Transfer
  - [ ] Burn
- [ ] 🔴 Implementar **Multi-User Test** (10 users)
- [ ] 🔴 Implementar **Max Supply Hit** scenario
- [ ] 🔴 Implementar **Admin Workflow** test
- [ ] 🔴 Implementar **Bridge Flow** test
- [ ] 🔴 Implementar **Gas Cost Validation**
- [ ] 🔴 Implementar **Storage Rent** lifecycle test

**Validation**: 7/7 integration tests passing, full flow validated.

---

#### Dia 11-12: CI/CD + Documentation
- [ ] 🔴 Configurar GitHub Actions para tests:
  ```yaml
  .github/workflows/ton-tests.yml
  ```
- [ ] 🔴 Adicionar badge de coverage ao README
- [ ] 🔴 Documentar test suite:
  - [ ] `tests/ton/README.md`
  - [ ] Como rodar testes
  - [ ] Como adicionar novos testes
- [ ] 🔴 Code review de todos os testes (peer review)

**Validation**: CI verde, docs completas.

---

## 🌐 FASE 2: Testnet Deployment

### Semana 3 — Deployment Scripts

#### Dia 13-14: Deploy Scripts
- [ ] 🔴 Criar `scripts/ton/deploy-testnet.ts`:
  - [ ] Factory deployment
  - [ ] Admin config
  - [ ] Treasury config
  - [ ] Validation checks
- [ ] 🔴 Criar `scripts/ton/create-test-jettons.ts`:
  - [ ] Deploy 3 test tokens
  - [ ] Different configurations
- [ ] 🔴 Criar `scripts/ton/validate-deployment.ts`:
  - [ ] Check storage layout
  - [ ] Verify op-codes
  - [ ] Test basic operations

**Validation**: Scripts executam sem erros em local sandbox.

---

#### Dia 15-16: Testnet Deploy
- [ ] 🔴 Deploy factory em **testnet.toncenter.com**
- [ ] 🔴 Verificar contract no TonScan
- [ ] 🔴 Configurar admin (usar testnet wallet por enquanto)
- [ ] 🔴 Deploy **Token A** (Public mint enabled, 10k cap)
- [ ] 🔴 Deploy **Token B** (Public mint disabled, 1M cap)
- [ ] 🔴 Deploy **Token C** (Bridge test)
- [ ] 🔴 Documentar addresses:
  ```markdown
  # Testnet Addresses
  Factory: EQ...
  Token A: EQ...
  Token B: EQ...
  Token C: EQ...
  ```

**Validation**: 3 tokens deployados e verificados no TonScan.

---

### Semana 4 — Validation

#### Dia 17-18: Public Mint Testing
- [ ] 🔴 Executar 50 public mints no Token A:
  - [ ] Script automatizado
  - [ ] Diferentes wallets
  - [ ] Monitorar gas costs
- [ ] 🔴 Tentar mint no Token B (deve falhar):
  - [ ] Validar reject message
- [ ] 🔴 Atingir max supply no Token A:
  - [ ] Validar supply cap enforcement
- [ ] 🔴 Documentar gas costs reais:
  ```markdown
  # Gas Costs (Testnet)
  - Public Mint: X TON
  - First-time wallet deploy: Y TON
  - Avg per mint: Z TON
  ```

**Validation**: 50+ mints executados, gas costs documentados.

---

#### Dia 19-20: Transfer & Burn Testing
- [ ] 🔴 Executar 100 transfers:
  - [ ] Between existing wallets
  - [ ] To new wallets (deploy)
  - [ ] Edge amounts (min, max)
- [ ] 🔴 Executar 20 burns:
  - [ ] Different amounts
  - [ ] Verify supply decrease
- [ ] 🔴 Admin operations:
  - [ ] Withdraw accumulated TON
  - [ ] Update metadata
  - [ ] Toggle public mint
- [ ] 🔴 Stress test:
  - [ ] 20 concurrent operations
  - [ ] Monitor failures

**Validation**: 100+ transfers, 20+ burns, admin ops OK.

---

#### Dia 21-22: Monitoring & Report
- [ ] 🔴 Setup monitoring:
  - [ ] TonScan API integration
  - [ ] Event listener
  - [ ] Basic dashboard
- [ ] 🔴 Coletar métricas:
  - [ ] Total operations
  - [ ] Success rate
  - [ ] Average gas costs
  - [ ] Failed transactions (analyze)
- [ ] 🔴 Criar **Testnet Validation Report**:
  ```markdown
  # Testnet Report
  ## Summary
  - Tokens deployed: 3
  - Public mints: 50+
  - Transfers: 100+
  - Burns: 20+
  - Success rate: X%
  ## Gas Costs
  (tabela)
  ## Issues Found
  (lista)
  ## Recommendations
  (lista)
  ```

**Validation**: Report completo, issues documentados.

---

## 🔒 FASE 3: Security & Audit

### Semana 5-6 — Internal Review

#### Dia 23-25: Code Review
- [ ] 🔴 **Reviewer 1** (Senior Dev):
  - [ ] Review NeoJettonFactory.fc
  - [ ] Review NeoJettonMinter.fc
  - [ ] Review NeoJettonWallet.fc
  - [ ] Document findings
- [ ] 🔴 **Reviewer 2** (Security Focus):
  - [ ] Attack vector analysis
  - [ ] Access control review
  - [ ] Gas griefing checks
  - [ ] Document findings
- [ ] 🔴 Consolidar findings:
  - [ ] Critical issues (immediate fix)
  - [ ] High issues (fix before audit)
  - [ ] Medium (document or fix)
  - [ ] Low (backlog)

**Validation**: Internal review report completo.

---

#### Dia 26-28: Fix Issues
- [ ] 🔴 Fix critical issues (se houver)
- [ ] 🔴 Fix high issues
- [ ] 🔴 Re-test após fixes
- [ ] 🔴 Update testnet deployment (se necessário)
- [ ] 🔴 Re-run validation tests

**Validation**: Zero critical/high issues, tests passing.

---

### Semana 7-8 — External Audit

#### Dia 29-30: Audit Preparation
- [ ] 🔴 Selecionar auditor:
  - [ ] CertiK vs Hacken vs outros
  - [ ] Get quotes
  - [ ] Choose & contract
- [ ] 🔴 Preparar documentation package:
  - [ ] Architecture docs
  - [ ] Test suite
  - [ ] Known issues log
  - [ ] Testnet report
- [ ] 🔴 Fornecer acesso ao auditor:
  - [ ] GitHub repo
  - [ ] Testnet addresses
  - [ ] Point of contact

**Validation**: Auditor contratado, docs enviados.

---

#### Dia 31-49: Audit Process (3 semanas)
- [ ] ⏸️ Aguardar audit findings
- [ ] ⏸️ Responder a questões do auditor
- [ ] ⏸️ Receber preliminary report
- [ ] 🔴 Fix critical/high findings
- [ ] 🔴 Document workarounds para medium/low
- [ ] 🔴 Re-submit para re-audit (se necessário)
- [ ] ⏸️ Receber final report

**Validation**: Final audit report com zero critical issues.

---

#### Dia 50-52: Post-Audit Actions
- [ ] 🔴 Publicar audit report (se permitido)
- [ ] 🔴 Update contratos com fixes
- [ ] 🔴 Re-deploy em testnet (versão final)
- [ ] 🔴 Re-run full validation suite
- [ ] 🔴 Update documentation

**Validation**: Versão auditada deployada em testnet, validada.

---

## 🚀 FASE 4: Mainnet Launch

### Semana 9 — Preparation

#### Dia 53-55: Infrastructure
- [ ] 🔴 Configurar **multisig wallets**:
  - [ ] Factory admin: 3-of-5
  - [ ] Treasury: 2-of-3
  - [ ] Document signers
  - [ ] Test multisig operations em testnet
- [ ] 🔴 Setup monitoring production:
  - [ ] TonScan integration
  - [ ] Alerting (PagerDuty / similar)
  - [ ] Dashboard
  - [ ] On-call rotation
- [ ] 🔴 Preparar runbooks:
  - [ ] Deployment playbook
  - [ ] Incident response plan
  - [ ] Rollback procedures (N/A para TON, documentar workarounds)

**Validation**: Multisigs testados, monitoring operational.

---

#### Dia 56-58: Documentation Finalization
- [ ] 🔴 **User Docs**:
  - [ ] How to deploy a token
  - [ ] How to public mint
  - [ ] How to transfer/burn
  - [ ] FAQ
- [ ] 🔴 **Developer Docs**:
  - [ ] Architecture deep dive
  - [ ] Integration guide
  - [ ] Op-codes reference
  - [ ] Gas optimization guide
- [ ] 🔴 **Operator Docs**:
  - [ ] Deployment guide
  - [ ] Monitoring guide
  - [ ] Troubleshooting guide

**Validation**: Docs peer-reviewed, publicadas.

---

### Semana 10 — Launch

#### Dia 59: Pre-Launch Checklist
- [ ] 🔴 **Go/No-Go Meeting**:
  - [ ] Review all checkpoints
  - [ ] Team consensus
  - [ ] Mellø final approval
- [ ] 🔴 Validar prerequisites:
  - [ ] ✅ Audit report OK
  - [ ] ✅ Tests 100% passing
  - [ ] ✅ Testnet validated (2+ weeks)
  - [ ] ✅ Multisigs configured
  - [ ] ✅ Monitoring ready
  - [ ] ✅ Docs complete
  - [ ] ✅ Team trained

**Decision**: 🟢 GO ou 🔴 NO-GO

---

#### Dia 60: Mainnet Deployment (GO day)
- [ ] 🔴 **Deploy Factory** (09:00 UTC):
  - [ ] Execute deployment script
  - [ ] Verify contract on TonScan
  - [ ] Transfer admin to multisig
  - [ ] Validate admin transfer
- [ ] 🔴 **Deploy NEØ Token** (10:00 UTC):
  - [ ] Deploy primeiro token oficial
  - [ ] Configure parameters
  - [ ] Execute smoke tests
  - [ ] Validate all operations
- [ ] 🔴 **Public Announcement** (12:00 UTC):
  - [ ] Tweet/X announcement
  - [ ] Discord announcement
  - [ ] Documentation link
  - [ ] Contract verification links
- [ ] 🔴 **Monitoring Active** (24/7):
  - [ ] On-call team ready
  - [ ] Alerts configured
  - [ ] Incident channel active

**Validation**: Factory + NEØ deployados, announcement feito, monitoring OK.

---

## 📊 Post-Launch (Week 11-12)

#### Week 11: Monitor & Support
- [ ] 🔴 Monitor 24/7 (first week)
- [ ] 🔴 Responder a issues no GitHub
- [ ] 🔴 Community support no Discord
- [ ] 🔴 Coletar feedback
- [ ] 🔴 Track usage metrics

#### Week 12: Analysis & Planning
- [ ] 🔴 Criar **Post-Launch Report**:
  - [ ] Usage statistics
  - [ ] Issues encountered
  - [ ] Feedback summary
  - [ ] Lessons learned
- [ ] 🔴 Plan V1.1 improvements:
  - [ ] Rate limiting
  - [ ] Multi-bridge support
  - [ ] Pausable functionality
- [ ] 🔴 Priorizar backlog

**Validation**: Report publicado, roadmap V1.1 definido.

---

## 🎯 Success Criteria Recap

### Technical
- ✅ Test coverage >= 85%
- ✅ Audit: zero critical issues
- ✅ Gas costs: ±10% do estimado
- ✅ 99.9% uptime em testnet (2 weeks)

### Business
- ✅ 10+ tokens deployados em testnet
- ✅ 100+ unique users testing
- ✅ 1000+ transactions em testnet

### Operational
- ✅ Incident response < 1h
- ✅ Docs completeness >= 90%
- ✅ Team confidence: High

---

## 🚨 Blocker Tracking

| Blocker ID | Description | Owner | Status | Resolution |
|------------|-------------|-------|--------|------------|
| - | - | - | 🟢 | - |

**Adicionar blockers conforme aparecerem.**

---

## 📞 Contacts

**Core Team**:
- Mellø (Architecture): [contact]
- Dev Lead: [contact]
- QA Lead: [contact]
- DevOps: [contact]

**External**:
- Auditor: [TBD after contract]
- Community Manager: [contact]

**Escalation**:
- Critical issues: Alert all
- High issues: Dev Lead + Mellø
- Medium/Low: Dev Team

---

## 📝 Change Log

| Data | Versão | Mudança | Autor |
|------|--------|---------|-------|
| 2026-01-24 | 1.0 | Checklist inicial | AI Agent |

---

**Status Atual**: 🔴 **Aguardando início de FASE 1**  
**Próximo Action Item**: Dia 1 - Environment Setup  
**Owner**: Dev Team  
**Deadline Proposto**: Mainnet launch em ~10 semanas (final de Março 2026)

---

**Instruções Finais**:
1. Atualizar este checklist diariamente
2. Marcar checkboxes apenas após validation
3. Documentar blockers imediatamente
4. Commit changes ao fim de cada dia
5. Weekly sync meeting para review de progresso

✅ **Let's build!**
