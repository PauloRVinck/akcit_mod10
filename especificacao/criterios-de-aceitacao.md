# Critérios de Aceitação (BDD - Given / When / Then)

> **Projeto:** Sistema de Gestão de Eventos (Eventus)  
> **Formato:** Gherkin / BDD (Dado / Quando / Então) em Tabelas Markdown  
> **Escopo:** Todas as Histórias de Usuário (US01 a US11) com Cenários Principais e Alternativos/Exceções.

---

## US01 - Visualização do Catálogo de Eventos

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA01.1** | Principal | Dado que o participante acessa a página inicial do sistema | Quando a lista de eventos é carregada | Então o sistema deve exibir todos os eventos ativos com título, data, horário, vagas disponíveis e preço. |
| **CA01.2** | Alternativo (Filtro) | Dado que o participante está na página de catálogo de eventos | Quando ele digita o nome de um evento no campo de busca ou seleciona uma data específica | Então o sistema deve filtrar a listagem em tempo real trazendo apenas os eventos que atendem aos filtros. |
| **CA01.3** | Exceção (Nenhum Resultado) | Dado que o participante aplica um filtro de busca | Quando nenhum evento cadastrado corresponder aos critérios | Então o sistema deve exibir a mensagem: "Nenhum evento encontrado para os filtros selecionados". |

---

## US02 - Realização de Inscrição em Eventos

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA02.1** | Principal (Evento Gratuito) | Dado que o participante seleciona um evento gratuito com vagas disponíveis | Quando preenche seus dados cadastrais e confirma a inscrição | Então a inscrição é gravada com status `Confirmada` e uma mensagem de sucesso é apresentada na tela. |
| **CA02.2** | Alternativo (Evento Pago) | Dado que o participante seleciona um evento pago com vagas disponíveis | Quando ele confirma os dados da inscrição | Então o sistema grava a inscrição no status `Pendente de Pagamento` e redireciona para a tela de pagamento. |
| **CA02.3** | Exceção (Conflito de Horário) | Dado que o participante já possui inscrição confirmada no "Workshop A" das 14h às 16h | Quando tenta se inscrever no "Workshop B" do mesmo dia com horário das 15h às 17h | Então o sistema bloqueia a inscrição e exibe a mensagem de erro: "Não é possível se inscrever em workshops com horários conflitantes". |

---

## US03 - Recebimento de Comprovante de Inscrição

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA03.1** | Principal | Dado que o participante concluiu com sucesso uma inscrição gratuita ou teve o pagamento confirmado | Quando a transação é finalizada no sistema | Então o sistema envia automaticamente um e-mail de comprovante contendo o QR Code/Código de Inscrição e dados do evento. |
| **CA03.2** | Exceção (Falha no Envio de E-mail) | Dado que o serviço externo de e-mail apresenta instabilidade momentânea | Quando a inscrição é confirmada | Então a inscrição é mantida como confirmada e o comprovante fica disponível para download direto na dashboard do participante. |

---

## US04 - Autosserviço de Cancelamento de Inscrição

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA04.1** | Principal | Dado que o participante possui inscrição confirmada em um evento cujas regras permitem cancelamento | Quando ele clica no botão "Cancelar Inscrição" e confirma a caixa de diálogo | Então o status da inscrição é alterado para `Cancelada`, a vaga do evento é liberada e uma notificação é enviada ao participante. |
| **CA04.2** | Exceção (Evento Não Permite Cancelamento) | Dado que o evento foi configurado pelo organizador com a regra `permite_cancelamento = false` | Quando o participante visualiza os detalhes de sua inscrição | Então o botão de cancelamento não deve estar visível/habilitado na interface e uma mensagem informativa explicitará a regra do evento. |

---

## US05 - Emissão de Certificado de Participação

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA05.1** | Principal | Dado que o evento já foi encerrado E o participante teve sua presença confirmada | Quando o participante clica em "Emitir Certificado" na sua área logada | Então o sistema gera e inicia o download do arquivo PDF do certificado com código de verificação autêntico. |
| **CA05.2** | Exceção (Sem Presença Confirmada) | Dado que o evento foi encerrado mas o participante não possui registro de presença | Quando acessa a página de certificados | Então o sistema exibe o status "Certificado Indisponível: Presença não registrada no evento". |

---

## US06 - Entrada Automática em Lista de Espera

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA06.1** | Principal | Dado que o evento atingiu 100% de ocupação de suas vagas | Quando um novo participante tenta se inscrever | Então o sistema altera a ação para "Entrar na Lista de Espera" e grava a solicitação no status `Lista de Espera` com posição cronológica. |
| **CA06.2** | Alternativo (Convocação por Desistência) | Dado que um participante da lista de espera está na 1ª posição E ocorre um cancelamento de vaga | Quando a vaga é liberada | Então o sistema altera o status da inscrição para `Convocado` e envia um e-mail de notificação concedendo prazo para confirmação. |

---

## US07 - Gestão de Eventos e Controle de Vagas

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA07.1** | Principal | Dado que o organizador está autenticado no painel administrativo | Quando ele preenche o formulário de novo evento com título, data, vagas, valor e salva | Então o sistema valida os dados cadastrais, persiste o evento no banco de dados e o disponibiliza no catálogo público. |
| **CA07.2** | Exceção (Dados Inválidos) | Dado que o organizador tenta cadastrar um evento | Quando define um número de vagas menor ou igual a zero ou data no passado | Então o sistema exibe mensagens de erro de validação nos campos correspondentes e impede o salvamento. |

---

## US08 - Acompanhamento do Painel de Inscrições em Tempo Real

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA08.1** | Principal | Dado que o organizador acessa a dashboard do evento "Congresso 2026" | Quando a página é carregada | Então o sistema exibe os contadores atualizados em tempo real: Total Inscritos, Vagas Restantes, Em Lista de Espera e Inscrições Pagas. |

---

## US09 - Confirmação de Pagamento e Liberação de Inscrição

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA09.1** | Principal | Dado que existe uma inscrição no status `Pendente de Pagamento` | Quando a equipe financeira registra a confirmação de pagamento manual ou o webhook do gateway envia o status de pago | Então o status da inscrição muda para `Confirmada` e o participante é notificado por e-mail. |
| **CA09.2** | Exceção (Pagamento Recusado/Expirado) | Dado que o pagamento do participante é recusado pela operadora | Quando o status de recusa é recebido | Então a inscrição assume o status `Pagamento Recusado` e a vaga temporária é liberada para novo participante. |

---

## US10 - Gestão de Reembolsos de Cancelamento

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA10.1** | Principal | Dado que o participante cancelou uma inscrição em evento pago com direito a reembolso | Quando a equipe financeira acessa o painel de reembolsos e clica em "Efetuar Estorno" | Então o sistema registra a devolução, altera o status financeiro para `Reembolsado` e notifica o participante. |

---

## US11 - Consulta da Agenda e Lista de Participantes pelo Palestrante

| ID Cenário | Tipo de Cenário | Dado (Given) | Quando (When) | Então (Then) |
| :--- | :--- | :--- | :--- | :--- |
| **CA11.1** | Principal | Dado que o palestrante faz login na sua área exclusiva | Quando clica sobre uma de suas atividades agendadas | Então o sistema exibe a lista nominal dos participantes inscritos (respeitando as regras de privacidade LGPD). |
