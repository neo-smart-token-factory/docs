# NΞØ Doctor CLI — Detalhamento da Fase A

> **Produto:** NΞØ Doctor (Módulo do `nsf` CLI)
> **Status:** Em desenvolvimento (Prioridade 0)
> **Mantra:** "Diagnóstico rápido, correção cirúrgica."

---

## 🩺 O Conceito "Doctor"
O **NΞØ Doctor** não é apenas um linter ou um verificador de ambiente. É uma ferramenta de **Inteligência Operacional** que garante que um protocolo Web3 está "sadio" antes, durante e depois do deployment.

### Por que alguém paga por isso?
No mundo Web3, um erro de configuração (ex: owner errado, proxy mal inicializado) custa caro. O Doctor CLI elimina a ansiedade do deployer fornecendo um selo de "Pronto para Produção".

---

## 💎 Funcionalidades Detalhadas (V0.1)

### 1. Smart Scan (Validação de Contratos)
O Doctor analisa o bytecode e o estado on-chain para verificar inconsistências.
-**Verificação de Inicialização:** Garante que o contrato `Initializable` não foi deixado aberto.
-**Proxy Integrity:** Valida se a implementação do Proxy (UUPS ou Transparent) coincide com os artefatos locais.
-**Supply Match:** Cruza o `MAX_SUPPLY` definido no código com o estado atual do contrato.

### 2. Security Pulse (Auditoria de Permissões)
Gera um mapa visual do poder dentro do contrato.
-**Rolestack:** Lista quem tem `DEFAULT_ADMIN_ROLE`, `MINTER_ROLE`, etc.
-**Ownership Trail:** Verifica se o `owner` atual é uma EOA, uma Multisig (Safe) ou se o contrato foi renunciado acidentalmente.
-**Blacklist/Pause Status:** Verifica se funções de emergência estão ativas ou configuradas corretamente.

### 3. Engine de Otimização de Gas
Analisa os custos operacionais em tempo real.
-**Benchmark de Mint:** Quanto custa o mint nas condições atuais de Gwei?
-**Sugeridor de Janela:** Baseado no histórico da rede (Base/Ethereum), sugere o melhor horário para operações de alto consumo (ex: bridge de liquidez).

### 4. Relatórios Exportáveis (Recurso PRO)
A CLI gera um arquivo `health-report-[timestamp].pdf` ou `Markdown` com branding da NΞØ.
-**Uso:** Fundadores podem anexar este relatório em seus decks de investidores ou canais da comunidade para provar a saúde técnica do projeto.

---

## 💰 Modelo de Monetização (Phase A Logic)

| Nível | Recursos | Modelo |
| :--- | :--- | :--- |
| **Básico (Livre)** | Check de ambiente, RPC Status, Saldo de gas. | Grátis |
| **Audit (Um Único Uso)** | Smart Scan completo + Security Pulse de 1 contrato. | Taxa fixa (ETH/Base) |
| **Operador (Licença)** | Uso ilimitado do Doctor + Relatórios exportáveis + Correção automática. | Assinatura anual (Licença NFT) |

---

## 🎨 Experiência do Usuário (CLI UX)
A interface deve ser "Premium Obsidian":
-**Spinners customizados:** Durante o scan.
-**Tabelas ANSI:** Para exibir a matriz de permissões.
-**Relatórios Visuais:** Uso de cores (Verde, Amarelo, Vermelho Crítico) para indicar a urgência.

```bash
# Exemplo de Comando
$ nsf doctor --deep --contract 0x... --output report.pdf
```

---

## 🛠️ TODO Lista Técnica (Prioridade)
-[ ] Implementar conector `ethers` robusto com fallback de múltiplos RPCs.
-[ ] Criar parser de ABI para identificar funções de governança automaticamente.
-[ ] Desenvolver gerador de relatórios em Markdown purificado.
-[ ] Gate de licença inicial (verificação de posse de token/NFT na carteira do operador).

---

### 👤 Governança do Produto

**Lead Engineer**: NODE NEØ
**NΞØ PROTOCOL**: Operações Cirúrgicas em Web3

> *Expand until silence becomes structure.*
