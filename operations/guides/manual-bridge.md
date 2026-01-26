# NΞØ SMART FACTORY — Manual Bridge System

> **Sistema de Bridge Manual com Multi-Sig para NeoTokenV2**  
> Versão: v0.5.3 — MULTICHAIN FOUNDATION

---

## 🌉 Visão Geral

O **Manual Bridge System** é uma solução pragmática e segura para permitir transferências cross-chain de tokens NeoTokenV2 sem dependências de protocolos externos caros (LayerZero, Wormhole, etc).

### Características

-✅ **Multi-Sig**: Validação por múltiplos signers (2/3, 3/5, etc)
-✅ **Replay Protection**: Previne ataques de replay com nonces únicos
-✅ **Low Cost**: ~50k gas por bridge (vs ~300k+ em protocolos externos)
-✅ **Self-Sovereign**: Sem dependências externas ou taxas recorrentes
-✅ **Automated**: Scripts Node.js para monitoramento e relay automático

---

## 📁 Estrutura

```
smart-core/
├── contracts/
│   └── bridge/
│       ├── ManualBridge.sol       # Contrato principal de bridge
│       └── BridgeValidator.sol    # Biblioteca de validação
│
└── scripts/
    └── bridge/
        ├── monitor.js             # Monitora eventos de lock
        ├── sign-proof.js          # Assina provas (multi-sig)
        └── relay.js               # Relay automático para chain destino
```

---

## 🔧 Como Funciona

### Fluxo Completo

```
┌─────────────┐                  ┌──────────────┐                  ┌─────────────┐
│  Chain A    │                  │   Backend    │                  │  Chain B    │
│  (Polygon)  │                  │   (Node.js)  │                  │   (Base)    │
└──────┬──────┘                  └──────┬───────┘                  └──────┬──────┘
       │                                │                                 │
       │ 1. lockTokens()                │                                 │
       │────────────────────────────>   │                                 │
       │                                │                                 │
       │ 2. Event: TokenLocked          │                                 │
       │────────────────────────────>   │                                 │
       │                                │                                 │
       │                                │ 3. Monitor detecta              │
       │                                │    Gera bridgeId                │
       │                                │    Assina com signers (2/3)     │
       │                                │                                 │
       │                                │ 4. bridgeWithProof()            │
       │                                │─────────────────────────────────>
       │                                │                                 │
       │                                │                                 │ 5. Valida assinaturas
       │                                │                                 │    Minta tokens
       │                                │                                 │
       │                                │         6. Event: TokenBridged  │
       │                                │<─────────────────────────────────
```

### Etapas Detalhadas

1. **Lock (Chain A)**
   - Usuário chama `lockTokens(token, to, amount, targetChainId)`
   - Tokens são transferidos para o bridge
   - Evento `TokenLocked` é emitido

2. **Monitoramento (Backend)**
   - Script `monitor.js` detecta evento
   - Gera `bridgeId` único
   - Assina com chave privada do signer

3. **Multi-Sig (Backend)**
   - Múltiplos signers assinam a mesma prova
   - Provas são armazenadas em `./bridge-proofs/`

4. **Relay (Chain B)**
   - Script `relay.js` submete prova + assinaturas
   - Contrato valida assinaturas
   - Tokens são mintados para o destinatário

---

## 🚀 Setup

### 1. Deploy dos Contratos

```bash
# Deploy ManualBridge na Polygon
npx hardhat run scripts/deploy-bridge.js --network polygon

# Deploy ManualBridge na Base
npx hardhat run scripts/deploy-bridge.js --network base
```

### 2. Configurar Signers

```solidity
// Adicionar signers autorizados (multi-sig 2/3)
await bridge.addSigner("0xSigner1Address");
await bridge.addSigner("0xSigner2Address");
await bridge.addSigner("0xSigner3Address");
await bridge.setRequiredSignatures(2); // 2 de 3
```

### 3. Configurar Tokens Suportados

```solidity
// Adicionar token NeoTokenV2
await bridge.addSupportedToken("0xTokenAddress");

// Configurar bridge como bridgeMinter no token
await token.setBridgeMinter("0xBridgeAddress");
```

### 4. Configurar Backend

```bash
# Instalar dependências
cd smart-core/scripts/bridge
npm install ethers

# Configurar variáveis de ambiente
cat > .env << EOF
# RPCs
POLYGON_RPC=https://polygon-rpc.com
BASE_RPC=https://mainnet.base.org

# Endereços dos bridges
POLYGON_BRIDGE_ADDRESS=0x...
BASE_BRIDGE_ADDRESS=0x...

# Chaves privadas (signers)
BRIDGE_SIGNER_KEY=0x...
BRIDGE_SIGNER_KEY_2=0x...
BRIDGE_SIGNER_KEY_3=0x...

# Chave do relayer
BRIDGE_RELAYER_KEY=0x...
EOF
```

### 5. Iniciar Monitoramento

```bash
# Terminal 1: Monitor (detecta locks e gera provas)
node monitor.js

# Terminal 2: Relay (submete provas para chain destino)
# Modo manual
node relay.js all

# Ou configurar cron job para relay automático
*/5 * * * * cd /path/to/smart-core/scripts/bridge && node relay.js all
```

---

## 💼 Uso

### Para Usuários (Frontend)

```javascript
// 1. Aprovar tokens
await token.approve(bridgeAddress, amount);

// 2. Lock tokens para bridge
await bridge.lockTokens(
    tokenAddress,      // Token a ser bridgeado
    destinationAddress, // Endereço na chain destino
    amount,            // Quantidade
    8453,              // Chain ID destino (Base)
    { value: bridgeFee } // Fee do bridge
);

// 3. Aguardar processamento (5-10 minutos)
// Tokens aparecerão automaticamente na chain destino
```

