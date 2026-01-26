# 🤖 Guia: Coinbase AI Agent Kit - Base Network

## 📋 Visão Geral

Este guia mostra como usar o **Coinbase AI Agent Kit** para interagir com a rede Base, incluindo envio de ETH, deploy de contratos e outras operações.

## 🔧 Instalação

### 1. Instalar Dependências

```bash
npm install @coinbase/coinbase-sdk dotenv
```

### 2. Configurar Variáveis de Ambiente

Crie ou edite o arquivo `.env` na raiz do projeto:

```bash
# ========================================
# COINBASE AI AGENT KIT - BASE NETWORK
# ========================================

# Coinbase CDP API Credentials
# Obtenha em: https://portal.cdp.coinbase.com/
CDP_API_KEY_NAME=your_api_key_name_here
CDP_API_KEY_PRIVATE_KEY=your_private_key_here

# Network Configuration
NETWORK_ID=base-mainnet  # ou base-sepolia para testnet

# Wallet Configuration (opcional - será criada automaticamente se não existir)
WALLET_DATA=./wallet_data.json
```

## 📝 Como Obter as Credenciais

### Passo 1: Criar Conta no Coinbase Developer Platform

1. Acesse: https://portal.cdp.coinbase.com/
2. Crie uma conta ou faça login
3. Navegue até "API Keys"

### Passo 2: Criar API Key

1. Clique em "Create API Key"
2. Dê um nome descritivo (ex: "NEO Smart Factory Agent")
3. Selecione as permissões necessárias:
   - ✅ `wallet:read`
   - ✅ `wallet:write`
   - ✅ `wallet:transfer`
4. Clique em "Create"

### Passo 3: Salvar Credenciais

⚠️ **IMPORTANTE**: Salve as credenciais imediatamente! Elas só serão mostradas uma vez.

-`CDP_API_KEY_NAME`: Nome da API Key
-`CDP_API_KEY_PRIVATE_KEY`: Chave privada (formato JSON ou string)

## 💸 Enviar 0,003 ETH

### Opção 1: Script Simples

Crie o arquivo `scripts/send-eth-agentkit.js`:

```javascript
require('dotenv').config();
const { Coinbase, Wallet } = require('@coinbase/coinbase-sdk');

async function sendETH() {
  try {
    console.log('🚀 Inicializando Coinbase Agent Kit...\n');

    // Configurar Coinbase SDK
    Coinbase.configure({
      apiKeyName: process.env.CDP_API_KEY_NAME,
      privateKey: process.env.CDP_API_KEY_PRIVATE_KEY,
    });

    console.log('✅ SDK configurado com sucesso!\n');

    // Criar ou importar wallet
    let wallet;
    try {
      // Tentar importar wallet existente
      const walletData = require('../wallet_data.json');
      wallet = await Wallet.import(walletData);
      console.log('📂 Wallet importada com sucesso!');
    } catch (error) {
      // Criar nova wallet se não existir
      wallet = await Wallet.create({ networkId: process.env.NETWORK_ID || 'base-mainnet' });
      console.log('🆕 Nova wallet criada!');
      
      // Salvar dados da wallet
      const fs = require('fs');
      fs.writeFileSync('./wallet_data.json', JSON.stringify(wallet.export()));
      console.log('💾 Dados da wallet salvos em wallet_data.json');
    }

    // Obter endereço da wallet
    const address = await wallet.getDefaultAddress();
    console.log(`\n📍 Endereço da Wallet: ${address.getId()}\n`);

    // Verificar saldo
    const balance = await wallet.getBalance('eth');
    console.log(`💰 Saldo atual: ${balance} ETH\n`);

    // Verificar se há saldo suficiente
    const amountToSend = '0.003';
    if (parseFloat(balance) < parseFloat(amountToSend)) {
      console.log('❌ Saldo insuficiente!');
      console.log(`   Necessário: ${amountToSend} ETH`);
      console.log(`   Disponível: ${balance} ETH`);
      console.log(`\n💡 Deposite ETH no endereço acima para continuar.`);
      return;
    }

    // Endereço de destino (ALTERE AQUI)
    const destinationAddress = '0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb'; // Exemplo

    console.log('📤 Preparando transferência...');
    console.log(`   De: ${address.getId()}`);
    console.log(`   Para: ${destinationAddress}`);
    console.log(`   Valor: ${amountToSend} ETH\n`);

    // Confirmar antes de enviar
    const readline = require('readline').createInterface({
      input: process.stdin,
      output: process.stdout
    });

    readline.question('Confirmar transferência? (sim/não): ', async (answer) => {
      if (answer.toLowerCase() === 'sim') {
        try {
          // Enviar ETH
          const transfer = await wallet.createTransfer({
            amount: amountToSend,
            assetId: 'eth',
            destination: destinationAddress,
          });

          console.log('\n⏳ Aguardando confirmação da transação...');
          
          await transfer.wait();

          console.log('\n✅ Transferência concluída com sucesso!');
          console.log(`🔗 Hash da transação: ${transfer.getTransactionHash()}`);
          console.log(`🌐 Ver no explorer: https://basescan.org/tx/${transfer.getTransactionHash()}`);
        } catch (error) {
          console.error('\n❌ Erro ao enviar ETH:', error.message);
        }
      } else {
        console.log('\n❌ Transferência cancelada.');
      }
      readline.close();
    });

  } catch (error) {
    console.error('❌ Erro:', error.message);
    console.error('\n💡 Dicas:');
    console.error('   1. Verifique se as credenciais CDP estão corretas no .env');
    console.error('   2. Certifique-se de que a API Key tem as permissões necessárias');
    console.error('   3. Verifique sua conexão com a internet');
  }
}

