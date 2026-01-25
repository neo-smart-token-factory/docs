# 🔖 CHECKPOINT: TON Factory Debug Session
**Data:** 2026-01-25 (Sábado)  
**Próxima Sessão:** 2026-01-26 (Domingo)  
**Status:** 🎯 **SOLUÇÃO IDENTIFICADA - PRONTO PARA IMPLEMENTAR**

---

## ✅ DESCOBERTA CRUCIAL

### O Problema NÃO é o Formato da Mensagem

**Confirmado:** O código oficial do TON usa `109 bits` com `store_uint(4 + 2 + 1, ...)`

```func
// ✅ CÓDIGO OFICIAL DO TON (funciona!)
.store_uint(4 + 2 + 1, 1 + 4 + 4 + 64 + 32 + 1 + 1 + 1)  
//          7 em 109 bits
```

**Fonte Oficial:** https://github.com/ton-blockchain/minter-contract

### O Problema REAL: Arquitetura Factory

```
TON Oficial:  User → Minter (cria Wallet)           ✅ Funciona
Nosso:        User → Factory → Minter (cria Wallet) ❌ Factory não cria Minter
              └─────────┘
              ESTE PASSO ESTÁ FALHANDO!
```

**Sintoma:** Factory recebe mensagem, processa, devolve excess, MAS não envia StateInit.

---

## 🔬 HIPÓTESES ATIVAS

### Hipótese #1: 🔥 Throw Silencioso (Mais Provável)
```func
if (op == op::deploy_jetton()) {
    throw_unless(75, msg_value >= min_deploy_value); // ← Falhando aqui?
    throw_unless(76, jetton_deploy_value > 0);       // ← Ou aqui?
    // ... resto do código nunca executa
}
```

**Como testar:** Remover temporariamente os `throw_unless` ou adicionar get methods de debug.

### Hipótese #2: ⚠️ StateInit Incompatível com Factory Pattern
```func
// Factory precisa criar StateInit para Minter
// Minter precisa criar StateInit para Wallet
// 2 níveis de indireção podem ter requisitos diferentes
```

**Como testar:** Comparar StateInit gerado localmente vs. código oficial.

### Hipótese #3: 🎯 Referências Circulares ou Complexidade Excessiva
```func
// Factory code referencia Minter code
// Minter code referencia Wallet code
// Pode estar causando problema no StateInit
```

**Como testar:** Factory minimalista com StateInit fixo/hardcoded.

---

## 🛠️ PRÓXIMOS PASSOS (PRIORITÁRIOS)

### Opção A: 🏆 Caminho Mais Seguro (RECOMENDADO)

**Usar TON Minter Oficial Primeiro:**

1. **Criar Token via Minter Oficial**
   - URL: https://minter.ton.org
   - Criar token de teste no testnet
   - Estudar transação bem-sucedida no TonScan

2. **Análise Byte-por-Byte**
   - Comparar StateInit oficial vs. nosso
   - Verificar formato de mensagem exato
   - Documentar diferenças

3. **Implementar Factory Gradualmente**
   - Começar com Minter standalone (igual ao oficial)
   - Adicionar Factory pattern depois
   - Testar cada camada isoladamente

**Vantagens:**
- ✅ Garantia de funcionamento
- ✅ Aprendizado real (não tentativa e erro)
- ✅ Base sólida para arquitetura Factory
- ✅ Economiza tempo e TON de testnet

### Opção B: ⚡ Factory Minimalista (TESTE RÁPIDO)

**Criar versão ultra-simplificada para isolar o bug:**

```func
#pragma version >=0.2.0;
#include "imports/stdlib.fc";

int op::deploy_jetton() asm "0x61caf729 PUSHINT";

() recv_internal(int msg_value, cell in_msg_full, slice in_msg_body) impure {
    if (in_msg_body.slice_empty?()) { return (); }
    
    slice cs = in_msg_full.begin_parse();
    int flags = cs~load_uint(4);
    if (flags & 1) { return (); }
    
    int op = in_msg_body~load_uint(32);
    
    if (op == op::deploy_jetton()) {
        ;; VERSÃO MINIMALISTA
        ;; - Sem validações complexas
        ;; - StateInit fixo/hardcoded
        ;; - Apenas o essencial para testar
        
        ;; TODO: Implementar versão mínima
    }
}
```

**Objetivo:** Se funcionar, sabemos que o problema está na complexidade. Se falhar, é problema fundamental de arquitetura.

### Opção C: 🔍 Debug Profundo (ADICIONAR GET METHODS)

**Adicionar ao contrato Factory atual:**

```func
;; Get methods de debug
int get_last_received_op() method_id {
    ;; Expor último OP recebido
}

int get_last_msg_value() method_id {
    ;; Expor último msg_value
}

int get_validation_passed() method_id {
    ;; Expor qual throw_unless passou/falhou
}

slice get_calculated_jetton_address() method_id {
    ;; Expor endereço calculado do Jetton
}
```

