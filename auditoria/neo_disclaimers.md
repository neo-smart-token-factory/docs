# NΞØ SMART FACTORY — Disclaimers v0.5.1 IGNIÇÃO

> **Leia com atenção antes de usar**

---

## ⚠️ Status do Projeto

### Este é um projeto ALPHA

A NΞØ SMART FACTORY v0.5.1 está em **desenvolvimento ativo**.

**O que isso significa:**

- ✅ O core funciona e está estável
- ⚠️ Nem todas as features prometidas estão implementadas
- ⚠️ Bugs podem ocorrer
- ⚠️ Breaking changes podem acontecer entre versões
- ⚠️ Documentação pode estar desatualizada

**O que você deve fazer:**

- 🧪 Sempre teste em **testnet** primeiro (Polygon Mumbai ou Amoy)
- 📖 Leia a documentação antes de usar
- 🐛 Reporte bugs no GitHub
- 💬 Entre no Discord para suporte da comunidade

---

## 🔍 Funcionalidades — O que está disponível

### ✅ Implementado e Funcional

| Feature | Status | Descrição |
|---------|--------|-----------|
| **Deploy ERC20** | ✅ Funcional | Deploy automatizado de tokens na Polygon |
| **Contratos Base** | ✅ Funcional | `NeoTokenBase`, `IgnitionToken`, `NeoSmartFactory` |
| **CLI** | ✅ Funcional | Comandos `init` e `deploy` |
| **UI Básica** | ✅ Funcional | Landing page e formulário de criação |
| **Simulação** | ✅ Funcional | Validação pré-deploy com `NEO::simulate` |
| **Templates** | ✅ Funcional | Contratos e documentos customizáveis |
| **Verificação** | ✅ Funcional | Verificação automática no Polygonscan |

### 🔨 Em Desenvolvimento (Roadmap)

| Feature | Versão | Previsão | Descrição |
|---------|--------|----------|-----------|
| **Oracle Inteligente** | v0.6.0 | Fev 2025 | Refinamento via LLM |
| **DNA Completo** | v0.6.0 | Fev 2025 | Campos avançados (archetype, energy, ecosystem) |
| **Geração de Manifesto** | v0.7.0 | Mar 2025 | Automático via `forge-cult` |
| **Geração de Whitepaper** | v0.7.0 | Mar 2025 | Automático via `forge-cult` |
| **Kernel Automatizado** | v0.8.0 | Abr 2025 | "One-click deployment" |
| **Marketplace de Templates** | v1.0.0 | Mai 2025 | Comunidade de criadores |

### ❌ Não Implementado (Futuro)

- Integração com Safe (smart wallet)
- Storage descentralizado (Arweave)
- Sistema de badges/XP
- Rituais de comunidade
- Anti-Sybil automático
- Gamificação completa

---

## 🔐 Segurança — Responsabilidades

### ⚠️ IMPORTANTE: Você é responsável pelo seu deploy

**O que a NΞØ SMART FACTORY faz:**

- ✅ Fornece contratos base auditáveis
- ✅ Valida configurações básicas
- ✅ Detecta problemas comuns
- ✅ Fornece templates seguros

**O que a NΞØ SMART FACTORY NÃO faz:**

- ❌ Não garante que seu token terá sucesso
- ❌ Não audita código customizado que você adicionar
- ❌ Não se responsabiliza por configurações erradas
- ❌ Não oferece consultoria financeira ou legal

### Recomendações de Segurança

#### 1. **Teste em Testnet**
```bash
# Configure para Mumbai/Amoy primeiro
RPC_URL=https://rpc-mumbai.maticvigil.com
neo-smart-factory deploy
```

#### 2. **Revise Contratos**
- Leia o código gerado antes de deployar
- Entenda o que cada função faz
- Verifique permissões e roles

#### 3. **Proteja sua Private Key**
- Nunca commite `.env` no Git
- Use hardware wallet para mainnet
- Considere usar Safe/Gnosis para contratos importantes

#### 4. **Auditoria Externa**
Para projetos com valor significativo:
- Contrate auditoria profissional
- Use ferramentas como Slither, Mythril
- Peça code review de devs experientes

