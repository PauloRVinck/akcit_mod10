# Sistema de Gestão de Eventos (Eventus) - Engenharia de Requisitos com GenAI

## 1. Descrição do Projeto

Análise e especificação de requisitos para o Sistema de Gestão de Eventos da empresa Eventus (inscrições, pagamentos, controle de vagas, lista de espera e emissão de certificados).

---

## 2. Uso da IA Generativa

- **Ferramenta Utilizada:** Claude Code (modelo Claude Sonnet, Anthropic).
- **Como a IA Apoiou o Projeto:**
  - Classificação de Requisitos Funcionais, Regras de Negócio e Dúvidas/Lacunas.
  - Proposta de Requisitos Não Funcionais candidatos (Segurança, LGPD, Desempenho, Acessibilidade).
  - Criação de Histórias de Usuário, Critérios de Aceitação em BDD e Casos de Uso detalhados.
  - Auto-revisão crítica para evitar regras alucinadas sem validação prévia.

---

## 3. Análise Crítica (Aceites e Descartes)

- **Sugestões Aceitas:**
  - Proposta de RNFs essenciais (segurança TLS, RBAC, LGPD e SLA < 2s).
  - Separação estrita entre Requisitos Funcionais e Regras de Negócio.
  - Inclusão de cenários de exceção e erros para todos os critérios BDD.
- **Sugestões Descartadas / Modificadas:**
  - *Descartado:* Prazos e percentuais arbitrários de reembolso (convertidos em perguntas para os stakeholders em `duvidas-e-lacunas.md`).
  - *Modificado:* Reserva de vaga alterada para incluir tempo limite no status `Pendente de Pagamento`.
  - *Modificado:* Liberação de certificado condicionada à confirmação explicita de presença.

---

## 4. Justificativa dos Artefatos Escolhidos

Foi adotada uma **abordagem híbrida**:

- **Histórias de Usuário:** Mapeiam o valor do sistema de forma ágil para os papéis (Participante, Organizador, Financeiro, Palestrante).
- **Critérios de Aceitação (BDD):** Garantem cenários de teste claros em tabelas (Dado / Quando / Então).
- **Casos de Uso Detalhados:** Aplicados **apenas às 3 funcionalidades mais complexas** (*UC01: Inscrição e Lista de Espera*, *UC02: Cancelamento/Reembolso*, *UC03: Emissão de Certificado*).

*Justificativa:* Histórias de usuário cobrem bem o que é simples. As funcionalidades complexas (concorrência de vagas, lista FIFO, pagamentos) exigem a profundidade dos Casos de Uso para evitar ambiguidades no desenvolvimento.

---