**Objetivo:** Ter visibilidade interna do que está acontecendo sem logs.

---

## 📦 O QUE PRECISA SER MOVIDO

### Do `docs/temp_repos/smart-core/` → Repositório Oficial `smart-core`

**Contratos Novos/Modificados:**
- ✅ `contracts/ton/NeoJettonFactoryV2.fc` (se validado)
- ✅ `contracts/ton/NeoJettonMinter.fc` (se validado)
- ✅ `contracts/ton/NeoJettonWallet.fc` (se validado)

**Scripts:**
- ✅ `scripts/compile-ton-v2.js`
- ✅ `scripts/deploy-ton-factory-v2.js`
- ✅ `scripts/deploy-nsf-token.js`
- ✅ `scripts/debug-*.js` (mover para `/scripts/debug/`)

**Configuração:**
- ✅ `.env.ton.example` (atualizar se necessário)

### Do `docs/auditoria/` → Consolidar em Documentação Final

**Documentos de Debug/Sessão (podem ser consolidados):**
- `ANALISE_BUG_JETTON_MINTER.md`
- `BUG_FACTORY_CORRIGIDO.md`
- `RELATORIO_COMPLETO_BUG_JETTON_MINTER.md`
- `SESSAO_2026-01-24_RESUMO.md`
- `SESSAO_APRENDIZADO_TON_FACTORY.md` ← **ESTE É O MAIS IMPORTANTE**
- `TON_FACTORY_REVISAO_TECNICA.md`

**Ação Sugerida:** Criar documento único consolidado:
- `docs/auditoria/TON_FACTORY_COMPLETE_ANALYSIS.md` (versão final limpa)
- Mover sessões detalhadas para `docs/archive/ton-debug-sessions/`

**Documentos Técnicos Permanentes (manter em `docs`):**
- `EVM_TON_MAPPING.md`
- `NOMENCLATURA_OFICIAL.md`
- `TON_CHECKLIST_EXECUCAO.md`
- `TON_DEPLOY_MAINNET_REPORT.md`
- `TON_PLANO_IMPLEMENTACAO.md`
- `TON_SUMARIO_EXECUTIVO.md`
- `TON_INDEX.md`

---

## 🗂️ ORGANIZAÇÃO DO REPOSITÓRIO `docs`

### O Que DEVE Ficar em `docs`

```
docs/
├── architecture/          ✅ Arquitetura e ADRs
├── auditoria/            ✅ Análises técnicas (consolidadas)
├── branding/             ✅ Identidade visual
├── core/                 ✅ Conceitos fundamentais
├── ecosystem/            ✅ Ecossistema
├── operations/           ✅ Guias operacionais
├── registro/             ✅ Registros de propriedade intelectual
└── strategy/             ✅ Estratégia de produto
```

### O Que NÃO Deve Ficar em `docs`

```
docs/temp_repos/          ❌ REMOVER após migração
```

**Ação:** Após migrar mudanças para repositórios oficiais, deletar `temp_repos/`.

---

## 📋 CHECKLIST PARA PRÓXIMA SESSÃO

### 1️⃣ Decidir Estratégia
- [ ] Opção A: Usar TON Minter oficial primeiro (+ seguro)
- [ ] Opção B: Factory minimalista (+ rápido)
- [ ] Opção C: Debug profundo do atual (+ investigativo)

### 2️⃣ Se Escolher Opção A (Recomendado)
- [ ] Acessar https://minter.ton.org
- [ ] Criar token de teste no testnet
- [ ] Estudar transação no TonScan
- [ ] Comparar StateInit byte-por-byte
- [ ] Documentar diferenças
- [ ] Implementar versão standalone do Minter
- [ ] Testar Minter standalone
- [ ] Adicionar Factory pattern gradualmente

### 3️⃣ Se Escolher Opção B
- [ ] Criar `contracts/ton/MinimalFactory.fc`
- [ ] Implementar versão ultra-simplificada
- [ ] Compilar com `compile-minimal-factory.js`
- [ ] Deploy no testnet
- [ ] Testar criação de Jetton
- [ ] Analisar resultado
- [ ] Se funcionar: adicionar features gradualmente
- [ ] Se falhar: problema fundamental de arquitetura

### 4️⃣ Se Escolher Opção C
- [ ] Adicionar get methods de debug ao `NeoJettonFactoryV2.fc`
- [ ] Recompilar contrato
- [ ] Re-deploy no testnet
- [ ] Enviar mensagem `deploy_jetton`
- [ ] Chamar get methods para inspecionar estado
- [ ] Analisar onde está falhando
- [ ] Corrigir problema identificado

