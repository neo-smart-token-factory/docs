# Arquitetura da NΞØ SMART FACTORY

## Visão Geral da Arquitetura

A NΞØ SMART FACTORY utiliza um padrão de **Factory Modular** onde cada componente pode ser criado independentemente ou como parte de um protocolo completo.

## Componentes Principais

### 1. NeoSmartFactory (Contrato Principal)

**Responsabilidades:**
- Orquestrar a criação de protocolos completos
- Gerenciar taxas de criação
- Registrar todos os protocolos criados
- Controlar acesso através de authorized creators

**Estrutura de Dados:**
```solidity
struct Protocol {
    address creator;
    string name;
    string symbol;
    address tokenAddress;
    address vestingAddress;
    address rewardsAddress;
    uint256 createdAt;
    bool active;
}
```

**Funções Principais:**
- `createProtocol()`: Cria um protocolo completo
- `createToken()`: Cria apenas um token ERC20
- `createNFT()`: Cria apenas uma coleção NFT
- `getProtocol()`: Retorna informações de um protocolo
- `getCreatorProtocols()`: Lista protocolos de um criador

### 2. NeoERC20 (Token Customizável)

**Características:**
- Baseado em OpenZeppelin ERC20
- Suporte opcional para mint, burn e pause
- Ownership transferível para o criador
- Configuração imutável após deploy

**Flags de Configuração:**
- `isMintable`: Permite criação de novos tokens
- `isBurnable`: Permite queima de tokens
- `isPausable`: Permite pausar transferências

### 3. NeoERC721 (NFT Customizável)

**Características:**
- Baseado em OpenZeppelin ERC721
- Metadata URI por token
- Base URI configurável
- Mint em lote suportado
- Contador automático de token IDs

**Funcionalidades:**
- `mint()`: Cria um único NFT
- `batchMint()`: Cria múltiplos NFTs de uma vez
- `setBaseURI()`: Atualiza a base URI

### 4. NeoVesting (Sistema de Vesting)

**Características:**
- Múltiplos schedules por beneficiário
- Vesting linear com cliff period
- Revogação opcional
- Liberação automática de tokens

**Estrutura de Vesting:**
```solidity
struct VestingSchedule {
    address beneficiary;
    uint256 totalAmount;
    uint256 releasedAmount;
    uint256 startTime;
    uint256 duration;
    uint256 cliff;
    bool revocable;
    bool revoked;
}
```

**Fluxo de Vesting:**
1. Tokens são transferidos para o contrato de vesting
2. Schedule é criado com parâmetros definidos
3. Beneficiário pode liberar tokens após o cliff
4. Tokens são liberados linearmente ao longo da duração
5. Owner pode revogar (se revocable)

### 5. NeoRewards (Sistema de Recompensas)

**Características:**
- Badges personalizados com metadata
- Distribuição de recompensas em tokens
- Histórico completo de recompensas
- Múltiplos badges por usuário

**Estruturas:**
```solidity
struct Badge {
    string name;
    string description;
    string metadataURI;
    uint256 createdAt;
    bool active;
}

struct Reward {
    address recipient;
    uint256 amount;
    string reason;
    uint256 timestamp;
}
```

## Fluxo de Criação de Protocolo

```
1. Usuário chama createProtocol() com configurações
   ↓
2. Factory valida taxa e configurações
   ↓
3. Factory cria NeoERC20 com configurações
   ↓
4. Se há vesting configs:
   - Factory cria NeoVesting
   - Transfere tokens para vesting
   - Configura schedules
   ↓
5. Se rewardsEnabled:
   - Factory cria NeoRewards
   ↓
6. Factory registra protocolo
   ↓
7. Emite eventos de criação
```

## Segurança

### Medidas Implementadas

1. **ReentrancyGuard**: Todas as funções que transferem tokens
2. **SafeERC20**: Transferências seguras de tokens
3. **Validações**: Verificação de todos os parâmetros de entrada
4. **Ownership**: Controle de acesso através de Ownable
5. **Immutabilidade**: Flags de configuração são imutáveis após deploy

### Considerações de Segurança

- Taxas são acumuladas no contrato e podem ser retiradas pelo owner
- Vesting schedules podem ser revogados apenas se `revocable = true`
- Tokens mintados são transferidos diretamente para o criador
- NFTs podem ser mintados apenas pelo owner do contrato NFT

## Gas Optimization

### Otimizações Implementadas

1. **Packed Structs**: Estruturas otimizadas para reduzir storage
2. **Events**: Uso extensivo de events para indexação off-chain
3. **Batch Operations**: Funções batch para reduzir custos de gas
4. **Immutable**: Variáveis imutáveis para reduzir gas de leitura

### Estimativas de Gas (Aproximadas)

- Criar Token: ~2.5M gas
- Criar NFT: ~2.8M gas
- Criar Protocolo Completo: ~4.5M gas
- Criar Vesting Schedule: ~150K gas
- Liberar Tokens (Vesting): ~80K gas
- Distribuir Recompensa: ~60K gas

## Extensibilidade

### Pontos de Extensão

1. **Novos Tipos de Tokens**: Adicionar novos contratos de token
2. **Novos Módulos**: Adicionar novos sistemas (governance, staking, etc.)
3. **Templates**: Sistema de templates para protocolos pré-configurados
4. **Plugins**: Sistema de plugins para funcionalidades adicionais

### Padrões de Design

- **Factory Pattern**: Criação de contratos sob demanda
- **Modular Design**: Componentes independentes e reutilizáveis
- **Event-Driven**: Comunicação através de events
- **Ownership Pattern**: Controle descentralizado por criador

## Integração com Frontend

### Eventos Importantes

```javascript
// Protocolo criado
ProtocolCreated(protocolId, creator, name, tokenAddress, vestingAddress, rewardsAddress)

// Token criado
TokenCreated(protocolId, tokenAddress, name, symbol)

// Vesting criado
VestingCreated(protocolId, vestingAddress, beneficiary)

// Recompensas criadas
RewardsCreated(protocolId, rewardsAddress)
```

### Queries Úteis

```javascript
// Listar protocolos de um criador
const protocols = await factory.getCreatorProtocols(creatorAddress);

// Obter informações de um protocolo
const protocol = await factory.getProtocol(protocolId);

// Obter badges de um usuário
const badges = await rewards.getUserBadges(userAddress);

// Obter recompensas de um usuário
const rewards = await rewardsContract.getUserRewards(userAddress);
```

## Roadmap Técnico

### Fase 1: Core (Atual)
- ✅ Factory básica
- ✅ Tokens ERC20/ERC721
- ✅ Sistema de vesting
- ✅ Sistema de recompensas

### Fase 2: Expansão
- [ ] Tokens ERC1155
- [ ] Sistema de governance
- [ ] Staking pools
- [ ] Airdrop automático

### Fase 3: Automação
- [ ] Templates de protocolos
- [ ] Oracles para dados externos
- [ ] Automação de tarefas recorrentes
- [ ] Integração com IPFS

### Fase 4: Descentralização
- [ ] DAO para governança da factory
- [ ] Sistema de reputação
- [ ] Marketplace de templates
- [ ] Token de governança próprio

