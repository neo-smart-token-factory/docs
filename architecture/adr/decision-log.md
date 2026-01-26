# Registro de Decisões Técnicas (ADR)

## ADR-001: Arquitetura Moderna (Factory) vs. Geradores Genéricos

**Data:** 20 de Janeiro de 2026
**Status:** Decidido e Implementado

### Contexto
O mercado de criação de tokens tem sido dominado por "Token Generators" (repositórios como `erc20-token-generator` ou variantes BEP20). Esses sistemas geralmente operam sob a lógica de um "Canivete Suíço": um único contrato massivo contendo todas as funcionalidades possíveis (Mintable, Burnable, Taxable, Pausable, etc.), ativadas ou desativadas por boolean flags (`if/else`).

Durante a concepção da **NΞØ SMART FACTORY**, avaliamos se deveríamos seguir esse padrão ou adotar uma abordagem diferente.

### Análise Técnica

#### 1. Abordagem "Generator" (Canivete Suíço)
*   **Prós:** Facilidade inicial de implementação (um contrato serve para tudo).
*   **Contras (Bloatware):** O contrato final carrega bytecode morto. Se você cria um token simples sem taxas, a lógica de taxas ainda existe no blockchain, consumindo espaço e aumentando o custo de deploy (gas).
*   **Risco de Segurança:** Uma vulnerabilidade em uma função não utilizada (ex: lógica de taxas) pode comprometer o contrato inteiro, mesmo que a flag de taxas esteja desligada.
*   **Auditoria:** Dificulta a auditoria, pois o auditor precisa validar todas as permutações possíveis de flags.

#### 2. Abordagem NΞØ (Factory Modular & Cirúrgica)
*   **Base:** OpenZeppelin Contracts v5.0 (Padrão Ouro).
*   **Estratégia:** Implementação "Vanilla".
*   **Lógica:** Em vez de um contrato gigante cheio de flags, a Factory seleciona e implementa apenas o que é necessário.
*   **Segurança:** Herança direta de contratos auditados. Se o token não tem taxas, o código de taxas **não existe** no contrato deployado.

### Decisão
Optamos pela **Abordagem NΞØ (Factory Modular)** baseada em OpenZeppelin.

**Justificativa:**
1.  **Eficiência de Gas:** Deploys mais baratos e limpos.
2.  **Segurança Superior:** Menor superfície de ataque (código morto = zero).
3.  **Profissionalismo:** Tokens gerados são "puros" (`contract Token is ERC20`), sem a estigma de "tokens de gerador" que muitas vezes são associados a scams ou projetos amadores.
4.  **Longevidade:** Manutenção simplificada por depender de padrões da indústria (OZ) e não de repositórios mantidos por indivíduos.

## ADR-002: Soberania Web3 (Raiz) vs. Managed SaaS (Thirdweb style)

**Data:** 20 de Janeiro de 2026
**Status:** Decidido

### Contexto
Plataformas como Thirdweb facilitam o deploy, mas muitas vezes criam uma dependência (lock-in) onde o controle do contrato ou sua interface depende de mensalidades ou infraestrutura proprietária ("SaaS Web3").

### Decisão
A **NΞØ SMART FACTORY** adota a filosofia **Web3 Raiz**.
1. **Zero Fees recorrentes:** O usuário é dono total do contrato; a fábrica é a ferramenta de forja, não o dono da bigorna.
2. **Código Aberto e Verificável:** Sem amarras em dashboards proprietários.
3. **Poder ao Criador:** Foco em ferramentas que o criador pode rodar localmente ou em sua própria infra (ex: internal-ops).

---

## ADR-003: Evolução para Smart Accounts e Multichain

**Data:** 20 de Janeiro de 2026
**Status:** Planejado

### Decisão
Integrar suporte nativo para:
1. **Account Abstraction (ERC-4337):** Wallets que não dependem de seed phrases puras.
2. **MPC (Multi-Party Computation):** Seguindo a tendência de wallets da BASE/Coinbase para onboarding em massa.
3. **Metamask Snaps:** Extensões da fábrica diretamente na wallet do usuário.
4. **Arquitetura Multichain:** Tokens que nascem preparados para pontes e presença em múltiplas redes simultaneamente.

---

## ADR-004: NeoTokenV2 — Multichain & Account Abstraction Ready

**Data:** 20 de Janeiro de 2026
**Status:** ✅ Implementado (v0.5.3)

### Contexto
Com a evolução do ecossistema Web3 para Account Abstraction (ERC-4337) e arquiteturas multichain, o `NeoTokenBase` original precisava evoluir para suportar:
- Transações gasless via ERC20Permit (EIP-2612)
- Mint cross-chain via bridges autorizadas
- Proteção anti-bot nativa
- Supply cap rígido

