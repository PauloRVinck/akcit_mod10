# Regras de Negócio (RN)

> **Projeto:** Sistema de Gestão de Eventos (Eventus)  
> **Convenção de ID:** RN01, RN02, RN03...

---

## Introdução
Este documento especifica as Regras de Negócio que regem as operações do Sistema de Gestão de Eventos. As regras de negócio definem as políticas, restrições e premissas operacionais da empresa Eventus que condicionam o comportamento dos requisitos funcionais do sistema.

---

## Lista de Regras de Negócio

### RN01 - Modalidade Financeira do Evento
- **Descrição:** Todo evento ou workshop cadastrado no sistema deve obrigatoriamente possuir uma indicação clara de modalidade financeira: **Gratuito** ou **Pago**.
- **Impacto:** Determina o fluxo de inscrição do participante. Inscrições em eventos gratuitos avançam diretamente para a confirmação, enquanto eventos pagos exigem interação com o módulo financeiro.

### RN02 - Liberação de Inscrição Mediante Confirmação de Pagamento
- **Descrição:** Para eventos da modalidade **Pago**, a inscrição do participante permanecerá no status `Pendente de Pagamento` e a vaga reservada/confirmada somente será efetivamente liberada após a confirmação do recebimento do pagamento pela Equipe Financeira ou confirmação automática via Gateway de Pagamento.
- **Impacto:** Impede o acesso do participante a recursos restritos (ex.: emissão de comprovante definitivo, acesso ao evento, material de apoio) antes da quitação financeira.

### RN03 - Restrição de Simultaneidade de Workshops
- **Descrição:** Um mesmo participante é proibido de possuir inscrições ativas ou pendentes em dois ou mais workshops cujos horários de realização coincidam total ou parcialmente no mesmo dia.
- **Impacto:** O sistema deve executar a validação de conflito de horário antes de prosseguir com qualquer tentativa de confirmação de inscrição em múltiplos workshops.

### RN04 - Configurabilidade do Permissivo de Cancelamento
- **Descrição:** A permissão de cancelamento de inscrição por parte do participante não é global; ela é um parâmetro configurável individualmente para cada evento no momento de seu cadastro pelo Organizador (`permite_cancelamento: true/false`).
- **Impacto:** Se o evento for configurado com `permite_cancelamento = false`, a opção de autosserviço de cancelamento não ficará disponível para o participante.

### RN05 - Gestão de Esgotamento de Vagas e Lista de Espera
- **Descrição:** Quando o total de inscrições confirmadas/reservadas atingir a capacidade máxima (limite de vagas) definida para o evento pelo Organizador, o sistema deve automaticamente alterar a modalidade de novas inscrições para a `Lista de Espera`.
- **Impacto:** A lista de espera deve respeitar rigorosamente a ordem cronológica de registro (FIFO - *First In, First Out*). Havendo desistência/cancelamento de uma inscrição confirmada, o primeiro participante da lista de espera assume o direito à vaga.

### RN06 - Condicionalidade para Emissão de Certificados
- **Descrição:** A emissão de certificado de participação é estritamente vinculada à realização do evento e à validação da presença efetiva do participante na atividade.
- **Impacto:** O botão de emissão de certificado permanecerá desabilitado até que a data do evento tenha passado E o organizador tenha efetuado a confirmação de presença do participante no sistema.

### RN07 - Política de Elegibilidade a Reembolso (Pendente de Especificação Final)
- **Descrição:** Em caso de cancelamento de inscrição em eventos pagos que permitam cancelamento, o direito a reembolso total ou parcial depende do cumprimento de prazos limites configurados (ex.: até X dias antes da data do evento).
- **Impacto:** O cálculo e a aprovação do reembolso na Equipe Financeira dependerão da validação automatizada desta regra de prazo.
