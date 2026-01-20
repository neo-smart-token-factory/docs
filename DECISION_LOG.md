# Registro de Decisões Técnicas (ADR)

## ADR-001: Arquitetura Moderna (Factory) vs. Geradores Genéricos

**Data:** 20 de Janeiro de 2026
**Status:** Decidido e Implementado

### Contexto
O mercado de criação de tokens tem sido dominado por "Token Generators" (repositórios como `erc20-token-generator` ou variantes BEP20). Esses sistemas geralmente operam sob a lógica de um "Canivete Suíço": um único contrato massivo contendo todas as funcionalidades possíveis (Mintable, Burnable, Taxable, Pausable, etc.), ativadas ou desativadas por boolean flags (`if/else`).

Durante a concepção da **NΞØ SMART FACTORY**, avaliamos se deveríamos seguir esse padrão ou adotar uma abordagem diferente.

### Análise Técnica

#### 1. Abordagem "Generator" (Canivete Suíço)
*   **Prós:** Facilidade inicial de implementação (um contrato serve para tudo).
*   **Contras (Bloatware):** O contrato final carrega bytecode morto. Se você cria um token simples sem taxas, a lógica de taxas ainda existe no blockchain, consumindo espaço e aumentando o custo de deploy (gas).
*   **Risco de Segurança:** Uma vulnerabilidade em uma função não utilizada (ex: lógica de taxas) pode comprometer o contrato inteiro, mesmo que a flag de taxas esteja desligada.
*   **Auditoria:** Dificulta a auditoria, pois o auditor precisa validar todas as permutações possíveis de flags.

#### 2. Abordagem NΞØ (Factory Modular & Cirúrgica)
*   **Base:** OpenZeppelin Contracts v5.0 (Padrão Ouro).
*   **Estratégia:** Implementação "Vanilla".
*   **Lógica:** Em vez de um contrato gigante cheio de flags, a Factory seleciona e implementa apenas o que é necessário.
*   **Segurança:** Herança direta de contratos auditados. Se o token não tem taxas, o código de taxas **não existe** no contrato deployado.

### Decisão
Optamos pela **Abordagem NΞØ (Factory Modular)** baseada em OpenZeppelin.

**Justificativa:**
1.  **Eficiência de Gas:** Deploys mais baratos e limpos.
2.  **Segurança Superior:** Menor superfície de ataque (código morto = zero).
3.  **Profissionalismo:** Tokens gerados são "puros" (`contract Token is ERC20`), sem a estigma de "tokens de gerador" que muitas vezes são associados a scams ou projetos amadores.
4.  **Longevidade:** Manutenção simplificada por depender de padrões da indústria (OZ) e não de repositórios mantidos por indivíduos.

### Consequências
*   O documento `ARCHITECTURE_SURGICAL.md` foi atualizado para remover referências a geradores antigos.
*   A base técnica oficial é **OpenZeppelin**.
*   Qualquer nova funcionalidade deve ser implementada via módulos/extensões, não inchando o contrato base.