---

## 💰 Custos — Transparência Total

### Custos Conhecidos

| Item | Valor Estimado | Frequência |
|------|----------------|------------|
| **Gas fee (deploy)** | ~$0.10 - $1.00 | Uma vez |
| **Gas fee (verify)** | ~$0.05 - $0.20 | Uma vez |
| **RPC (Alchemy free)** | Grátis | Até 300M requests/mês |
| **NΞØ SMART FACTORY** | Grátis (v0.5.1) | - |

### Custos Futuros (Possíveis)

A partir de versões futuras, **podem** ser cobrados:
- 🔮 Planos premium para Oracle avançado
- 🔮 Geração avançada de documentos (Cult)
- 🔮 Suporte prioritário
- 🔮 Templates premium na marketplace

**Compromisso:**
- ✅ Core sempre open source e gratuito
- ✅ Self-hosted sempre possível
- ✅ Transparência sobre preços futuros

---

## 🌐 Blockchain & Redes

### Redes Suportadas

| Rede | Status | RPC Recomendado |
|------|--------|-----------------|
| **Polygon Mainnet** | ✅ Suportado | Alchemy, Infura, QuickNode |
| **Polygon Mumbai** | ✅ Suportado (testnet) | Alchemy, public RPC |
| **Polygon Amoy** | ✅ Suportado (testnet) | Alchemy, public RPC |
| **Ethereum** | ⚠️ Experimental | Alchemy (gas alto!) |
| **Outras EVMs** | 🔜 Futuro | - |

### Limitações Conhecidas

**Polygon:**
- ⚠️ Ocasionalmente há congestionamento (gas fee sobe)
- ⚠️ RPC público pode ter rate limit
- ✅ Geralmente estável e barato

**Ethereum:**
- ⚠️ Gas fees muito altos ($50-$200 por deploy)
- ⚠️ Não recomendado para testes
- ⚠️ Use apenas para projetos sérios

---

## 📜 Aspectos Legais

### ⚠️ Não somos advogados

**Este software não oferece:**
- ❌ Consultoria jurídica
- ❌ Consultoria fiscal
- ❌ Consultoria financeira
- ❌ Garantias de compliance regulatório

### Sua Responsabilidade

Ao usar a NΞØ SMART FACTORY, você é responsável por:

1. **Compliance Legal**
   - Verificar leis de securities no seu país
   - Verificar leis de AML/KYC
   - Consultar advogado se necessário

2. **Aspectos Fiscais**
   - Declarar tokens criados
   - Pagar impostos devidos
   - Manter registros adequados

3. **Uso Ético**
   - Não criar tokens fraudulentos
   - Não fazer promessas falsas
   - Ser transparente com sua comunidade

### Proibições

**NÃO use esta ferramenta para:**
- ❌ Criar scams ou rug pulls
- ❌ Fraudes financeiras
- ❌ Lavagem de dinheiro
- ❌ Violação de propriedade intelectual
- ❌ Qualquer atividade ilegal

**Consequências:**
- Bannimento da plataforma
- Reporte às autoridades se necessário
- Ações legais cabíveis

---

## 🐛 Bugs & Limitações Conhecidas

### Bugs Conhecidos (v0.5.1)

| Bug | Impacto | Workaround | Fix Previsto |
|-----|---------|------------|--------------|
| `.env` não carrega automaticamente | Baixo | Configurar manualmente | v0.6.0 |
| Verificação falha em alguns RPC | Médio | Usar Alchemy | v0.5.2 |
| UI não valida campos vazios | Baixo | Validar manualmente | v0.6.0 |
| Simulação não detecta todos os erros | Médio | Revisar manualmente | v0.6.0 |

### Limitações de Design

**CLI:**
- Requer Node.js 18+
- Não funciona no Windows sem WSL
- Não tem interface gráfica

**UI:**
- Não salva progresso automaticamente
- Não tem sistema de autenticação
- Não sincroniza entre dispositivos

**Contratos:**
- ERC20 básico apenas (sem ERC721, ERC1155)
- Sem upgradability (proxy pattern)
- Sem governança avançada

