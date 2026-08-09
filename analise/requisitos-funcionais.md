# Requisitos Funcionais (RF)

> **Projeto:** Sistema de Gestão de Eventos (Eventus)  
> **Convenção de ID:** RF01, RF02, RF03...

---

## Introdução
Este documento apresenta a especificação dos Requisitos Funcionais do Sistema de Gestão de Eventos da empresa Eventus. Cada requisito foi derivado das declarações dos stakeholders coletadas durante a fase de elicitação. Em conformidade com os critérios de qualidade da norma **ISO/IEC/IEEE 29148**, todos os requisitos aqui descritos foram formulados para serem **completos, consistentes, não ambíguos, verificáveis, viáveis, necessários e rastreáveis**.

---

## Tabela de Requisitos Funcionais

| ID | Descrição do Requisito | Stakeholder de Origem | Critério de Verificação |
| :--- | :--- | :--- | :--- |
| **RF01** | O sistema deve permitir que os participantes visualizem um catálogo de eventos disponíveis, apresentando título, data, horário, local/link, quantidade de vagas disponíveis e valor da inscrição. | Participantes | Teste de interface exibindo a listagem completa e correta de eventos cadastrados no banco de dados. |
| **RF02** | O sistema deve permitir que o participante realize sua inscrição em um ou mais eventos/workshops selecionados. | Participantes | Inclusão com sucesso do registro do participante no banco de dados para o evento selecionado. |
| **RF03** | O sistema deve gerar e enviar automaticamente um comprovante de inscrição em formato digital (ex.: PDF e/ou e-mail) ao participante imediatamente após a conclusão do processo de inscrição. | Participantes | Recebimento do documento com identificador único de inscrição e dados do evento no e-mail do participante. |
| **RF04** | O sistema deve permitir que o participante solicite o cancelamento de sua inscrição por meio de autosserviço no painel do sistema, respeitando as permissões do evento. | Participantes | Execução da mudança de status da inscrição para "Cancelada" sem intervenção manual da organização. |
| **RF05** | O sistema deve disponibilizar para download a emissão do certificado de participação em formato PDF para os participantes que concluírem o evento e tiverem presença registrada. | Participantes | Geração e download do certificado contendo nome do participante, carga horária e autenticação digital. |
| **RF06** | O sistema deve permitir que o participante solicite inscrição em múltiplos workshops agendados para o mesmo dia, desde que não possuam horários sobrepostos. | Participantes | Validação pelo sistema permitindo inscrições no mesmo dia em horários distintos e bloqueando em horários idênticos. |
| **RF07** | O sistema deve permitir que os organizadores cadastrem, editem, alterem o status e excluam (logicamente) eventos, definindo título, descrição, carga horária, data/hora, limite de vagas, valor e se o evento aceita cancelamento. | Organizadores | Execução das operações de CRUD de eventos no painel administrativo e persistência dos dados. |
| **RF08** | O sistema deve realizar o controle e a atualização automática da contagem de vagas disponíveis para cada evento em tempo real a cada nova inscrição ou cancelamento. | Organizadores | Verificação do decremento do saldo de vagas ao efetuar inscrição e incremento ao processar cancelamento. |
| **RF09** | O sistema deve direcionar automaticamente o participante para uma lista de espera quando as vagas do evento atingirem o limite máximo configurado. | Organizadores | Tentativa de inscrição em evento lotado resulta no registro do participante no status "Lista de Espera" com timestamp. |
| **RF10** | O sistema deve disponibilizar aos organizadores um painel (dashboard) com o número total de inscritos, vagas remanescentes, participantes na lista de espera e status de pagamentos em tempo real. | Organizadores | Exibição correta das métricas agregadas e consolidadas no painel do organizador. |
| **RF11** | O sistema deve validar e impedir a inscrição de um mesmo participante em dois ou mais workshops cujos horários de realização coincidam total ou parcialmente. | Organizadores / Participantes | Emissão de mensagem de erro e bloqueio da operação ao tentar inscrever em workshops com sobreposição de horário. |
| **RF12** | O sistema deve suportar o cadastro de eventos gratuitos e eventos pagos, adaptando o fluxo de inscrição conforme o tipo de cobrança do evento. | Equipe Financeira | Verificação do fluxo direto de confirmação para eventos gratuitos e redirecionamento de pagamento para eventos pagos. |
| **RF13** | O sistema deve permitir que a Equipe Financeira consulte a lista de inscrições com pagamentos pendentes e efetue a confirmação manual ou receba a confirmação via webhook de gateway de pagamento. | Equipe Financeira | Alteração do status da inscrição de "Pendente de Pagamento" para "Confirmada" mediante ação manual ou integração. |
| **RF14** | O sistema deve permitir que a Equipe Financeira visualize e processe a lista de solicitações de reembolso decorrentes de cancelamentos de inscrições elegíveis. | Equipe Financeira | Atualização do status financeiro para "Reembolsado" e registro do valor devolvido. |
| **RF15** | O sistema deve permitir aos palestrantes visualizar a agenda detalhada de suas atividades atribuídas e a listagem dos participantes devidamente inscritos nas suas sessões. | Palestrantes | Acesso restrito do palestrante aos seus eventos e visualização da lista nominal de alunos inscritos. |

---

## Matriz de Rastreabilidade Simplificada

| ID Requisito | Origem na Elicitação | Responsável / Papel |
| :--- | :--- | :--- |
| **RF01** | "Gostaria de visualizar todos os eventos disponíveis em um único lugar." | Participante |
| **RF02** | "Inscrições por formulários on-line e planilhas..." / Visão Geral | Participante |
| **RF03** | "Seria interessante receber um comprovante logo após a inscrição." | Participante |
| **RF04** | "Gostaria de cancelar minha inscrição sem precisar entrar em contato..." | Participante |
| **RF05** | "Quero conseguir emitir meu certificado depois do evento." | Participante |
| **RF06** | "Gostaria de me inscrever em vários workshops que acontecerão no mesmo dia." | Participante |
| **RF07** | "Criar eventos, controlar vagas, acompanhar inscrições..." | Organizador |
| **RF08** | "Precisamos controlar automaticamente o número de vagas." | Organizador |
| **RF09** | "Quando um evento lotar, seria interessante criar uma lista de espera." | Organizador |
| **RF10** | "Gostaríamos de acompanhar a quantidade de inscritos em tempo real." | Organizador |
| **RF11** | "Os workshops que acontecem no mesmo horário devem ocorrer simultaneamente." | Organizador / Participante |
| **RF12** | "Alguns eventos são gratuitos e outros exigem pagamento." | Equipe Financeira |
| **RF13** | "Precisamos confirmar os pagamentos antes de liberar determinadas inscrições." | Equipe Financeira |
| **RF14** | "Em alguns casos o participante tem direito ao reembolso..." | Equipe Financeira |
| **RF15** | "Gostaria de consultar a lista de participantes inscritos em minhas atividades." | Palestrante |