### Análise Técnica

#### Limitações do NeoTokenBase
- Sem suporte nativo para meta-transactions
- Sem preparação para operações cross-chain
- Proteção anti-bot dependente de implementação externa
- Supply cap configurável (não imutável)

#### Solução: NeoTokenV2
Evolução que mantém a filosofia "Vanilla" mas adiciona recursos essenciais para o ecossistema moderno:

1. **ERC20Permit (EIP-2612)**
   - Meta-transactions nativas via assinaturas off-chain
   - Compatível com Smart Wallets (Coinbase, Safe, Argent)
   - UX gasless para onboarding

2. **Bridge Minter Role**
   - Endereço autorizado para mint cross-chain
   - Preparado para LayerZero, Wormhole, Axelar
   - Validações de segurança (zero address, supply cap)

3. **Supply Cap Imutável**
   - `MAX_SUPPLY` constante de 1 bilhão
   - Verificação em `publicMint()` e `bridgeMint()`
   - Transparência e escassez garantidas

4. **Anti-bot Integrado**
   - Mapping `hasPublicMinted` (1 mint por wallet)
   - Proteção contra ataques sybil
   - Função `resetPublicMint()` para casos de emergência

5. **Eventos Completos**
   - `PublicMinted(minter, amount, pricePaid)`
   - `BridgeMinted(to, amount)`
   - Otimizado para indexadores (The Graph, Dune)

6. **Segurança Reforçada**
   - `withdraw()` usa `call{}` em vez de `transfer()`
   - Validações de zero address
   - Ownable2Step para transferência segura de ownership

### Decisão
Adotar **NeoTokenV2** como padrão para novos tokens que requerem:
- Account Abstraction
- Arquitetura Multichain
- Proteção anti-bot nativa
- Supply cap imutável

**NeoTokenBase** permanece disponível para casos de uso mais simples.

**Justificativa:**
1. **AA-Ready**: Suporte nativo para Smart Wallets sem dependências externas
2. **Multichain**: Arquitetura preparada para expansão cross-chain
3. **Segurança**: Padrões modernos (call{}, validações, eventos)
4. **DX**: View function `getContractInfo()` facilita integração frontend
5. **Compatibilidade**: Mantém herança OpenZeppelin v5.0 (auditado)

### Impacto
- ✅ Tokens criados são "future-proof" para AA e multichain
- ✅ Reduz necessidade de upgrades futuros
- ✅ Mantém filosofia "Vanilla" (sem bloatware)
- ✅ Facilita integração com wallets modernas

---

## ADR-005: Paridade de Stack (EVM ↔ TON)

**Data:** 25 de Janeiro de 2026
**Status:** ✅ Decidido e Implementado

### Contexto
Com a expansão para a rede TON, surgiu o desafio de manter a mesma proposta de valor da NΞØ SMART FACTORY em ecossistemas tecnicamente distintos (EVM/Solidity vs. TON/Tact/FunC). A fragmentação de funcionalidades entre redes prejudicaria a experiência do usuário e a integridade do protocolo.

### Decisão
Estabelecer o princípio de **Paridade de Funcionalidades**:
1. **Espelhamento de Lógica:** Todo recurso crítico implementado no EVM (como o Protocol Fee de 5%, Anti-bot, e Supply Cap) deve ter uma implementação equivalente em TON.
2. **Standardization de Comportamento:** Embora a linguagem mude (Solidity para FunC/Tact), o comportamento externo e as garantias de segurança devem ser idênticos.
3. **Mapeamento Técnico:** Criar e manter um documento de mapeamento (`EVM_TON_MAPPING.md`) que sirva como especificação para implementadores de novas chains.

### Justificativa
1. **Consistência de Marca:** O usuário recebe a mesma "Operação Cirúrgica" independente da chain.
2. **Segurança Unificada:** Auditorias e verificações podem seguir o mesmo checklist lógico.
3. **Multichain Real:** Facilita a criação de bridges e orquestradores que funcionam de forma previsível entre redes.

### Implementação
- Implementado em: `smart-core/contracts/ton/` (Jetton Factory, Minter, Wallet).
- Mapeamento detalhado: `docs/auditoria/EVM_TON_MAPPING.md`.

---

### 👤 Autoria

**Project Lead**: NODE NEØ  
**Email**: neo@neoprotocol.space  
**Web3 Identity**: neoprotocol.eth  
**NEØ PROTOCOL**: https://neoprotocol.space  
[![GitHub](https://img.shields.io/badge/GitHub-neo--smart--token--factory-181717?style=flat&logo=github)](https://github.com/neo-smart-token-factory)

> *Expand until silence becomes structure.*
