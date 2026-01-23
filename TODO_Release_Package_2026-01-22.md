# TODO: Pacote de Release - NΞØ SMART TOKEN FACTORY v1.0

**Data de criação**: 2026-01-22  
**Status**: Aguardando início  
**Data oficial do pacote**: 2026-01-22

---

## Fase 0: Regras de Segurança e Escopo ✅

### Regras Obrigatórias

- [x] **Não vazar segredos**
  - Não copiar nem resumir código sensível, chaves, endpoints privados, seeds, credenciais, tokens, links internos, dados de parceiros, ou qualquer informação confidencial fora do necessário
  - Não criar "exemplos" inventados
  - Se algo não estiver nos documentos, marcar como [PENDENTE]

- [x] **Dados pessoais do autor**
  - Dados pessoais (nome, CPF, e-mail) serão fornecidos para inclusão nos PDFs finais
  - Esses dados NÃO podem ficar versionados em arquivo público
  - Solução: gerar duas variantes:
    - **Public**: com redactions (ex: CPF mascarado)
    - **Private**: completo para uso offline

- [x] **Tom de voz e estilo**
  - Tom: técnico-jurídico, direto, sem marketing, sem floreio
  - Proibido: frases vagas tipo "inovador", "disruptivo", "revolucionário" sem explicação técnica
  - Obrigatório: linguagem defendível, reproduzível intelectualmente, com títulos objetivos

- [x] **Data e consistência**
  - Data oficial do pacote: 2026-01-22
  - Deve referenciar que há organização/documentação no GitHub desde 2025, sem afirmar detalhes que não conseguir verificar no repo

---

## Fase 1: Inventário e Extração do que Já Existe ✅

### Tarefa Principal

- [x] **Varrer o repo Docs e identificar documentos que descrevem:**
  - NΞØ SMART TOKEN FACTORY
  - Arquitetura, módulos, governança, automação
  - Wallet abstraction, MPC/MCP
  - Políticas de exposição de repositório
  - Outros documentos relevantes

- [x] **Criar arquivo de inventário:**
  - Arquivo: `registro/INVENTORY_Docs_Map_2026-01-22.md` ✅ CRIADO
  - Conteúdo necessário:
    - Lista de arquivos relevantes (path completo) ✅
    - Breve descrição de cada um (1 a 2 linhas) ✅
    - Lacunas percebidas (o que está faltando para o pacote mínimo) ✅
  - **Regra**: Sem conjectura. Só fatos encontrados. ✅

**Resultado**: 45+ documentos relevantes identificados e mapeados em 13 categorias.

---

## Fase 2: Gerar o Pacote Mínimo (4 arquivos) em Duas Variantes (Public/Private)

### Estrutura de Arquivos

**Pasta base**: `release/`

- `release/public/` - versões com redactions
- `release/private/` - versões completas (não commitar se repo for público)

### Arquivos a Criar

#### 00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22.pdf

- [ ] **Conteúdo obrigatório:**
  - Identificação do projeto e versão
  - Lista dos arquivos do pacote
  - Instrução de leitura
  - Referência à existência histórica no GitHub desde 2025 (sem exageros)
  - Separação clara entre Public/Private

#### 01_CORE_Authorship_and_Prior_Art_v1.0_2026-01-22.pdf
- [ ] **Conteúdo obrigatório:**
  - Bloco jurídico de autoria e anterioridade
  - Dados do autor como placeholders no template:
    - `[AUTHOR_FULL_NAME]`
    - `[AUTHOR_ID_DOCUMENT]`
    - `[AUTHOR_EMAIL]`
    - `[AUTHOR_CITY_COUNTRY]`
    - `[SIGNATURE]`
  - Cláusula de limites de uso
  - Data e local fixos

#### 02_SYSTEM_Executable_Concept_Overview_v1.0_2026-01-22.pdf
- [ ] **Conteúdo obrigatório:**
  - Descrição funcional objetiva do sistema
  - Diferenciais estruturais (explicados, não adjetivados)
  - Um diagrama simples (ASCII no mínimo, ou mermaid se permitido) cobrindo:
    - Factory
    - Token instances
    - Governança
    - Automação
    - Integração (wallet abstraction, miniapps, etc. se existir nos docs)
  - Seção "Estado do projeto" com base no que estiver documentado (sem inventar)

#### 03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt
- [ ] **Conteúdo obrigatório:**
  - Declaração resumida e hashable (texto exato, sem formatação fancy)
  - Placeholders do autor
  - Data, local e versão

