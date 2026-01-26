# Instruções para Arquivo .ots (OpenTimestamps)

**Arquivo gerado**: `03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt.ots`

---

## ✅ O QUE VOCÊ TEM AGORA

1. **Arquivo original**: `03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt`
2. **Arquivo de prova**: `*.ots` (na pasta Downloads)
3. **Hash SHA-256**: `c8cc3f4bd08b7244031510ca17468f14fb02bddf32d4104f000c83d1cf33e141`

---

## 📝 INFORMAÇÕES PARA PREENCHER NO 04_PROOF

Com o arquivo .ots gerado, você precisa de:

### Rede Blockchain:
**OpenTimestamps** (ou "OpenTimestamps.org")

### TXID / Identificador:
O arquivo .ots É a prova do timestamp. Você pode usar:
-O nome do arquivo .ots
-Ou o hash SHA-256 do arquivo original: `c8cc3f4bd08b7244031510ca17468f14fb02bddf32d4104f000c83d1cf33e141`

### Timestamp UTC:
**2026-01-22T23:XX:XXZ** (use a hora atual em UTC)

**Para converter hora local para UTC**:
-Se você está em Goiânia (UTC-3), adicione 3 horas
-Exemplo: Se são 23:00 em Goiânia → 02:00 UTC (do dia seguinte)
-Mas como queremos registrar hoje (22/01), use: **2026-01-22T23:00:00Z** ou a hora que você gerou o timestamp

---

## 🔍 COMO VERIFICAR O TIMESTAMP

### Opção 1: Site OpenTimestamps
1. Acesse: https://opentimestamps.org/
2. Clique em "Verify"
3. Faça upload do arquivo `.ots`
4. Veja o timestamp exato

### Opção 2: Linha de Comando (se tiver Python)
```bash
ots verify arquivo.ots
```

---

## 📋 PREENCHIMENTO RÁPIDO

**Rede**: OpenTimestamps  
**TXID/ID**: `c8cc3f4bd08b7244031510ca17468f14fb02bddf32d4104f000c83d1cf33e141`  
**Timestamp UTC**: `2026-01-22T23:00:00Z` (ajuste para a hora exata que você gerou)

---

## 💾 GUARDAR O ARQUIVO .ots

**IMPORTANTE**: Guarde o arquivo `.ots` junto com os PDFs assinados! Ele é a prova do timestamp.

Sugestão: Mova o arquivo `.ots` para a pasta `registro/release/private/` junto com os outros documentos.