// Executar
sendETH();
```

### Opção 2: Script com AI Agent (Mais Avançado)

```javascript
require('dotenv').config();
const { Coinbase, Wallet } = require('@coinbase/coinbase-sdk');

class BaseAgent {
  constructor() {
    this.wallet = null;
  }

  async initialize() {
    // Configurar SDK
    Coinbase.configure({
      apiKeyName: process.env.CDP_API_KEY_NAME,
      privateKey: process.env.CDP_API_KEY_PRIVATE_KEY,
    });

    // Criar/importar wallet
    try {
      const walletData = require('../wallet_data.json');
      this.wallet = await Wallet.import(walletData);
    } catch {
      this.wallet = await Wallet.create({ networkId: 'base-mainnet' });
      const fs = require('fs');
      fs.writeFileSync('./wallet_data.json', JSON.stringify(this.wallet.export()));
    }
  }

  async sendETH(to, amount) {
    const transfer = await this.wallet.createTransfer({
      amount: amount.toString(),
      assetId: 'eth',
      destination: to,
    });
    await transfer.wait();
    return transfer.getTransactionHash();
  }

  async getBalance() {
    return await this.wallet.getBalance('eth');
  }

  async getAddress() {
    const address = await this.wallet.getDefaultAddress();
    return address.getId();
  }
}

// Uso
async function main() {
  const agent = new BaseAgent();
  await agent.initialize();

  console.log('Endereço:', await agent.getAddress());
  console.log('Saldo:', await agent.getBalance(), 'ETH');

  // Enviar 0.003 ETH
  const txHash = await agent.sendETH('0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb', 0.003);
  console.log('Transação:', txHash);
}

main();
```

## 🔐 Segurança

### ⚠️ NUNCA faça commit de:
-`.env` (adicione ao `.gitignore`)
-`wallet_data.json` (adicione ao `.gitignore`)
-Chaves privadas ou API keys

### ✅ Boas Práticas:
1. Use `.env.example` como template
2. Mantenha backups seguros das credenciais
3. Use diferentes wallets para dev/prod
4. Teste sempre em testnet primeiro (base-sepolia)

## 📚 Recursos Adicionais

-[Coinbase SDK Docs](<https://docs.cdp.coinbase.com/>)
-[Base Network Docs](<https://docs.base.org/>)
-[Agent Kit GitHub](<https://github.com/coinbase/agentkit>)

## 🎯 Próximos Passos

1. **Deploy de Contratos**: Use o Agent Kit para fazer deploy de smart contracts
2. **Automação**: Crie agentes que executam tarefas automaticamente
3. **Integração com IA**: Combine com LLMs para criar agentes inteligentes

---

**NΞØ SMART FACTORY** — Expandindo até o silêncio se tornar estrutura.
