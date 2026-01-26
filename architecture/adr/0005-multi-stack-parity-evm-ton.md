# ADR 0005: Paridade de Stack e Funcionalidades (EVM ↔ TON)

**Status:** Aceito  
**Data:** 2026-01-25  
**Decisores:** NΞØ Architecture & NODE NEØ  
**Aplica-se a:** smart-core, smart-cli, docs

---

## Contexto

A expansão da NΞØ SMART FACTORY para a rede TON introduziu um ambiente técnico radicalmente diferente (modelo Actor, Assíncrono, FunC/Tact) em comparação com o ecossistema EVM (Síncrono, Solidity). 

Sem uma diretriz clara de paridade, o protocolo corria o risco de se tornar fragmentado, oferecendo recursos diferentes em chains diferentes, o que comprometeria a marca de "Operações Cirúrgicas" e a previsibilidade para parceiros institucionais.

---

## Decisão

Estabelecemos o princípio de **Multi-Stack Parity**. A NΞØ Smart Factory garante que o núcleo funcional do protocolo seja idêntico em todas as chains suportadas.

As decisões específicas para TON incluem:

1. **Paridade de Lógica Crítica:** O "Protocol Fee" de 5% (split de withdrawal) deve ser implementado no TON Jetton Minter exatamente como no NeoTokenV2.
2. **Standardization de Segurança:** O mecanismo Anti-bot (1 mint por wallet) e o Supply Cap imutável devem ser aplicados rigorosamente, adaptando as estruturas de dados do TON (Dictionaries) para espelhar os Mappings do Solidity.
3. **Equivalência de Interface:** Funções de visualização como `get_contract_info` devem retornar o mesmo set de dados que a `getContractInfo` do EVM.
4. **Mapeamento como Contrato:** O documento `EVM_TON_MAPPING.md` passa a ser a especificação técnica normativa para qualquer atualização do protocolo em ambas as redes.

---

## Justificativa

-**Integridade da Marca:** "NΞØ" deve significar o mesmo set de garantias e segurança independente da infraestrutura subjacente.
-**Eficiência Operacional:** Permite que a CLI (`nsf`) e a UI (`smart-ui`) tratem as diferentes chains com uma camada de abstração unificada.
-**Segurança Jurídica:** Facilita auditorias cross-chain, permitindo que checklists de conformidade sejam aplicados uniformemente.

---

## Consequências

### Positivas
-✅ Experiência de usuário consistente.
-✅ Facilidade de integração de bridges (as garantias de supply são as mesmas).
-✅ Checklist de auditoria unificado.

### Negativas
-❌ Maior esforço de desenvolvimento (exige portabilidade de lógica complexa).
-❌ Limita o uso de "atalhos" específicos de uma chain que não existem na outra.

---

## Implementação

Esta decisão está materializada em:
-**smart-core/contracts/ton/**: Implementação FunC/Tact seguindo estas regras.
-**docs/auditoria/EVM_TON_MAPPING.md**: Documentação técnica da paridade.

---

## Notas para Implementadores

Ao adicionar uma nova rede (ex: Solana, Polkadot), o primeiro passo deve ser preencher o checklist de paridade em relação ao **NeoTokenV2.sol** (EVM Reference).

---

**NΞØ PROTOCOL**: Operações Cirúrgicas em Web3  
> *Expand until silence becomes structure.*
