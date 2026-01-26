# Inventário de Documentos — NΞØ SMART TOKEN FACTORY

**Data**: 2026-01-22  
**Versão**: 1.0  
**Status**: Inventário Completo

---

## 📋 Resumo Executivo

Este inventário mapeia todos os documentos relevantes do repositório `docs` que descrevem a NΞØ SMART TOKEN FACTORY, incluindo arquitetura, módulos, governança, automação, wallet abstraction, MPC/MCP e políticas de exposição de repositório.

**Total de documentos identificados**: 57 arquivos Markdown  
**Documentos relevantes para o pacote**: 45+ arquivos

---

## 🏛️ 1. Core & Fundamentos

### Manifesto e Valores

| Path | Descrição | Relevância |
|------|-----------|------------|
| `core/manifesto.md` | Manifesto oficial do projeto: visão, valores e missão da NΞØ SMART FACTORY | ⭐⭐⭐ CRÍTICO |
| `core/governance.md` | Protocolo de governança: workflows, regras de contribuição, padrões de qualidade | ⭐⭐⭐ CRÍTICO |
| `core/contributing.md` | Guia de contribuição: padrões de commit, estrutura de PRs | ⭐⭐ ALTO |
| `core/LICENSE` | Licença MIT do projeto | ⭐⭐ ALTO |

### Documentos de Apresentação

| Path | Descrição | Relevância |
|------|-----------|------------|
| `INVESTOR_PITCH.md` | Apresentação completa para investidores | ⭐⭐ ALTO |
| `INVESTOR_PITCH_SUMMARY.md` | Resumo executivo para investidores | ⭐⭐ ALTO |
| `README.md` | Documentação centralizada e navegação rápida | ⭐⭐⭐ CRÍTICO |
| `INDEX.md` | Índice completo da documentação organizada por domínios | ⭐⭐⭐ CRÍTICO |

---

## 🏗️ 2. Arquitetura & Especificações Técnicas

### Arquitetura Geral

| Path | Descrição | Relevância |
|------|-----------|------------|
| `architecture/architecture.md` | Arquitetura detalhada: Factory Modular, componentes principais (NeoSmartFactory, NeoERC20, NeoERC721, NeoVesting, NeoRewards) | ⭐⭐⭐ CRÍTICO |
| `architecture/surgical.md` | Arquitetura cirúrgica: descrição detalhada dos 5 blocos (smart-core, smart-cli, smart-ui, docs, internal-ops) | ⭐⭐⭐ CRÍTICO |
| `architecture/nomenclature.md` | Padrões de nomenclatura e convenções do projeto | ⭐⭐ ALTO |
| `architecture/adr/decision-log.md` | Registro de decisões arquiteturais (ADRs) | ⭐⭐ ALTO |
| `architecture/ARCHITECTURAL_ADDENDUMS.md` | Adendos arquiteturais: MCP, automação, MPC, wallets, extensões, KYC, governança | ⭐⭐⭐ CRÍTICO |

### Especificações Técnicas (Specs)

| Path | Descrição | Relevância |
|------|-----------|------------|
| `architecture/specs/neotoken-v2.md` | NeoTokenV2: arquitetura multichain & Account Abstraction (EIP-2612, Bridge Minter, anti-bot) | ⭐⭐⭐ CRÍTICO |
| `architecture/specs/doctor-cli-deep-dive.md` | Detalhamento do Doctor CLI (Produto Fase A) | ⭐⭐ ALTO |
| `architecture/specs/base-repository.md` | Padrão ouro do repositório: estrutura e padrões | ⭐⭐ ALTO |
| `architecture/specs/base-agentkit-guide.md` | Guia de integração com Coinbase AI Agent Kit (Base Network) | ⭐⭐ ALTO |

---

## ⚙️ 3. Operações & Padrões

### Guias Operacionais

| Path | Descrição | Relevância |
|------|-----------|------------|
| `operations/guides/operational-guide.md` | Manual de operação: como usar ferramentas internas | ⭐⭐ ALTO |
| `operations/guides/manual-bridge.md` | Manual de bridge: segurança e logística de transferências cross-chain | ⭐⭐ ALTO |
| `operations/guides/miniapp-integration.md` | Integração MiniApp Telegram: arquitetura de distribuição, backend, configuração | ⭐⭐ ALTO |

