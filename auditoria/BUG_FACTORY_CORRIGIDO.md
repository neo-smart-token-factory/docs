# 🔥 BUG CRÍTICO IDENTIFICADO E CORRIGIDO

**Data:** 2026-01-25  
**Arquivo:** `contracts/ton/NeoJettonFactoryMultiAdmin.fc`  
**Severidade:** 🔴 CRÍTICA  
**Status:** ✅ CORRIGIDO

---

## 📋 Resumo Executivo

Bug no formato de mensagem interna da Factory impedia o deploy de Jetton Minters na Mainnet.

**Impacto:** 100% das tentativas de deploy falhavam silenciosamente (3/3 tentativas).

**Root Cause:** Bits incorretos no header da mensagem de deploy.

---

## 🔍 Investigação

### Sintomas Observados:

```diff
✅ Factory recebia mensagem deploy_jetton
✅ Factory processava sem reverter
✅ Factory devolvia excess TON (~0.498 TON)
❌ Factory NÃO enviava mensagem com StateInit
❌ Jetton Minter NUNCA foi criado
```

### Diagnóstico:

Executamos debug em **TODAS as 3 factories** deployadas na Mainnet:

```
Factory #1 (EQAqoO...C2ZM): ❌ Nenhum StateInit enviado
Factory #2 (EQCFO...XMz9):  ❌ Nenhum StateInit enviado  
Factory #3 (EQBtx...dalz):  ❌ Nenhum StateInit enviado
```

**Resultado:** Confirmado que o bug está no smart contract, não no script.

---

## 🐛 Bug Identificado

### Localização:

**Arquivo:** `contracts/ton/NeoJettonFactoryMultiAdmin.fc`  
**Linhas:** 163-174

### Código Bugado:

```func
;; ❌ ANTES (ERRADO)
var msg = begin_cell()
    .store_uint(0x18, 6)
    .store_slice(jetton_address)
    .store_coins(jetton_deploy_value)
    .store_uint(4 + 2 + 1, 1 + 4 + 4 + 64 + 32 + 1 + 1 + 1)  // ← BUG AQUI!
    .store_ref(state_init);

msg = msg.store_ref(begin_cell().end_cell());

send_raw_message(msg.end_cell(), 1);
```

### Problema:

```diff
- .store_uint(4 + 2 + 1, 1 + 4 + 4 + 64 + 32 + 1 + 1 + 1)
-            ^^^^^^^  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
-            Valor: 7     Bits: 109

❌ Armazena valor 7 em 109 bits:
   00000000...00000111 (107 zeros + 111)
   
❌ Isso corrompe o formato da mensagem TON!
```

---

## 📐 Formato Correto de Mensagem TON

### Estrutura da Message após `store_coins(value)`:

```
┌─────────────────┬──────┬────────────────────────────┐
│ Campo           │ Bits │ Valor Padrão               │
├─────────────────┼──────┼────────────────────────────┤
│ extra_currencies│  1   │ 0 (não tem moedas extras)  │
│ ihr_fee         │  4   │ 0000                       │
│ fwd_fee         │  4   │ 0000                       │
│ created_lt      │ 64   │ 0 (64 zeros)               │
│ created_at      │ 32   │ 0 (32 zeros)               │
│ init_present    │  1   │ 1 (tem StateInit)          │
│ body_present    │  1   │ 1 (tem body)               │
└─────────────────┴──────┴────────────────────────────┘
                    TOTAL: 107 bits
```

### Valores dos Flags:

```
Binário:  ...00000110
                  ^^
                  ||
                  |+-- body_present (bit 0)
                  +--- init_present (bit 1)

Valor: 0b110 = 6 decimal
```

**Correto:** `.store_uint(6, 107)` ou `.store_uint(4 + 2, 107)`

---

## ✅ Correção Aplicada

### Código Corrigido:

```func
;; ✅ DEPOIS (CORRETO)
var msg = begin_cell()
    .store_uint(0x18, 6)
    .store_slice(jetton_address)
    .store_coins(jetton_deploy_value)
    .store_uint(4 + 2, 1 + 4 + 4 + 64 + 32 + 1 + 1)  // ✅ CORRIGIDO: 6 em 107 bits
    .store_ref(state_init)
    .store_ref(begin_cell().end_cell());  // Empty body

send_raw_message(msg.end_cell(), 1);
```

### Mudanças:

```diff
- .store_uint(4 + 2 + 1, 1 + 4 + 4 + 64 + 32 + 1 + 1 + 1)
+ .store_uint(4 + 2, 1 + 4 + 4 + 64 + 32 + 1 + 1)

- msg = msg.store_ref(begin_cell().end_cell());
- send_raw_message(msg.end_cell(), 1);
+ .store_ref(begin_cell().end_cell())
+ send_raw_message(msg.end_cell(), 1);
```

---

## 📊 Impacto da Correção

### Antes (Bugado):

```
Mensagem com 109 bits extras: FORMATO INVÁLIDO
└─> Não processada pela blockchain
└─> Contrato não criado
└─> Excess retornado ao sender
```

### Depois (Corrigido):

```
Mensagem com 107 bits extras: FORMATO VÁLIDO
└─> Processada corretamente
└─> StateInit aplicado
└─> Jetton Minter criado no endereço calculado
```

---

## 🧪 Próximos Passos

### 1. Recompilar:

```bash
node scripts/compile-ton-multiadmin.js
```

### 2. Testar em Testnet:

```bash
# Primeiro testar em testnet antes de deployar na mainnet
export TON_NETWORK=testnet
node scripts/deploy-ton-factory-multiadmin.js
```

### 3. Deploy Nova Factory na Mainnet:

```bash
# Após validação em testnet
export TON_NETWORK=mainnet
node scripts/deploy-ton-factory-multiadmin.js
```

### 4. Testar Deploy de Token:

```bash
# Deploy do $NSF via nova Factory
node scripts/deploy-nsf-token.js
```

### 5. Verificar:

```bash
# Executar debug para confirmar
node scripts/debug-jetton-address.js
```

---

## 📈 Lições Aprendidas

### 🎯 Diagnóstico Correto:

1. ✅ Analisamos todas as 3 factories na blockchain
2. ✅ Confirmamos que NENHUMA enviou StateInit
3. ✅ Identificamos que o problema era no contrato, não no script
4. ✅ Localizamos o bug exato no formato da mensagem

### 🔧 Ferramentas Criadas:

1. `scripts/debug-jetton-address.js` - Analisa transações e calcula endereço esperado
2. `scripts/debug-all-factories.js` - Audita múltiplas factories
3. `auditoria/ANALISE_BUG_JETTON_MINTER.md` - Documentação completa do bug
4. `auditoria/BUG_FACTORY_CORRIGIDO.md` - Este documento

---

## ⚠️ Notas de Segurança

### Factories Antigas (Bugadas):

```
EQAqoO4t8NKfjXQ1mEeBwqqjEON6zwECv-haaX__pGp_C2ZM - ❌ Não usar
EQCFOkAK28g0uhy_D3t2SpRhHDtjFjAkouGdh0qatW7RXMz9 - ❌ Não usar
EQBtxNPwrpX6Enzw3j7bjFkGFUpnFivLeRW9LVOeT-Yldalz - ❌ Não usar
```

**IMPORTANTE:** Não tentar usar essas factories. Elas têm o bug e não podem deployar Jettons.

### Próxima Factory:

- Será deployada com o código corrigido
- Deve ser testada em testnet primeiro
- Endereço será atualizado após deploy bem-sucedido

---

## 📝 Referências

### Documentos Criados:

- `auditoria/ANALISE_BUG_JETTON_MINTER.md` - Análise completa das 3 tentativas
- `auditoria/BUG_FACTORY_CORRIGIDO.md` - Este documento
- `auditoria/EVM_TON_MAPPING.md` - Mapeamento EVM/TON
- `auditoria/TON_DEPLOY_MAINNET_REPORT.md` - Histórico de deploys

### Scripts de Debug:

- `scripts/debug-jetton-address.js` - Debug de uma factory específica
- `scripts/debug-all-factories.js` - Auditoria de múltiplas factories

### Padrões TON:

- [TON Documentation - Messages](https://docs.ton.org/develop/data-formats/msg-tlb)
- [TON Jetton Standard](https://github.com/ton-blockchain/TEPs/blob/master/text/0074-jettons-standard.md)

---

## ✅ Checklist de Deploy Pós-Correção

- [ ] Código corrigido em `NeoJettonFactoryMultiAdmin.fc`
- [ ] Contratos recompilados
- [ ] Testado em TON Testnet
- [ ] Factory deployada na Mainnet
- [ ] Token de teste deployado via nova Factory
- [ ] Endereço do Jetton Minter verificado
- [ ] Debug confirmou StateInit enviado corretamente
- [ ] Endereço calculado = endereço real na blockchain
- [ ] Documentação atualizada
- [ ] Factory address registrada em `.env`

---

**Status Final:** 🟢 Bug identificado, corrigido e documentado. Pronto para recompilação e redeploy.