### Para Operadores (Backend)

```bash
# Monitorar eventos
node monitor.js

# Assinar prova manualmente
node sign-proof.js sign ./bridge-proofs/0x123...abc.json

# Relay de prova específica
node relay.js single 0x123...abc

# Relay de todas as provas pendentes
node relay.js all
```

---

## 🔒 Segurança

### Multi-Sig

-**Mínimo 2 assinaturas** necessárias
-Configuração recomendada: **2/3** ou **3/5**
-Signers devem ser endereços independentes

### Replay Protection

-Cada bridge tem `bridgeId` único
-Mapping `processedBridges` previne duplicação
-Nonces por usuário previnem colisões

### Validações

-✅ Zero address checks
-✅ Chain ID validation
-✅ Amount > 0
-✅ Token suportado
-✅ Assinaturas válidas
-✅ Sem duplicatas de assinatura

---

## 💰 Custos

### Gas Costs (Estimativa)

| Operação | Chain A (Lock) | Chain B (Mint) |
|----------|----------------|----------------|
| lockTokens | ~80k gas | - |
| bridgeWithProof (2 sigs) | - | ~120k gas |
| bridgeWithProof (3 sigs) | - | ~150k gas |

**Total**: ~200k-230k gas por bridge completa

### Comparação com Protocolos Externos

| Protocolo | Gas Cost | Taxas Extras | Setup |
|-----------|----------|--------------|-------|
| **Manual Bridge** | ~200k | Bridge fee (configurável) | Self-hosted |
| LayerZero | ~300k+ | $0.10-$1.00 | Integração complexa |
| Wormhole | ~400k+ | $0.50-$2.00 | Guardians externos |
| Axelar | ~350k+ | $0.20-$1.50 | Validators externos |

**Economia**: 30-50% em gas + sem taxas de protocolo

---

## 📊 Monitoramento

### Logs do Monitor

```
🌉 Bridge Monitor iniciado...
Monitorando chains: polygon, base
polygon: Bloco inicial 52847392
base: Bloco inicial 10234567

🔍 polygon: 1 evento(s) de lock encontrado(s)

📦 Lock detectado:
   Chain: polygon → Chain ID 8453
   Token: 0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb
   From: 0x1234...5678
   To: 0xabcd...ef01
   Amount: 1000.0
   Tx: 0x9876...5432

✅ Prova gerada e salva: 0xabc123...def456
```

### Logs do Relay

```
🚀 Iniciando relay de provas...

📋 3 prova(s) encontrada(s)

🔄 Processando prova:
   Bridge ID: 0xabc123...def456
   Target Chain: 8453
   Assinaturas: 2
   ⛽ Gas estimado: 145234
   📤 Submetendo transação...
   🔗 Tx Hash: 0xdef456...abc123
   ⏳ Aguardando confirmação...
   ✅ Bridge concluída! Block: 10234789

✅ Relay concluído
```

---

## 🛠️ Troubleshooting

### Problema: "Not enough signatures"

**Solução**: Adicione mais assinaturas à prova

```bash
node sign-proof.js sign ./bridge-proofs/0x123...abc.json $SIGNER_KEY_2
node sign-proof.js sign ./bridge-proofs/0x123...abc.json $SIGNER_KEY_3
```

### Problema: "Bridge already processed"

**Solução**: Prova já foi processada, verificar na chain destino

```bash
# Verificar se tokens foram mintados
cast call $TOKEN_ADDRESS "balanceOf(address)(uint256)" $USER_ADDRESS --rpc-url $BASE_RPC
```

### Problema: "Token not supported"

**Solução**: Adicionar token ao bridge

```bash
cast send $BRIDGE_ADDRESS "addSupportedToken(address)" $TOKEN_ADDRESS --private-key $OWNER_KEY
```

---

## 🗺️ Roadmap

### Fase 1: Manual (✅ Implementado)
-[x] Contrato ManualBridge
-[x] Scripts de monitoramento
-[x] Multi-sig validation
-[x] Relay automático

### Fase 2: UI (🔨 Próximo)
-[ ] Interface web para bridge
-[ ] Status tracking em tempo real
-[ ] Histórico de bridges
-[ ] Estimativa de tempo

### Fase 3: Otimizações (📋 Futuro)
-[ ] Batch processing (múltiplas bridges em 1 tx)
-[ ] Merkle proofs para reduzir gas
-[ ] Suporte a mais chains (Arbitrum, Optimism)

---

## 📚 Referências

### Contratos
-`ManualBridge.sol` — Contrato principal
-`BridgeValidator.sol` — Biblioteca de validação
-`NeoTokenV2.sol` — Token com suporte a bridge

### Scripts
-`monitor.js` — Monitoramento de eventos
-`sign-proof.js` — Assinatura de provas
-`relay.js` — Relay automático

---

**Versão**: v0.5.3 — MULTICHAIN FOUNDATION  
**License**: MIT

---

### 👤 Autoria

**Project Lead**: NODE NEØ  
**Email**: neo@neoprotocol.space  
**Web3 Identity**: neoprotocol.eth  
**NEØ PROTOCOL**: https://neoprotocol.space  
[![GitHub](<https://img.shields.io/badge/GitHub-neo--smart--token--factory-181717?style=flat&logo=github>)](https://github.com/neo-smart-token-factory)

> *Expand until silence becomes structure.*