### Deployment & CI

| Path | Descrição | Relevância |
|------|-----------|------------|
| `operations/deployment/history.md` | Histórico de deployments | ⭐ MÉDIO |
| `operations/deployment/ci-workflows.md` | Especificação de workflows CI | ⭐⭐ ALTO |

### Padrões de Repositório (Standards)

| Path | Descrição | Relevância |
|------|-----------|------------|
| `operations/standards/workflow-baseline.md` | Baseline de workflows: padrões mínimos | ⭐⭐ ALTO |
| `operations/standards/bootstrap-checklist.md` | Checklist de bootstrap para novos repositórios | ⭐⭐ ALTO |
| `operations/standards/github-apps.md` | GitHub Apps e integrações | ⭐ MÉDIO |
| `operations/standards/REPOSITORY_VISIBILITY_POLICY.md` | Política de visibilidade: o que pode ser público vs privado | ⭐⭐⭐ CRÍTICO |
| `operations/standards/SECURITY_ENFORCEMENT_REPORT.md` | Relatório de enforcement de segurança | ⭐⭐ ALTO |

---

## 🎯 4. Estratégia & Produto

### Roadmaps

| Path | Descrição | Relevância |
|------|-----------|------------|
| `strategy/roadmap-tech.md` | Roadmap técnico: evolução da stack tecnológica, integração Base Network | ⭐⭐ ALTO |
| `strategy/roadmap-cash.md` | Roadmap de produto e cash: estratégia de monetização e fluxos de caixa | ⭐⭐ ALTO |
| `strategy/cli-product-roadmap.md` | Roadmap do CLI como produto | ⭐⭐ ALTO |

### Planejamento de Execução

| Path | Descrição | Relevância |
|------|-----------|------------|
| `strategy/planning/overview.md` | Visão geral de planejamento | ⭐ MÉDIO |
| `strategy/planning/landing-plan.md` | Plano de landing page | ⭐ MÉDIO |
| `strategy/planning/offer-definition.md` | Definição de oferta | ⭐ MÉDIO |
| `strategy/planning/monetization-plan.md` | Plano de monetização detalhado | ⭐⭐ ALTO |

---

## 📜 5. Histórico & Auditoria

### Auditoria

| Path | Descrição | Relevância |
|------|-----------|------------|
| `auditoria/RELATORIO_AUDITORIA.md` | Relatório de auditoria: comparação modelo inicial vs implementação atual | ⭐⭐ ALTO |
| `auditoria/MODELO_INICIAL_CONCEITUAL.md` | Modelo inicial conceitual: visão inicial e brainstorm | ⭐ MÉDIO |
| `auditoria/neo_manifesto_updated.md` | Manifesto atualizado (histórico) | ⭐ MÉDIO |
| `auditoria/neo-multirepo.md` | Plano de migração multi-repo | ⭐ MÉDIO |
| `auditoria/factory-status.md` | Status da factory | ⭐ MÉDIO |
| `auditoria/CHANGELOG.md` | Changelog da auditoria | ⭐ MÉDIO |
| `auditoria/INCONSISTENCIAS_NOMENCLATURA.md` | Inconsistências de nomenclatura | ⭐ BAIXO |
| `auditoria/STRUCTURE_VALIDACAO.md` | Validação de estrutura | ⭐ BAIXO |
| `auditoria/neo_disclaimers.md` | Disclaimers | ⭐ BAIXO |

### Análise e Conclusão

| Path | Descrição | Relevância |
|------|-----------|------------|
| `auditoria/analise-conclusao/ANALISE_DOCUMENTOS.md` | Análise de documentos | ⭐ MÉDIO |
| `auditoria/analise-conclusao/arquitetura.md` | Arquitetura (planejamento futuro) | ⭐ MÉDIO |
| `auditoria/analise-conclusao/MAPEAMENTO_ATUAL_VS_FUTURO.md` | Mapeamento atual vs futuro | ⭐ MÉDIO |
| `auditoria/analise-conclusao/plano-migr.md` | Plano de migração | ⭐ MÉDIO |
| `auditoria/analise-conclusao/repos.md` | Repositórios oficiais | ⭐ MÉDIO |
| `auditoria/analise-conclusao/REPOSITORIOS_NECESSARIOS.md` | Repositórios necessários | ⭐ MÉDIO |