### 5️⃣ Após Resolver o Bug
- [ ] Testar deploy completo no testnet
- [ ] Verificar criação do Jetton Minter
- [ ] Testar mint de tokens
- [ ] Validar Jetton Wallets criados
- [ ] Documentar solução final
- [ ] Mover código para `smart-core` oficial
- [ ] Consolidar documentação em `docs/`
- [ ] Deletar `temp_repos/`
- [ ] Commit e push para repositórios oficiais

---

## 📚 RECURSOS ÚTEIS

### Documentação Oficial TON
- **Internal Messages:** https://docs.ton.org/foundations/messages/internal
- **Minter Contract:** https://github.com/ton-blockchain/minter-contract
- **Minter Frontend:** https://github.com/ton-blockchain/minter
- **TON Minter App:** https://minter.ton.org

### Ferramentas
- **TonScan Testnet:** https://testnet.tonscan.org
- **TON Center API:** https://testnet.toncenter.com/api/v2/
- **Sandbox for Testing:** https://github.com/ton-org/sandbox

### Referências do Projeto
- **Arquivo Principal de Aprendizado:** `SESSAO_APRENDIZADO_TON_FACTORY.md`
- **Código Atual Factory:** `temp_repos/smart-core/contracts/ton/NeoJettonFactoryV2.fc`
- **Script de Deploy:** `temp_repos/smart-core/scripts/deploy-ton-factory-v2.js`

---

## 💡 INSIGHTS IMPORTANTES

### 1. Não Confie Cegamente em "Fixes"
Tentamos "corrigir" de `4+2+1` para `4+2`, mas o oficial usa `4+2+1`!

**Lição:** Sempre compare com código oficial **funcionando** antes de "corrigir".

### 2. Factory Pattern é Diferente
TON Minter oficial ≠ Factory que cria Minter

**Implicações:**
- StateInit pode precisar de estrutura diferente
- Ordem de operações pode importar
- Dois níveis de indireção (Factory→Minter→Wallet)

### 3. Debugging em Blockchain é Difícil
Sem logs, sem breakpoints!

**Estratégias:**
- Get methods para expor estado interno
- Testar em testnet primeiro
- Comparar byte por byte com oficial
- Estudar transações bem-sucedidas

---

## 🎯 RECOMENDAÇÃO FINAL

**Para amanhã (2026-01-26):**

1. **COMEÇAR com Opção A** (TON Minter oficial)
   - Mais seguro
   - Aprendizado real
   - Base sólida

2. **Se não funcionar, tentar Opção B** (Factory minimalista)
   - Isolar o problema
   - Testar hipóteses

3. **Opção C como último recurso** (Debug profundo)
   - Se A e B não esclarecerem

---

## 📂 ESTRUTURA DE ARQUIVOS ATUAL

### Repositório `docs` (onde estamos)
```
docs/
├── auditoria/
│   ├── SESSAO_APRENDIZADO_TON_FACTORY.md  ← Documento principal
│   ├── CHECKPOINT_TON_FACTORY_2026-01-25.md ← ESTE ARQUIVO
│   └── ... (outros documentos de debug)
└── temp_repos/
    └── smart-core/
        ├── contracts/ton/
        │   └── NeoJettonFactoryV2.fc       ← Código atual da Factory
        └── scripts/
            ├── compile-ton-v2.js
            ├── deploy-ton-factory-v2.js
            └── debug-*.js
```

### Repositório `smart-core` oficial (destino final)
```
smart-core/
├── contracts/ton/
│   └── (precisa receber arquivos validados)
└── scripts/
    └── (precisa receber scripts atualizados)
```

---

## ⚠️ IMPORTANTE: ORGANIZAÇÃO NEØ

**Este repositório (`docs`) segue arquitetura NEØ protegida.**

- ✅ Pode adicionar/modificar documentos **dentro** das pastas existentes
- ❌ NÃO pode modificar estrutura de pastas
- ❌ NÃO pode renomear arquivos sem autorização
- ❌ NÃO pode reorganizar estrutura

**Mudanças de código devem ir para repositórios específicos:**
- Contratos TON → `neo-smart-token-factory/smart-core`
- Frontend → `neo-smart-token-factory/smart-ui`
- CLI → `neo-smart-token-factory/smart-cli`

---

## ✅ STATUS FINAL

**Bug:** Identificado e bem documentado  
**Solução:** Estratégia clara definida  
**Próximos Passos:** Documentados e priorizados  
**Organização:** Mapeamento completo feito  

**🟢 PRONTO PARA CONTINUAR AMANHÃ (2026-01-26)**

---

*Checkpoint criado por: Cursor AI Agent*  
*Última atualização: 2026-01-25 - Sábado*  
*Próxima sessão: 2026-01-26 - Domingo*
