# 🎓 Sessão de Aprendizado: Bug na TON Factory

**Data:** 2026-01-25  
**Objetivo:** Entender por que a Factory não cria o Jetton Minter  
**Status:** 🔍 Em Investigação

---

## 📚 O Que Aprendemos

### 1. ✅ Código Oficial do TON Minter

Estudamos o código oficial: https://github.com/ton-blockchain/minter-contract

**Linha crítica do `mint_tokens()`:**

```func
var msg = begin_cell()
    .store_uint(0x18, 6)
    .store_slice(to_wallet_address)
    .store_coins(amount)
    .store_uint(4 + 2 + 1, 1 + 4 + 4 + 64 + 32 + 1 + 1 + 1)  // ← OFICIAL!
    .store_ref(state_init)
    .store_ref(master_msg);
send_raw_message(msg.end_cell(), 1);
```

**Descoberta:** O código oficial do TON usa **`4 + 2 + 1` em `109 bits`** - exatamente o que tínhamos originalmente!

### 2. 📖 Estrutura de Mensagem Internal no TON

Documentação oficial: https://docs.ton.org/foundations/messages/internal

```
int_msg_info$0
    ihr_disabled:Bool
    bounce:Bool
    bounced:Bool
    src:MsgAddress
    dest:MsgAddressInt
    value:CurrencyCollection
    extra_flags:(VarUInteger 16)
    fwd_fee:Grams
    created_lt:uint64
    created_at:uint32
= CommonMsgInfoRelaxed;
```

**Campos Fixos Após `value`:**
- `extra_flags`: VarUInteger 16 (variável)
- `fwd_fee`: Grams (variável)
- `created_lt`: 64 bits (fixo)
- `created_at`: 32 bits (fixo)

### 3. ⚙️ Diferença: Minter vs Factory

**TON Oficial (Minter):**
- Deploy **direto** do Jetton Minter
- Usuário → Jetton Minter (com StateInit)

**Nossa Arquitetura (Factory):**
- Deploy **indireto** via Factory
- Usuário → Factory → Jetton Minter (com StateInit)
- **Problema:** Factory não está criando o Jetton Minter!

### 4. 🔍 Comportamento Observado

```
✅ Factory recebe mensagem deploy_jetton
✅ Factory processa sem reverter
✅ Factory devolve ~0.498 TON (excess)
❌ Factory NÃO envia StateInit
❌ Jetton Minter NÃO é criado
```

---

## 🐛 Análise do Bug

### Evidências Coletadas:

#### ✅ O Que Está Correto:

1. **OP Code:** `0x61caf729` está correto em script e contrato
2. **Compilação:** Contrato compila sem erros
3. **Deploy da Factory:** Factory é deployada com sucesso
4. **Transaction:** Transaction é confirmada sem erro
5. **Balance:** Factory tem TON suficiente

#### ❌ O Que Está Falhando:

1. **Nenhum StateInit enviado** nas OUT messages
2. **Nenhum Jetton Minter criado** na blockchain
3. **Bug reproduzível** em 100% das tentativas (5/5 factories testadas)

---

## 🔬 Hipóteses de Root Cause

### Hipótese #1: 🔥 **Throw Silencioso (Mais Provável)**

```func
if (op == op::deploy_jetton()) {
    throw_unless(75, msg_value >= min_deploy_value); // ← Pode estar falhando aqui?
    throw_unless(76, jetton_deploy_value > 0);       // ← Ou aqui?
    
    // ... código de deploy ...
    send_raw_message(msg.end_cell(), 1);
    return ();
}
```

**Problema:** Se algum `throw_unless` falha, a transaction reverte **MAS** o excess é devolvido normalmente.

**Teste:** Adicionar logs ou verificar valores exatos.

### Hipótese #2: ⚠️ **Formato de Mensagem Incorreto**

```func
var msg = begin_cell()
    .store_uint(0x18, 6)
    .store_slice(jetton_address)
    .store_coins(jetton_deploy_value)
    .store_uint(4 + 2, 1 + 4 + 4 + 64 + 32 + 1 + 1)  // ← Nosso "fix"
    .store_ref(state_init)
    .store_ref(begin_cell().end_cell());
```

**Problema:** Tentamos "corrigir" mas o oficial usa `4 + 2 + 1` em `109 bits`.

**Porquê o oficial funciona?** Código oficial não é Factory, é Minter direto!

### Hipótese #3: 🎯 **StateInit Incorreto**

```func
cell state_init = calculate_jetton_minter_state_init(
    owner_address, content, jetton_minter_code, jetton_wallet_code, 
    max_supply, mint_price, mint_amount
);
```

**Problema:** A função pode estar construindo StateInit incompatível.

**Comparação com oficial:**
- Oficial: Minter cria Wallet (1 nível)
- Nosso: Factory cria Minter (que cria Wallet - 2 níveis)

