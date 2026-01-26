# NEOFLW MiniApp Integration Guide

## 🎯 Arquitetura de Distribuição

O NEOFLW opera em **modo bridgeMinter** para distribuição automatizada no Telegram MiniApp:

-❌ Mint público desabilitado (sem barreiras de wallet/gas)
-✅ Distribuição via backend controlado
-✅ Recompensas por engajamento (tarefas, referrals, streaks)

---

## 📐 Configuração Inicial

### 1. Criar Wallet Distribuidor

**Opção A - Hot Wallet Dedicado** (Recomendado para início)
```javascript
const { ethers } = require('ethers');

// Criar nova wallet APENAS para distribuição
const distributorWallet = ethers.Wallet.createRandom();

console.log('Address:', distributorWallet.address);
console.log('Private Key:', distributorWallet.privateKey);
// ⚠️ NUNCA exponha a private key - use secrets manager
```

**Opção B - Multi-Sig Safe** (Recomendado para produção)
```
Criar em: https://app.safe.global/
Configuração: 2/3 multi-sig
Signers: Você + 2 backups
```

### 2. Configurar no Contrato

No Basescan: https://basescan.org/address/0xF4Fbd30e3Ea69457adD30F7C3D6fde25f7D8Db26#writeContract

```solidity
// 1. Configurar bridge minter
setBridgeMinter("0xENDERECO_DO_DISTRIBUIDOR")

// 2. Desabilitar mint público
setPublicMintStatus(false)
```

### 3. Financiar Wallet Distribuidor

```bash
# Enviar ~0.003 ETH para gas
# Endereço: 0x... (do distribuidor)
```

---

## 🔧 Backend de Distribuição

### Estrutura de Arquivos

```
smart-core/scripts/miniapp/
├── distributor.js          # Lógica de distribuição
├── rewards-config.js       # Configuração de recompensas
├── validator.js            # Validação de tarefas
└── monitor.js             # Monitoramento de supply
```

### distributor.js