---

## 📊 Dados & Privacidade

### O que coletamos

**Atualmente:**
- ❌ Nenhum dado pessoal
- ❌ Nenhuma telemetria
- ❌ Nenhum analytics

**Futuro (com opt-in):**
- 🔮 Analytics anônimo de uso
- 🔮 Logs de erro (se autorizado)
- 🔮 Estatísticas de deploy (públicas)

### O que NUNCA coletaremos

- ❌ Private keys
- ❌ Senhas
- ❌ Informações financeiras pessoais
- ❌ Dados sensíveis

---

## 🛟 Suporte & Comunidade

### O que oferecemos

**Grátis:**
- ✅ Documentação completa
- ✅ Exemplos e tutoriais
- ✅ Suporte da comunidade no Discord
- ✅ Issues no GitHub
- ✅ Respostas em 24-48h (best effort)

**NÃO oferecemos:**
- ❌ Suporte 24/7
- ❌ SLA garantido
- ❌ Consultoria personalizada (por enquanto)
- ❌ Reembolsos (software gratuito)

### Onde buscar ajuda

1. **Documentação**: Leia primeiro em [docs]
2. **Discord**: Comunidade ativa
3. **GitHub Issues**: Bugs e features
4. **GitHub Discussions**: Dúvidas gerais

---

## 🔄 Atualizações & Breaking Changes

### Como funciona

**Versionamento:**
- Seguimos Semantic Versioning (semver)
- `v0.x.x` = Alpha/Beta (pode ter breaking changes)
- `v1.x.x` = Estável (breaking changes apenas em major)

**Breaking Changes:**
- Sempre anunciados com 2 semanas de antecedência
- Migration guide fornecido
- Versão antiga suportada por 1 mês

**Como se manter atualizado:**
- 📢 Siga no Twitter/X
- 📧 Assine newsletter (futuro)
- ⭐ Watch no GitHub

---

## ✅ Checklist — Antes de Usar

### Pré-requisitos Técnicos

- [ ] Node.js 18+ instalado
- [ ] Git instalado
- [ ] MetaMask ou outra wallet configurada
- [ ] MATIC para gas fees (testnet ou mainnet)
- [ ] Conta no Alchemy/Infura (RPC)

### Conhecimento Necessário

- [ ] Entendo o que é blockchain
- [ ] Sei o que é um smart contract
- [ ] Entendo tokens ERC20
- [ ] Sei usar linha de comando básica
- [ ] Entendo os riscos de crypto

### Responsabilidades

- [ ] Li este documento completo
- [ ] Entendo que estou em ambiente alpha
- [ ] Vou testar em testnet primeiro
- [ ] Não vou culpar a ferramenta por meus erros
- [ ] Entendo que não há garantias

---

## 📞 Contato

**Problemas de segurança:**
- 🔒 Email: security@neosmart.factory
- 🔒 Reporte via GitHub (private security advisory)

**Outros contatos:**
- 💬 Discord: [servidor]
- 🐦 Twitter/X: [@neosmart_factory]
- 📧 Email: team@neosmart.factory
- 🐙 GitHub: [repositório]

---

## 📝 Termo de Uso Simplificado

**Ao usar a NΞØ SMART FACTORY, você concorda que:**

1. O software é fornecido "as is", sem garantias
2. Você é responsável por seus deploys e contratos
3. Você usará a ferramenta de forma ética e legal
4. Você entende os riscos de blockchain e crypto
5. Você não nos responsabilizará por perdas ou danos

**Licença:** MIT License (código aberto)

---

## 🔥 Mensagem Final

A NΞØ SMART FACTORY é uma ferramenta **poderosa**.

Com grande poder vem grande responsabilidade.

Use com sabedoria.  
Teste antes de deployar.  
Seja transparente com sua comunidade.

E lembre-se: **você não está sozinho**.

A comunidade está aqui para ajudar.

---

*NΞØ SMART FACTORY v0.5.1 — IGNIÇÃO*  
*Última atualização: 17 de Novembro de 2025*

**Por qualquer dúvida, leia este documento novamente. 90% das perguntas estão respondidas aqui.**