---

## 🔧 Próximos Passos para Debug

### 1. 📊 Adicionar Get Methods de Debug

```func
;; Adicionar no Factory:
int get_last_op() method_id {
    ;; Retorna último OP recebido
}

int get_last_msg_value() method_id {
    ;; Retorna último msg_value recebido
}

slice get_calculated_jetton_address() method_id {
    ;; Retorna último endereço calculado
}
```

### 2. 🧪 Testar com Valores Maiores

```javascript
// Testar com mais TON
const DEPLOY_AMOUNT = toNano('1.0'); // ← Aumentar para 1 TON

// Ver se é problema de gas
```

### 3. 📝 Comparar StateInit Byte por Byte

```javascript
// Calcular localmente o StateInit esperado
const expectedStateInit = buildStateInit(code, data);

// Comparar com o que a Factory está gerando
// (via get-method ou TonScan)
```

### 4. 🔍 Simplificar ao Máximo

Criar uma versão **minimalista** da Factory:

```func
() recv_internal(int msg_value, cell in_msg_full, slice in_msg_body) impure {
    int op = in_msg_body~load_uint(32);
    
    if (op == 0x61caf729) {  // deploy_jetton
        // StateInit fixo, hardcoded
        cell state_init = begin_cell()
            .store_uint(0, 2)
            .store_uint(1, 1)
            .store_ref(jetton_code)
            .store_uint(1, 1)
            .store_ref(jetton_data)
            .store_uint(0, 1)
            .end_cell();
        
        // Mensagem mais simples possível
        var msg = begin_cell()
            .store_uint(0x18, 6)
            .store_slice(calculated_address)
            .store_coins(100000000)  // 0.1 TON fixo
            .store_uint(0, 1 + 4 + 4 + 64 + 32 + 1 + 1)
            .store_uint(1, 1)  // init present
            .store_ref(state_init)
            .store_uint(0, 1)  // body empty
            .end_cell();
        
        send_raw_message(msg, 1);
        return ();
    }
}
```

### 5. 🎓 Estudar Exemplos Reais de Factory

Procurar projetos TON que usam Factory pattern:

- Jetton Factory projects no GitHub
- TON NFT Collections (também usam Factory)
- TON DAO Factory examples

---

## 📊 Comparação: Nosso Código vs Oficial

| Aspecto | TON Oficial | Nosso Factory | Status |
|---------|-------------|---------------|--------|
| OP Code | N/A (direto) | `0x61caf729` | ✅ OK |
| StateInit | Wallet | Minter | ❓ Verificar |
| Message Format | `4+2+1` em 109 bits | `4+2` em 107 bits | ❌ Diverge |
| Arquitetura | User→Minter | User→Factory→Minter | ⚠️ Mais complexo |
| Resultado | ✅ Funciona | ❌ Não cria Minter | 🔴 Bug |

---

## 💡 Insights Importantes

### 1. **Não Confie Cegamente em "Fixes"**

Tentamos "corrigir" de `4+2+1` para `4+2` mas o oficial usa `4+2+1`!

**Lição:** Sempre compare com código oficial **funcionando** antes de "corrigir".

### 2. **Factory Pattern é Diferente**

TON Minter oficial ≠ Factory que cria Minter

**Implicações:**
- StateInit pode precisar de estrutura diferente
- Ordem de operações pode importar
- Dois níveis de indireção (Factory→Minter→Wallet)

### 3. **Debugging em Blockchain é Difícil**

**Sem logs, sem breakpoints!**

Estratégias:
- Get methods para expor estado interno
- Testar em testnet primeiro
- Comparar byte por byte com oficial
- Estudar transações bem-sucedidas no TonScan

---

## 🎯 Próxima Ação Recomendada

**Simplificar e Isolar:**

1. Criar Factory **minimalista** (sem features extras)
2. Testar com StateInit fixo/hardcoded
3. Comparar resultado com TON Minter oficial
4. Adicionar complexidade gradualmente

**OU**

Usar TON Minter oficial e adicionar Factory depois (quando entendermos melhor).

---

## 📚 Recursos Úteis

- **TON Docs:** https://docs.ton.org/foundations/messages/internal
- **Minter Contract:** https://github.com/ton-blockchain/minter-contract
- **Minter Frontend:** https://github.com/ton-blockchain/minter
- **TON Minter App:** https://minter.ton.org

---

## ✅ O Que Funciona (Para Referência)

```bash
# Usar TON Minter oficial para criar tokens:
https://minter.ton.org

# Deploy de Factory funciona (contrato é criado)
# Transaction é confirmada (sem erro aparente)
# Excess é devolvido corretamente
```

---

**Status:** Investigação continua. Bug persistente mas bem documentado. 🔍