### Archive

| Path | Descrição | Relevância |
|------|-----------|------------|
| `archive/changelog.md` | Changelog histórico | ⭐ MÉDIO |
| `archive/patch-v0.5.1.md` | Patch v0.5.1 - Notas da versão de ignição | ⭐ MÉDIO |

---

## 🎨 6. Branding & Identidade

| Path | Descrição | Relevância |
|------|-----------|------------|
| `branding/IDENTITY.md` | Identidade de marca | ⭐ MÉDIO |
| `branding/marca-tecnico.md` | Marca técnica | ⭐ MÉDIO |

---

## 🌐 7. Ecossistema

| Path | Descrição | Relevância |
|------|-----------|------------|
| `ecosystem/ANALYSIS_2026_01.md` | Análise do ecossistema (Janeiro 2026) | ⭐ MÉDIO |

---

## 🔐 8. Segurança & Políticas

### Políticas de Segurança

| Path | Descrição | Relevância |
|------|-----------|------------|
| `registro/SECURITY_REPO_ANTIGO_POLICY.md` | Política de segurança: repositório antigo (criado em 2026-01-22) | ⭐⭐ ALTO |
| `operations/standards/REPOSITORY_VISIBILITY_POLICY.md` | Política de visibilidade de repositórios | ⭐⭐⭐ CRÍTICO |

---

## 📊 9. Prova Histórica

### Repositórios

| Tipo | URL | Data Primeiro Commit | Status |
|------|-----|---------------------|--------|
| **Repositório Mais Antigo** | `https://github.com/neomello/neo_smart_factory` | 2025-11-16 | Privado, inativo (mantido para registro) |
| **Organização Atual** | `https://github.com/neo-smart-token-factory` | 2025-11-17 | Ativo, desenvolvimento contínuo |

### Documentos de Registro

| Path | Descrição | Relevância |
|------|-----------|------------|
| `registro/INVESTIGACAO_REPOSITORIO_ANTIGO.md` | Investigação do repositório antigo | ⭐⭐ ALTO |
| `registro/AUTHOR_DATA_TEMPLATE.md` | Template de dados do autor (não versionado) | ⭐⭐⭐ CRÍTICO |

---

## 🔍 10. Tópicos Específicos Identificados

### Wallet Abstraction & Account Abstraction

-✅ **NeoTokenV2** (`architecture/specs/neotoken-v2.md`): Suporte nativo para Account Abstraction via EIP-2612 (ERC20Permit)
-✅ **Integração MiniApp** (`operations/guides/miniapp-integration.md`): Sistema de distribuição via bridgeMinter

### MPC & MCP

-✅ **Adendos Arquiteturais** (`architecture/ARCHITECTURAL_ADDENDUMS.md`): Postura técnica sobre MCP, MPC, wallet extensions
-✅ **AgentKit Guide** (`architecture/specs/base-agentkit-guide.md`): Integração com Coinbase AI Agent Kit

### Automação

-✅ **Surgical Architecture** (`architecture/surgical.md`): Descrição dos blocos de automação (smart-core, smart-cli, internal-ops)
-✅ **Operational Guide** (`operations/guides/operational-guide.md`): Automações operacionais
-✅ **CI Workflows** (`operations/deployment/ci-workflows.md`): Automação de CI/CD

### Governança

-✅ **Governance** (`core/governance.md`): Protocolo completo de governança
-✅ **Repository Visibility Policy** (`operations/standards/REPOSITORY_VISIBILITY_POLICY.md`): Política de exposição
-✅ **Workflow Baseline** (`operations/standards/workflow-baseline.md`): Padrões de workflow

---

## ⚠️ 11. Lacunas Identificadas

### Para o Pacote Mínimo de Registro

#### [PENDENTE] Documentos que Precisam ser Criados

1. **00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22.pdf**
   - Status: Não existe
   - Necessário: Índice do pacote com instruções de leitura

2. **01_CORE_Authorship_and_Prior_Art_v1.0_2026-01-22.pdf**
   - Status: Não existe
   - Necessário: Bloco jurídico de autoria e anterioridade
   - Dados necessários: Preenchidos no `AUTHOR_DATA_TEMPLATE.md`