```javascript
/**
 * NEOFLW Distributor - MiniApp Rewards System
 * Distribui tokens NEOFLW para usuários do Telegram MiniApp
 */

const { ethers } = require('ethers');
require('dotenv').config();

// Configuração
const NEOFLW_ADDRESS = "0xF4Fbd30e3Ea69457adD30F7C3D6fde25f7D8Db26";
const DISTRIBUTOR_KEY = process.env.DISTRIBUTOR_PRIVATE_KEY;
const BASE_RPC = process.env.BASE_RPC;

// ABI mínimo necessário
const NEOFLW_ABI = [
  "function bridgeMint(address to, uint256 amount) external",
  "function totalSupply() view returns (uint256)",
  "function MAX_SUPPLY() view returns (uint256)",
  "function hasPublicMinted(address) view returns (bool)"
];

// Setup
const provider = new ethers.JsonRpcProvider(BASE_RPC);
const wallet = new ethers.Wallet(DISTRIBUTOR_KEY, provider);
const neoflw = new ethers.Contract(NEOFLW_ADDRESS, NEOFLW_ABI, wallet);

/**
 * Recompensa um usuário
 * @param {string} userAddress - Endereço da wallet do usuário
 * @param {string} taskType - Tipo de tarefa completada
 * @returns {Promise<string>} Transaction hash
 */
async function rewardUser(userAddress, taskType) {
  // Configuração de recompensas
  const REWARDS = {
    'daily_login': ethers.parseEther('10'),      // 10 NEOFLW
    'referral': ethers.parseEther('50'),         // 50 NEOFLW
    'task_complete': ethers.parseEther('25'),    // 25 NEOFLW
    'streak_7days': ethers.parseEther('100'),    // 100 NEOFLW
    'first_time': ethers.parseEther('5')         // 5 NEOFLW
  };
  
  const amount = REWARDS[taskType];
  if (!amount) throw new Error(`Invalid task type: ${taskType}`);
  
  // Validações
  if (!ethers.isAddress(userAddress)) {
    throw new Error('Invalid address');
  }
  
  // Verificar supply disponível
  const currentSupply = await neoflw.totalSupply();
  const maxSupply = await neoflw.MAX_SUPPLY();
  
  if (currentSupply + amount > maxSupply) {
    throw new Error('Max supply reached');
  }
  
  // Executar mint
  try {
    console.log(`🎁 Rewarding ${userAddress}: ${ethers.formatEther(amount)} NEOFLW (${taskType})`);
    
    const tx = await neoflw.bridgeMint(userAddress, amount);
    console.log(`⏳ Transaction sent: ${tx.hash}`);
    
    const receipt = await tx.wait();
    console.log(`✅ Confirmed in block ${receipt.blockNumber}`);
    
    return tx.hash;
  } catch (error) {
    console.error('❌ Mint failed:', error);
    throw error;
  }
}

/**
 * Batch reward - recompensa múltiplos usuários
 * @param {Array} rewards - Array de {address, taskType}
 */
async function batchReward(rewards) {
  const results = [];
  
  for (const reward of rewards) {
    try {
      const txHash = await rewardUser(reward.address, reward.taskType);
      results.push({ success: true, txHash, ...reward });
      
      // Delay entre transações para evitar nonce issues
      await new Promise(resolve => setTimeout(resolve, 2000));
    } catch (error) {
      results.push({ success: false, error: error.message, ...reward });
    }
  }
  
  return results;
}

/**
 * Obter estatísticas do contrato
 */
async function getStats() {
  const totalSupply = await neoflw.totalSupply();
  const maxSupply = await neoflw.MAX_SUPPLY();
  const utilizationRate = (totalSupply * 100n) / maxSupply;
  
  return {
    totalDistributed: ethers.formatEther(totalSupply),
    maxSupply: ethers.formatEther(maxSupply),
    utilizationRate: Number(utilizationRate),
    remaining: ethers.formatEther(maxSupply - totalSupply)
  };
}

module.exports = {
  rewardUser,
  batchReward,
  getStats
};
```

### rewards-config.js

```javascript
/**
 * Configuração de Recompensas e Gamificação
 */

const { ethers } = require('ethers');

// Recompensas base
const BASE_REWARDS = {
  daily_login: ethers.parseEther('10'),
  referral: ethers.parseEther('50'),
  task_complete: ethers.parseEther('25'),
  streak_7days: ethers.parseEther('100'),
  streak_30days: ethers.parseEther('500'),
  first_time: ethers.parseEther('5')
};

// Sistema de níveis
const REWARD_TIERS = {
  bronze: { 
    multiplier: 1, 
    dailyLimit: ethers.parseEther('100'),
    minPoints: 0
  },
  silver: { 
    multiplier: 1.5, 
    dailyLimit: ethers.parseEther('200'),
    minPoints: 1000
  },
  gold: { 
    multiplier: 2, 
    dailyLimit: ethers.parseEther('500'),
    minPoints: 5000
  },
  platinum: {
    multiplier: 3,
    dailyLimit: ethers.parseEther('1000'),
    minPoints: 10000
  }
};

/**
 * Calcula recompensa com multiplicador de tier
 */
function calculateReward(taskType, userTier = 'bronze') {
  const baseAmount = BASE_REWARDS[taskType];
  if (!baseAmount) return 0n;
  
  const tier = REWARD_TIERS[userTier];
  const multiplier = BigInt(Math.floor(tier.multiplier * 100));
  
  return (baseAmount * multiplier) / 100n;
}

/**
 * Valida se usuário pode receber recompensa
 */
function canReceiveReward(userStats, taskType, amount) {
  const tier = getUserTier(userStats.points);
  const dailyLimit = REWARD_TIERS[tier].dailyLimit;
  
  if (userStats.dailyTotal + amount > dailyLimit) {
    return { allowed: false, reason: 'Daily limit exceeded' };
  }
  
  return { allowed: true };
}

/**
 * Determina tier do usuário baseado em pontos
 */
function getUserTier(points) {
  if (points >= REWARD_TIERS.platinum.minPoints) return 'platinum';
  if (points >= REWARD_TIERS.gold.minPoints) return 'gold';
  if (points >= REWARD_TIERS.silver.minPoints) return 'silver';
  return 'bronze';
}

module.exports = {
  BASE_REWARDS,
  REWARD_TIERS,
  calculateReward,
  canReceiveReward,
  getUserTier
};
```

