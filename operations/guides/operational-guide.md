# Guia Operacional NΞØ SMART FACTORY v0.5.3

> **Status Atual:** Multichain Foundation (Base, Polygon, Arbitrum)
> **Data:** 20 de Janeiro de 2026

Este documento explica como utilizar as ferramentas da NΞØ SMART FACTORY no estado atual ("Ignição"), onde a interface visual ainda não está disponível, mas o motor interno (`smart-cli`) está totalmente funcional via terminal.

## 🎯 Visão Geral

O projeto está na versão **v0.5.3**.
-**O que está pronto:** O cérebro neural da fábrica (simuladores, auditores), contratos multichain (NeoTokenV2), bridge manual e integração MiniApp.
-**O que falta:** A "face" da fábrica (website, dashboard visual).

Você pode (e deve) usar o terminal para acessar todas as funcionalidades críticas hoje.

---

## 🛠️ Como Usar (Via Terminal)

Todas as operações são feitas executando o script principal do `smart-cli` via Node.js na raiz do projeto.

### 1. Criar um Rascunho de Token
Cria a estrutura inicial do token sem fazer deploy.

```bash
node smart-cli/ops-handler.js "NEO::token draft NOME_DO_TOKEN"
```

*Exemplo:*
```bash
node smart-cli/ops-handler.js "NEO::token draft MAGMA"
```

### 2. Simulação de Ecossistema (OBRIGATÓRIO)
O check mais completo. Realiza uma simulação de 7 dias, verifica segurança, tokenômica e consistência narrativa. **Sempre execute isso antes de pensar em deploy.**

```bash
node smart-cli/ops-handler.js "NEO::simulate NOME_DO_TOKEN"
```

*O que ele verifica:*
-🛡️ **Segurança:** Riscos de exploit, travas incorretas.
-💰 **Economia:** Se a conta fecha (Supply vs Distribuição).
-📜 **Narrativa:** Se existe manifesto e alinhamento com a cultura NΞØ.
-📈 **Projeção:** Estima holders e volume para os primeiros 7 dias.

### 3. Gerar Manifesto
Se o simulador acusar falta de manifesto, gere um automaticamente:

```bash
node smart-cli/ops-handler.js "NEO::token manifest NOME_DO_TOKEN"
```

### 4. Auditoria Rápida
Uma verificação focada puramente em riscos técnicos e econômicos (menos narrativa que o `simulate`).

```bash
node smart-cli/ops-handler.js "NEO::token audit NOME_DO_TOKEN"
```

### 5. Deploy Real (Phase 2)
Executa o deploy real na rede configurada (Requer aprovação do simulador).

```bash
node smart-cli/ops-handler.js "NEO::token deploy NOME_DO_TOKEN"
```

### 6. Verificar Status do Projeto
Para ver o progresso geral da fábrica (o que falta para a v1.0).

```bash
node smart-cli/ops-handler.js "NEO::status"
```

---

## ⚠️ Solução de Problemas Comuns

### Erro: `Cannot read properties of null`
Se você encontrar este erro ao criar um draft, certifique-se de que está usando a versão mais recente do código (já corrigida em 20/01/2026). Se persistir, tente passar uma configuração vazia:

```bash
node smart-cli/ops-handler.js "NEO::token draft TOKEN {}"
```

### Erro: `Token não encontrado`
Certifique-se de que você executou o `draft` **antes** de tentar simular ou auditar. O token precisa existir em `tokens/` (gerado pelo draft) para ser lido.

---

## 📝 Próximos Passos

1. Use o `draft` para visualizar sua ideia.
2. Refine o arquivo JSON gerado em `smart-cli/tokens/` manualmente se precisar de ajustes finos.
3. Use o `simulate` repetidamente até obter um veredito **APPROVED**.
4. Use o `deploy` para executar o lançamento real via CLI (Phase 2).
