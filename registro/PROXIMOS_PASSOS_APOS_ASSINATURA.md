# Próximos Passos Após Assinatura dos Documentos 00, 01 e 02

**Status Atual**: ✅ Documentos 00, 01 e 02 assinados digitalmente

---

## ✅ O QUE JÁ FOI FEITO

-[x] Documento 00_INDEX assinado
-[x] Documento 01_CORE assinado  
-[x] Documento 02_SYSTEM assinado

---

## 📋 O QUE FALTA FAZER

### 1. Documento 03_PROOF (TXT) - NÃO PRECISA ASSINAR

**Arquivo**: `03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt`

**Status**: ✅ Já está pronto

**O que é**: Este arquivo é apenas texto puro para gerar hash SHA-256. Não precisa ser assinado, apenas usado para gerar o hash que será registrado na blockchain.

---

### 2. Gerar Hashes SHA-256 dos Arquivos Assinados

Você precisa gerar o hash SHA-256 de cada arquivo PDF assinado:

#### Arquivos para gerar hash:

1. **00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22.pdf** (já assinado)
2. **01_CORE_Authorship_and_Prior_Art_v1.0_2026-01-22.pdf** (já assinado)
3. **02_SYSTEM_Executable_Concept_Overview_v1.0_2026-01-22.pdf** (já assinado)
4. **03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt** (texto puro)

#### Como gerar hash SHA-256:

**Método 1: Linha de Comando (Mac/Linux)**

```bash
shasum -a 256 arquivo.pdf
```

**Método 2: Online**

-Acesse: https://emn178.github.io/online-tools/sha256_checksum.html
-Faça upload do arquivo PDF
-Copie o hash gerado

**Método 3: Windows PowerShell**
```powershell
Get-FileHash arquivo.pdf -Algorithm SHA256
```

---

### 3. Registrar na Blockchain

Use o arquivo `03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt` para registrar na blockchain.

#### Opções de registro:

**Opção A: Ethereum/Base/Arbitrum**
-Use o hash SHA-256 do arquivo 03_PROOF
-Crie uma transação na blockchain escolhida
-Anote o TXID e timestamp

**Opção B: Arweave**
-Faça upload do arquivo 03_PROOF
-Anote o TXID e timestamp

**Opção C: OpenTimestamps**
-Use o serviço OpenTimestamps
-Anote o timestamp e comprovante

---

### 4. Preencher Documento 04_PROOF

Após gerar os hashes e registrar na blockchain, preencha o documento `04_PROOF_SHA256_and_TXID_v1.0_2026-01-22.md`:

#### O que preencher:

1. **Tabela de Hashes SHA-256**:
   - Hash do arquivo 00_INDEX.pdf
   - Hash do arquivo 01_CORE.pdf
   - Hash do arquivo 02_SYSTEM.pdf
   - Hash do arquivo 03_PROOF.txt

2. **Informações de Registro Blockchain**:
   - Rede utilizada (ex: Ethereum Mainnet, Base Mainnet, Arweave)
   - TXID da transação
   - Timestamp UTC (formato: YYYY-MM-DDTHH:MM:SSZ)

---

### 5. Assinar Documento 04_PROOF

Após preencher todas as informações no documento 04_PROOF:

1. Importe o arquivo `.md` no Google Docs
2. Preencha os campos com os hashes e dados blockchain
3. Converta para PDF
4. Assine digitalmente via Gov.br

---

## 📝 CHECKLIST COMPLETO

### Fase Atual (Concluída):
-[x] Assinar documento 00_INDEX
-[x] Assinar documento 01_CORE
-[x] Assinar documento 02_SYSTEM

### Próxima Fase:
-[ ] Gerar hash SHA-256 do arquivo 00_INDEX.pdf
-[ ] Gerar hash SHA-256 do arquivo 01_CORE.pdf
-[ ] Gerar hash SHA-256 do arquivo 02_SYSTEM.pdf
-[ ] Gerar hash SHA-256 do arquivo 03_PROOF.txt
-[ ] Registrar hash do 03_PROOF na blockchain
-[ ] Obter TXID da transação blockchain
-[ ] Obter timestamp UTC da transação
-[ ] Preencher documento 04_PROOF com todos os dados
-[ ] Assinar documento 04_PROOF

---

## 💡 DICAS IMPORTANTES

1. **Use os PDFs assinados** para gerar os hashes (não os arquivos .md originais)
2. **Guarde todos os PDFs assinados** em local seguro
3. **O hash do 03_PROOF** é o que será registrado na blockchain
4. **O documento 04_PROOF** serve como manifesto de prova com todos os hashes e dados blockchain

---

**Próximo passo**: Gerar os hashes SHA-256 dos arquivos assinados.
