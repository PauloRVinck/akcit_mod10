# Dúvidas, Ambiguidade e Lacunas de Requisitos

> **Projeto:** Sistema de Gestão de Eventos (Eventus)  
> **Objetivo:** Matriz de Esclarecimento de Pendências para Entrevista com Stakeholders

---

## Introdução
Durante a análise do documento de elicitação inicial, foram identificados pontos omissos, regras não definidas e comportamentos ambíguos na seção de observações. Para evitar premissas incorretas que gerem retrabalho no desenvolvimento, este documento consolida a lista de **perguntas objetivas** a serem validadas com os stakeholders, acompanhadas do respectivo **impacto técnico e de negócio**.

---

## Matriz de Perguntas de Esclarecimento

| ID | Ponto Observado / Lacuna | Pergunta Objetiva para os Stakeholders | Impacto no Requisito / Arquitetura | Stakeholder Alvo |
| :--- | :--- | :--- | :--- | :--- |
| **LAC01** | **Prazo Limite para Cancelamento** | Até quando (quantos dias ou horas antes do evento) o participante pode realizar o cancelamento da sua inscrição via autosserviço? | **Impacto:** Afeta a validação da solicitação em **RF04** e a regra **RN04**. Impede o cancelamento de última hora que impossibilite o reaproveitamento da vaga. | Organizadores / Financeiro |
| **LAC02** | **Regras e Política de Reembolso** | Em quais situações específicas haverá devolução de valor (reembolso total ou parcial)? Existe retenção de taxa administrativa em caso de desistência pelo participante? | **Impacto:** Modifica o fluxo financeiro em **RF14** e na regra **RN07**. Exige a implementação de regras de cálculo de estorno no backend. | Equipe Financeira |
| **LAC03** | **Mecanismo da Lista de Espera** | Ao surgir uma vaga cancelada, o sistema deve convocar automaticamente o próximo da lista concedendo um prazo (ex.: 24h) para pagamento/aceite ou a vaga é atribuída e confirmada imediatamente? | **Impacto:** Define a lógica de filas (background jobs/cron), máquinas de estado de inscrição (**RF09**, **RN05**) e envio de notificações temporizadas. | Organizadores |
| **LAC04** | **Regra de Emissão de Certificados** | A liberação do certificado será totalmente automática após a data fim do evento ou dependerá de uma confirmação/registro manual de presença por parte da organização? | **Impacto:** Determina a necessidade de uma tela/funcionalidade de "Registro de Presença" para os Organizadores e a regra de bloqueio/liberação em **RF05** e **RN06**. | Organizadores / Participantes |
| **LAC05** | **Canais e Formatos de Notificação** | Por quais canais de comunicação (E-mail, SMS, WhatsApp) os comprovantes de inscrição, alertas de vaga e confirmações de pagamento devem ser enviados? | **Impacto:** Impacta a arquitetura de integração do backend (serviços de e-mail como SendGrid/SES ou APIs de mensageria WhatsApp/Twilio) em **RF03**. | Equipe de TI / Organizadores |
| **LAC06** | **Momento da Reserva de Vaga** | A vaga é temporariamente reservada no momento em que o participante inicia o checkout/pagamento (com timer de expiração) ou a vaga só é garantida no momento da liquidação efetiva do pagamento? | **Impacto:** **CRÍTICO.** Impacta o controle de concorrência em **RF08**, prevenção de *overbooking*, suporte a transações com cartão/PIX e gerenciamento de sessões/estoque de vagas. | Equipe Financeira / TI / Organizadores |
| **LAC07** | **Tratamento de Workshops Simultâneos** | Como o sistema deve sinalizar a tentativa de inscrição em workshops simultâneos? O sistema deve impedir a seleção visualmente na tela de catálogo ou emitir um erro na validação do formulário? | **Impacto:** Afeta a experiência de usuário (UX) do frontend React e as rotas de validação de negócios em **RF11** e **RN03**. | Participantes / TI |
| **LAC08** | **Privacidade e Visibilidade de Dados pelo Palestrante** | Quais dados específicos dos participantes inscritos podem ser visualizados pelos palestrantes (ex.: apenas nome e e-mail corporativo ou telefone e cargo)? | **Impacto:** Impacta diretamente a conformidade com a LGPD (**RNF03**), controle de permissões em **RF15** e minimização da exposição de dados sensíveis. | Palestrantes / TI / Jurídico |
| **LAC09** | **Definição dos Requisitos Não Funcionais** | Quais são as metas oficiais de tempo de resposta, volume de acessos simultâneos previstos no pico e nível de serviço (SLA) exigidos para a infraestrutura? | **Impacto:** Dimensionamento dos containers Docker, escolha das instâncias cloud, estratégias de cache (Redis) e testes de estresse (RNF01 a RNF08). | Equipe de TI |

---

## Próximos Passos
Recomenda-se agendar uma sessão de alinhamento (*workshop de validação de requisitos*) com os organizadores e a equipe financeira para responder a estas 9 questões antes do congelamento (*baseline*) da especificação.
