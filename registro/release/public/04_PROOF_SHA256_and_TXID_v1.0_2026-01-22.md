# MANIFESTO DE PROVA — SHA-256 E TXID

**Versão**: v1.0  
**Data**: 2026-01-22  
**Local**: Goiânia, Goiás - Brasil

---

## TABELA DE HASHES SHA-256

Esta tabela contém os hashes SHA-256 de cada arquivo do Pacote de Registro v1.0 do projeto NΞØ SMART TOKEN FACTORY.

| Arquivo | SHA-256 Hash |
|---------|--------------|
| 00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22 | `[A SER PREENCHIDO APÓS GERAÇÃO]` |
| 01_CORE_Authorship_and_Prior_Art_v1.0_2026-01-22 | `[A SER PREENCHIDO APÓS GERAÇÃO]` |
| 02_SYSTEM_Executable_Concept_Overview_v1.0_2026-01-22 | `[A SER PREENCHIDO APÓS GERAÇÃO]` |
| 03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt | `[A SER PREENCHIDO APÓS GERAÇÃO]` |

---

## INFORMAÇÕES DE REGISTRO BLOCKCHAIN

### Rede Blockchain

**Rede**: `[BLOCKCHAIN_NETWORK]`  
*Exemplo: Ethereum Mainnet, Base Mainnet, Arweave, OpenTimestamps*

### Transação Blockchain

**TXID (Transaction ID)**: `[TXID]`  
*Hash da transação que registra este pacote na blockchain*

**Timestamp UTC**: `[UTC_TIMESTAMP]`  
*Formato: YYYY-MM-DDTHH:MM:SSZ*  
*Exemplo: 2026-01-22T14:30:00Z*

---

## INSTRUÇÕES PARA GERAR HASHES

### Método 1: Linha de Comando (Linux/Mac)

```bash
# Gerar SHA-256 de um arquivo
sha256sum arquivo.md

# Ou usando shasum (Mac)
shasum -a 256 arquivo.md
```

### Método 2: Linha de Comando (Windows)

```powershell
# Usando PowerShell
Get-FileHash arquivo.md -Algorithm SHA256
```

### Método 3: Online

Use ferramentas online como:
-https://emn178.github.io/online-tools/sha256_checksum.html
-https://www.fileformat.info/tool/hash.htm

---

## INSTRUÇÕES PARA VALIDAÇÃO

### Passo 1: Gerar Hash de Cada Arquivo

Use um dos métodos acima para gerar o SHA-256 de cada arquivo do pacote:
-00_INDEX
-01_CORE
-02_SYSTEM
-03_PROOF (arquivo TXT)

### Passo 2: Comparar com Hashes Documentados

Compare os hashes gerados com os hashes documentados nesta tabela. Os hashes devem ser **idênticos**.

### Passo 3: Validar Statement (03_PROOF)

O arquivo `03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt` deve ser **idêntico** ao texto usado para gerar o hash que foi registrado na blockchain.

**Importante**: Qualquer alteração no arquivo 03_PROOF resultará em um hash diferente e invalidará a prova blockchain.

### Passo 4: Verificar TXID

Após o registro na blockchain:
1. Acesse o explorador da rede utilizada
2. Cole o TXID na busca
3. Verifique que a transação contém o hash do arquivo 03_PROOF
4. Confirme o timestamp da transação

---

## OBSERVAÇÕES IMPORTANTES

-Os hashes SHA-256 são gerados a partir do conteúdo exato dos arquivos
-Qualquer alteração nos arquivos resultará em hashes diferentes
-O arquivo 03_PROOF deve ser idêntico ao usado para registro blockchain
-Este documento deve ser atualizado após a geração dos hashes e registro blockchain

---

## STATUS

-[ ] Hashes SHA-256 gerados e preenchidos
-[ ] Transação blockchain criada
-[ ] TXID obtido e preenchido
-[ ] Timestamp UTC registrado
-[ ] Validação realizada

---

**NΞØ SMART TOKEN FACTORY — Manifesto de Prova SHA-256 e TXID v1.0**  
*Goiânia, Goiás - Brasil, 2026-01-22*
