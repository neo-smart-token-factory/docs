# Guia Rápido — Publicar Hash na Arweave

**Objetivo**: Publicar hash do 03_PROOF na Arweave para Camada 1 de proteção

**Hash para publicar**: `c8cc3f4bd08b7244031510ca17468f14fb02bddf32d4104f000c83d1cf33e141`

---

## 🦔 OPÇÃO 1: ArConnect (Recomendado - Mais Fácil)

### O que é:

Extensão de browser (Chrome/Firefox) similar ao MetaMask, mas para Arweave.

### Como usar

1. **Instalar ArConnect**:
   - Chrome: <https://chrome.google.com/webstore/detail/arconnect/einnioafmpimabjcddiinlhmijaionap>
   - Firefox: <https://addons.mozilla.org/en-US/firefox/addon/arconnect/>

2. **Criar/Importar Wallet**:
   - Abra a extensão ArConnect
   - Crie nova wallet ou importe existente
   - **Importante**: Baixe e guarde o arquivo keyfile (.json)

3. **Obter AR tokens** (para pagar upload):
   - Arweave Faucet: <https://faucet.arweave.net/>
   - Precisa de ~0.01 AR (muito pouco, quase grátis)

4. **Publicar hash**:
   - Use ArDrive: <https://app.ardrive.io>
   - Conecte ArConnect
   - Faça upload do arquivo `03_PROOF.txt` ou crie um arquivo com o hash
   - Anote o TXID gerado

---

## 🌐 OPÇÃO 2: ArDrive (Mais Simples para Upload)

### O que é:
Interface web para upload de arquivos na Arweave.

### Como usar:

1. **Acesse**: <https://app.ardrive.io>
2. **Conecte wallet**: ArConnect ou Arweave.app
3. **Crie um Drive** (público ou privado)
4. **Faça upload** do arquivo `03_PROOF.txt`
5. **Anote**: TXID da transação

**Vantagem**: Interface simples, não precisa código.

---

## 📝 OPÇÃO 3: Arweave.app (Web Wallet)

### O que é:
Wallet web open-source da Arweave.

### Como usar:

1. **Acesse**: <https://arweave.app>
2. **Crie wallet** ou importe existente
3. **Use ferramentas de upload** disponíveis no site
4. **Anote**: TXID gerado

---

## ⚡ MÉTODO MAIS RÁPIDO (5 minutos)

### Passo a Passo Simplificado:

1. **Instale ArConnect** (extensão do browser)
2. **Crie wallet** na extensão
3. **Pegue AR grátis** no faucet: <https://faucet.arweave.net/>
4. **Acesse ArDrive**: <https://app.ardrive.io>
5. **Conecte ArConnect** no ArDrive
6. **Faça upload** do arquivo `03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt`
7. **Anote o TXID** gerado
8. **Preencha no 04_PROOF**:
   - Rede: Arweave
   - TXID: [o que você anotou]
   - Data: [data de hoje]

---

## 📋 INFORMAÇÕES PARA PREENCHER NO 04_PROOF

Após publicar na Arweave, você terá:

-**Rede**: Arweave
-**TXID**: [hash da transação Arweave - começa com letras/números]
-**Data**: [data do upload]
-**Link**: `https://arweave.net/[TXID]`

---

## 💡 DICA

**Arquivo para upload**: Use o arquivo `03_PROOF.txt` que você já tem, ou crie um arquivo simples com apenas o hash:

```
Hash SHA-256: c8cc3f4bd08b7244031510ca17468f14fb02bddf32d4104f000c83d1cf33e141
Projeto: NEO SMART TOKEN FACTORY
Data: 2026-01-22
```

Isso cria uma prova pública permanente na Arweave!

---

**Tempo estimado**: 5-10 minutos  
**Custo**: ~0.01 AR (quase grátis via faucet)