### validator.js

```javascript
/**
 * Validador de Tarefas e Anti-Abuse
 */

const crypto = require('crypto');

class RewardValidator {
  constructor(database) {
    this.db = database;
    this.rateLimiter = new Map();
  }
  
  /**
   * Valida se usuário pode receber recompensa
   */
  async validateReward(userId, taskType, walletAddress) {
    // 1. Verificar rate limiting
    if (!this.checkRateLimit(userId, taskType)) {
      return { valid: false, reason: 'Rate limit exceeded' };
    }
    
    // 2. Verificar se tarefa já foi recompensada
    const alreadyClaimed = await this.db.checkClaimed(userId, taskType);
    if (alreadyClaimed) {
      return { valid: false, reason: 'Already claimed' };
    }
    
    // 3. Verificar se tarefa foi realmente completada
    const taskCompleted = await this.db.verifyTaskCompletion(userId, taskType);
    if (!taskCompleted) {
      return { valid: false, reason: 'Task not completed' };
    }
    
    // 4. Verificar wallet ownership
    const walletValid = await this.verifyWalletOwnership(userId, walletAddress);
    if (!walletValid) {
      return { valid: false, reason: 'Wallet not verified' };
    }
    
    return { valid: true };
  }
  
  /**
   * Rate limiting por usuário/tarefa
   */
  checkRateLimit(userId, taskType) {
    const key = `${userId}:${taskType}`;
    const now = Date.now();
    const lastClaim = this.rateLimiter.get(key);
    
    // Limites por tipo de tarefa
    const COOLDOWNS = {
      daily_login: 24 * 60 * 60 * 1000,  // 24h
      task_complete: 60 * 60 * 1000,     // 1h
      referral: 0                         // sem cooldown
    };
    
    const cooldown = COOLDOWNS[taskType] || 0;
    
    if (lastClaim && (now - lastClaim) < cooldown) {
      return false;
    }
    
    this.rateLimiter.set(key, now);
    return true;
  }
  
  /**
   * Verifica ownership da wallet (assinatura)
   */
  async verifyWalletOwnership(userId, walletAddress) {
    // Usuário deve ter assinado uma mensagem provando ownership
    const signature = await this.db.getWalletSignature(userId);
    if (!signature) return false;
    
    // Verificar assinatura
    const message = `I own this wallet for NEOFLW rewards: ${userId}`;
    const recoveredAddress = ethers.verifyMessage(message, signature);
    
    return recoveredAddress.toLowerCase() === walletAddress.toLowerCase();
  }
}

module.exports = RewardValidator;
```

### monitor.js

