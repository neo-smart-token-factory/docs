# MANIFESTO DE PROVA — SHA-256 E TXID

**Versão**: v1.0  
**Data**: 2026-01-22  
**Local**: Goiânia, Goiás - Brasil

---

## TABELA DE HASHES SHA-256

Esta tabela contém os hashes SHA-256 de cada arquivo do Pacote de Registro v1.0 do projeto NΞØ SMART TOKEN FACTORY.

| Arquivo | SHA-256 Hash |
|---------|--------------|
| 00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22.pdf | `bc5db68af68942956d9c9cc35f9577f18d57133646ab505bf84a21400bdb39b8` |
| 01_CORE_Authorship_and_Prior_Art_v1.0_2026-01-22.pdf | `f4d09edc1e3126c17e2ac069ffd96a047c2ae55f4acc09fd1ac7b411030cc0cd` |
| 02_SYSTEM_Executable_Concept_Overview_v1.0_2026-01-22.pdf | `ebe364bbf7383ab3a7a3a2435a820052e4935b00cae961bd7825b50f5da976d5` |
| 03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt | `c8cc3f4bd08b7244031510ca17468f14fb02bddf32d4104f000c83d1cf33e141` |

---

## INFORMAÇÕES DE REGISTRO BLOCKCHAIN

### Rede Blockchain

**Rede**: `OpenTimestamps`  
*Serviço de timestamping baseado em Bitcoin blockchain*

### Transação Blockchain

**TXID / Identificador**: `c8cc3f4bd08b7244031510ca17468f14fb02bddf32d4104f000c83d1cf33e141`  
*Hash SHA-256 do arquivo 03_PROOF registrado via OpenTimestamps*

**Arquivo de Prova (.ots)**: `03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt.ots`  
*Arquivo de prova OpenTimestamps gerado e armazenado localmente*

**Timestamp UTC**: `2026-01-23T02:20:00Z`  
*Timestamp da criação do arquivo .ots (Goiânia UTC-3: 23:20 → UTC: 02:20 do dia seguinte)*

### Registro Adicional em Rede Alternativa

**Rede**: `Arweave`  
**Data do Registro**: 2026-01-22

**TXID da Transação (Data)**: `-lEoP7zm3Xt21eNvW26JZQtmwaSjNEoqz8_ya8jsjNw`  
*Hash da transação Arweave que contém o arquivo 03_PROOF*

**TXID da Transação (Metadata)**: `eqyc-9Ex8__BJHoVCcgXP4K5AN6pwy7iRslkc4Bw1S8`  
*Hash da transação de metadata associada*

**Link ArDrive**: <https://app.ardrive.io/#/file/09f56c2f-47ef-40e2-a604-a926bbac2bb6/view?fileKey=d14g8iBu4QE_LFOKUU_zOytsyIGBTPE96YF_Ohc-aYo>

**Link Arweave Gateway**: <https://arweave.net/-lEoP7zm3Xt21eNvW26JZQtmwaSjNEoqz8_ya8jsjNw>

**Licença**: Attribution (CC BY) - Creative Commons

**Espelhamento de hash em rede diferente para redundância temporal inter-chain**: ✅ Implementado

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
- https://emn178.github.io/online-tools/sha256_checksum.html
- https://www.fileformat.info/tool/hash.htm

---

## INSTRUÇÕES PARA VALIDAÇÃO

### Passo 1: Gerar Hash de Cada Arquivo

Use um dos métodos acima para gerar o SHA-256 de cada arquivo do pacote:
- 00_INDEX
- 01_CORE
- 02_SYSTEM
- 03_PROOF (arquivo TXT)

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

- Os hashes SHA-256 são gerados a partir do conteúdo exato dos arquivos
- Qualquer alteração nos arquivos resultará em hashes diferentes
- O arquivo 03_PROOF deve ser idêntico ao usado para registro blockchain
- Este documento deve ser atualizado após a geração dos hashes e registro blockchain
- Esta é a versão PRIVATE com dados completos

---

## STATUS

- [x] Hashes SHA-256 gerados e preenchidos
- [x] Transação blockchain criada (OpenTimestamps)
- [x] TXID obtido e preenchido (hash SHA-256 do 03_PROOF)
- [x] Timestamp UTC registrado (2026-01-23T02:20:00Z)
- [x] Arquivo de prova .ots gerado e armazenado
- [x] Documento pronto para assinatura
- [x] Hash adicional registrado na Arweave (TXID: -lEoP7zm3Xt21eNvW26JZQtmwaSjNEoqz8_ya8jsjNw)
- [ ] Validação final (pode ser feita após assinatura via opentimestamps.org/verify)

---

## ASSINATURA

**ASSINATURA DIGITAL ICP-BRASIL**

Espaço reservado para assinatura digital via Gov.br
(Assinar após conversão para PDF)

_________________________________________________

**Eurycles Ramos Neto**  
CPF: 693.799.711-68  
Goiânia, GO, Brasil

**Data**: 2026-01-22  
**Local**: Goiânia, Goiás - Brasil

---

**NΞØ SMART TOKEN FACTORY — Manifesto de Prova SHA-256 e TXID v1.0**  
*Goiânia, Goiás - Brasil, 2026-01-22*