#### 04_PROOF_SHA256_and_TXID_v1.0_2026-01-22.pdf
- [ ] **Conteúdo obrigatório:**
  - Tabela com SHA-256 de cada arquivo 00, 01, 02 e 03
  - Espaço para TXID e rede:
    - `[BLOCKCHAIN_NETWORK]`
    - `[TXID]`
    - `[UTC_TIMESTAMP]`
  - Instruções de como gerar hash e como validar

### Variantes

- [ ] Gerar versão **Public** (com redactions) em `registro/release/public/`
- [ ] Gerar versão **Private** (completa) em `registro/release/private/`
- [ ] **Atenção**: versão Private não deve ser commitada se o repo for público

---

## Fase 3: Política de Exposição do Repositório

### Tarefa

- [ ] **Criar documento de política:**
  - Arquivo: `registro/SECURITY_Repo_Visibility_Policy_v1.0_2026-01-22.md`
  - Localização: pasta `registro/`
  - **Conteúdo obrigatório:**
    - O que pode ser público (docs sanitizados, manifesto de hash, statement, índice sem PII)
    - O que nunca pode ser público (código sensível, chaves, segredos, dados pessoais completos, contratos internos)
    - Regra de revisão antes de publicar
    - Orientação para ferramentas de IA: "não inferir, não inventar, não autocompletar com dados privados"

---

## Fase 4: Checklist de Validação (Anti-alucinação)

### Tarefa

- [ ] **Criar checklist de validação:**
  - Arquivo: `registro/CHECKLIST_Release_Validation_2026-01-22.md`
  - **Checks objetivos obrigatórios:**
    - [ ] Todos os arquivos existem e nomes batem
    - [ ] Datas e versão coerentes
    - [ ] Nenhum placeholder ficou sem preencher na versão private
    - [ ] Public não contém PII
    - [ ] Hashes conferem
    - [ ] Statement (03) é idêntico ao usado para hash

---

## Saída Esperada

### Ao Final do Processo

- [ ] **Arquivos gerados** (paths exatos no repo)
- [ ] **Resumo curto** do que foi criado e onde
- [ ] **Lista de placeholders** que precisam ser preenchidos na versão private:
  - `[AUTHOR_FULL_NAME]`
  - `[AUTHOR_ID_DOCUMENT]`
  - `[AUTHOR_EMAIL]`
  - `[AUTHOR_CITY_COUNTRY]`
  - `[SIGNATURE]`
  - `[BLOCKCHAIN_NETWORK]`
  - `[TXID]`
  - `[UTC_TIMESTAMP]`

### Regra Importante

- [ ] Se qualquer informação necessária não estiver no Docs, marcar como **[PENDENTE]** e sugerir onde inserir manualmente

---

## Notas de Trabalho

### Placeholders Identificados

**Dados do Autor (para preenchimento manual):**
- `[AUTHOR_FULL_NAME]`
- `[AUTHOR_ID_DOCUMENT]`
- `[AUTHOR_EMAIL]`
- `[AUTHOR_CITY_COUNTRY]`
- `[SIGNATURE]`

**Dados de Blockchain (para preenchimento após geração):**
- `[BLOCKCHAIN_NETWORK]`
- `[TXID]`
- `[UTC_TIMESTAMP]`

### Estrutura de Pastas Esperada

```
docs/
├── registro/
│   ├── AUTHOR_DATA_TEMPLATE.md (não versionado)
│   ├── release/
│   │   ├── public/
│   │   │   ├── 00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22.pdf
│   │   │   ├── 01_CORE_Authorship_and_Prior_Art_v1.0_2026-01-22.pdf
│   │   │   ├── 02_SYSTEM_Executable_Concept_Overview_v1.0_2026-01-22.pdf
│   │   │   ├── 03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt
│   │   │   └── 04_PROOF_SHA256_and_TXID_v1.0_2026-01-22.pdf
│   │   └── private/ (não versionado)
│   │       ├── 00_INDEX_NEO_Smart_Token_Factory_v1.0_2026-01-22.pdf
│   │       ├── 01_CORE_Authorship_and_Prior_Art_v1.0_2026-01-22.pdf
│   │       ├── 02_SYSTEM_Executable_Concept_Overview_v1.0_2026-01-22.pdf
│   │       ├── 03_PROOF_Blockchain_Timestamp_Statement_v1.0_2026-01-22.txt
│   │       └── 04_PROOF_SHA256_and_TXID_v1.0_2026-01-22.pdf
│   ├── INVENTORY_Docs_Map_2026-01-22.md
│   ├── SECURITY_Repo_Visibility_Policy_v1.0_2026-01-22.md
│   └── CHECKLIST_Release_Validation_2026-01-22.md
└── [outros arquivos do projeto]
```

---

**Status**: Documento criado. Aguardando próximo passo.