3. **02_SYSTEM_Executable_Concept_Overview_v1.0_2026-01-22.pdf**
   - Status: Não existe
   - Necessário: Descrição funcional objetiva do sistema
   - Base disponível: `architecture/architecture.md`, `architecture/surgical.md`, `architecture/specs/neotoken-v2.md`

4. **03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt**
   - Status: Não existe
   - Necessário: Declaração resumida e hashable

5. **04_PROOF_SHA256_and_TXID_v1.0_2026-01-22.pdf**
   - Status: Não existe
   - Necessário: Tabela com SHA-256 e espaço para TXID

#### [PENDENTE] Documentos de Política

6. **SECURITY_Repo_Visibility_Policy_v1.0_2026-01-22.md**
   - Status: Existe versão similar (`operations/standards/REPOSITORY_VISIBILITY_POLICY.md`)
   - Necessário: Versão específica para o pacote de registro com orientações para IAs

7. **CHECKLIST_Release_Validation_2026-01-22.md**
   - Status: Não existe
   - Necessário: Checklist de validação anti-alucinação

### Informações Disponíveis vs Necessárias

#### ✅ Informações Disponíveis

-✅ Arquitetura completa do sistema
-✅ Especificações técnicas detalhadas
-✅ Políticas de segurança e visibilidade
-✅ Histórico de desenvolvimento
-✅ Prova histórica (repositório antigo identificado)
-✅ Dados do autor (preenchidos no template)

#### ⚠️ Informações que Precisam ser Extraídas/Sintetizadas

-⚠️ **Diagrama do sistema**: Precisa ser criado baseado em `architecture/surgical.md` e `architecture/architecture.md`
-⚠️ **Estado atual do projeto**: Precisa ser sintetizado de múltiplos documentos
-⚠️ **Diferenciais estruturais**: Precisa ser extraído e explicado tecnicamente (sem adjetivos)

---

## 📝 12. Notas de Mapeamento

### Estrutura Modular Identificada

A documentação confirma a arquitetura modular multi-repo:

```
NΞØ SMART FACTORY Ecosystem
│
├─ Core Layer (Blockchain)
│  └─ smart-core/ → Contratos, scripts, templates
│
├─ Interface Layer (User)
│  ├─ smart-ui/ → PWA, landing, formulário
│  └─ smart-cli/ → CLI universal (nsf)
│
├─ Intelligence Layer (AI)
│  ├─ smart-oracle/ → Refinamento via LLM (planejado)
│  └─ smart-cult/ → Geração de narrativa (planejado)
│
├─ Data Layer (Schema)
│  └─ smart-dna/ → Schema JSON + validação (planejado)
│
├─ Orchestration Layer (Automation)
│  └─ smart-kernel/ → Orquestrador 1-click (planejado)
│
└─ Documentation Layer
   └─ docs/ → Documentação viva
```

### Versões Identificadas

-**v0.5.1** - IGNIÇÃO (primeira versão funcional)
-**v0.5.3** - MULTICHAIN FOUNDATION (atual)
-**v1.0** - Pacote de registro (a ser criado)

### Tecnologias Principais

-**Blockchain**: Solidity ^0.8.20, Hardhat, OpenZeppelin Contracts v5.0
-**Redes**: Polygon, Base, Arbitrum (multichain)
-**Frontend**: Next.js 14, Tailwind CSS, Nuxt.js
-**CLI**: Node.js, Commander.js
-**Padrões**: ERC20, ERC721, EIP-2612 (Account Abstraction)

---

## ✅ 13. Conclusão do Inventário

### Documentos Relevantes Encontrados: 45+

### Categorias Cobertas:
-✅ Arquitetura e especificações técnicas
-✅ Governança e políticas
-✅ Operações e padrões
-✅ Estratégia e produto
-✅ Histórico e auditoria
-✅ Segurança e visibilidade
-✅ Prova histórica

### Próximos Passos:
1. ✅ Inventário completo
2. ⏳ Gerar pacote mínimo (Fase 2)
3. ⏳ Criar políticas de segurança específicas (Fase 3)
4. ⏳ Criar checklist de validação (Fase 4)

---

**Inventário realizado em**: 2026-01-22  
**Baseado em**: Varredura completa do repositório `docs`  
**Método**: Análise semântica + leitura direta de arquivos  
**Sem conjectura**: Apenas fatos encontrados nos documentos