```javascript
/**
 * Monitor de Supply e Alertas
 */

const { ethers } = require('ethers');

class SupplyMonitor {
  constructor(contractAddress, provider) {
    this.contract = new ethers.Contract(
      contractAddress,
      ["function totalSupply() view returns (uint256)", "function MAX_SUPPLY() view returns (uint256)"],
      provider
    );
    this.alerts = [];
  }
  
  async checkSupply() {
    const totalSupply = await this.contract.totalSupply();
    const maxSupply = await this.contract.MAX_SUPPLY();
    const utilizationRate = (totalSupply * 100n) / maxSupply;
    
    const stats = {
      totalSupply: ethers.formatEther(totalSupply),
      maxSupply: ethers.formatEther(maxSupply),
      utilizationRate: Number(utilizationRate),
      timestamp: new Date().toISOString()
    };
    
    // Alertas
    if (utilizationRate >= 90n) {
      this.sendAlert('CRITICAL', 'Supply at 90%', stats);
    } else if (utilizationRate >= 75n) {
      this.sendAlert('WARNING', 'Supply at 75%', stats);
    } else if (utilizationRate >= 50n) {
      this.sendAlert('INFO', 'Supply at 50%', stats);
    }
    
    return stats;
  }
  
  sendAlert(level, message, data) {
    const alert = { level, message, data, timestamp: new Date() };
    this.alerts.push(alert);
    console.log(`🚨 [${level}] ${message}`, data);
    
    // Aqui você pode integrar com:
    // - Telegram Bot (notificação)
    // - Discord Webhook
    // - Email
    // - Sentry/Monitoring service
  }
  
  getAlerts() {
    return this.alerts;
  }
}

module.exports = SupplyMonitor;
```

---

## 🌐 API Endpoints (Express.js)

```javascript
const express = require('express');
const { rewardUser, getStats } = require('./distributor');
const RewardValidator = require('./validator');

const app = express();
app.use(express.json());

const validator = new RewardValidator(database);

// Endpoint de recompensa
app.post('/api/reward', async (req, res) => {
  try {
    const { userId, walletAddress, taskType } = req.body;
    
    // Validar requisição
    const validation = await validator.validateReward(userId, taskType, walletAddress);
    if (!validation.valid) {
      return res.status(400).json({ error: validation.reason });
    }
    
    // Distribuir recompensa
    const txHash = await rewardUser(walletAddress, taskType);
    
    // Registrar no banco
    await database.recordReward(userId, taskType, txHash);
    
    res.json({ 
      success: true, 
      txHash,
      explorer: `https://basescan.org/tx/${txHash}`
    });
  } catch (error) {
    console.error('Reward error:', error);
    res.status(500).json({ error: error.message });
  }
});

// Endpoint de estatísticas
app.get('/api/stats', async (req, res) => {
  const stats = await getStats();
  res.json(stats);
});

app.listen(3000, () => console.log('🚀 Distributor API running on port 3000'));
```

---

## 🔐 Segurança

### .env.example
```bash
# Base Network
BASE_RPC=https://your-quicknode-url
DISTRIBUTOR_PRIVATE_KEY=0x...

# Database
DATABASE_URL=postgresql://...

# Monitoring
TELEGRAM_BOT_TOKEN=...
ALERT_WEBHOOK=...
```

### Checklist de Segurança
-[ ] Private key em secrets manager (nunca em código)
-[ ] Rate limiting implementado
-[ ] Validação server-side de todas as tarefas
-[ ] Wallet ownership verificado (assinatura)
-[ ] Monitoramento de supply ativo
-[ ] Logs de todas as distribuições
-[ ] Backup da wallet distribuidor

---

## 📊 Dashboard de Monitoramento

```javascript
// Métricas em tempo real
setInterval(async () => {
  const stats = await getStats();
  console.log(`
📊 NEOFLW Distribution Stats
━━━━━━━━━━━━━━━━━━━━━━━━━━
Total Distributed: ${stats.totalDistributed} NEOFLW
Utilization: ${stats.utilizationRate}%
Remaining: ${stats.remaining} NEOFLW
━━━━━━━━━━━━━━━━━━━━━━━━━━
  `);
}, 60000); // A cada 1 minuto
```

---

## ✅ Próximos Passos

1. **Criar wallet distribuidor**
2. **Configurar `setBridgeMinter` no contrato**
3. **Desabilitar `publicMintEnabled`**
4. **Implementar backend de recompensas**
5. **Testar com endereço dummy**
6. **Deploy em produção**

---

**Documentação:** NΞØ SMART FACTORY v0.5.3  
**Contrato:** 0xF4Fbd30e3Ea69457adD30F7C3D6fde25f7D8Db26  
**Network:** Base Mainnet

*Expand until silence becomes structure.*
