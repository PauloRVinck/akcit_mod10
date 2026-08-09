# Casos de Uso Detalhados (Use Cases)

> **Projeto:** Sistema de Gestão de Eventos (Eventus)  
> **Escopo:** Especificação Detalhada das Funcionalidades Complexas

---

## UC01 - Inscrever-se em Evento com Controle de Vagas e Lista de Espera

### 1. Descrição do Caso de Uso
- **Identificador:** UC01
- **Nome:** Inscrever-se em Evento com Controle de Vagas e Lista de Espera
- **Objetivo:** Permitir que o participante selecione um ou mais eventos/workshops, efetue a inscrição com checagem de concorrência de horários e controle automático de saldo de vagas ou ingresso em lista de espera.
- **Ator Principal:** Participante
- **Atores Secundários:** Sistema de Gateway de Pagamento, Sistema de E-mail/Notificação
- **Pré-condições:** 
  1. O participante deve estar autenticado no sistema.
  2. O evento ou workshop deve estar no status "Ativo/Com Inscrições Abertas".

### 2. Fluxo Principal
1. O participante navega pelo catálogo e seleciona o evento/workshop desejado.
2. O participante clica na opção "Inscrever-se".
3. O sistema verifica se o participante já possui outra inscrição confirmada ou pendente para o mesmo dia e horário (Regra **RN03**).
4. O sistema verifica o saldo de vagas disponíveis no evento (Regra **RN05**).
5. O sistema confirma que existem vagas disponíveis (`vagas_disponiveis > 0`).
6. O sistema verifica a modalidade do evento (**RN01**):
   - **Caso seja Gratuito:** O sistema reserva a vaga, altera o status da inscrição para `Confirmada` e decrementa 1 vaga do total disponível.
   - **Caso seja Pago:** O sistema altera o status para `Pendente de Pagamento`, reserva temporariamente a vaga e redireciona o participante para o Gateway de Pagamento.
7. O sistema solicita o envio automático do comprovante de inscrição por e-mail ao participante (**RF03**).
8. O sistema exibe a mensagem de confirmação de inscrição realizada com sucesso.
9. O caso de uso é encerrado.

### 3. Fluxos Alternativos e de Exceção

#### FA01 - Redirecionamento para Lista de Espera (Evento Lotado)
- **Desvio no Passo 5:** O sistema verifica que `vagas_disponiveis == 0`.
- **Ações:**
  1. O sistema exibe mensagem: "Este evento está com vagas esgotadas. Deseja entrar na Lista de Espera?".
  2. O participante confirma o ingresso na lista de espera.
  3. O sistema grava o registro do participante com status `Lista de Espera` mantendo o timestamp e a posição cronológica (FIFO).
  4. O sistema exibe confirmação: "Você está na posição X da Lista de Espera".
  5. O caso de uso é encerrado.

#### FA02 - Processamento de Pagamento em Evento Pago
- **Desvio no Passo 6 (Evento Pago):**
- **Ações:**
  1. O participante informa os dados de pagamento (Cartão / PIX) e submete a transação.
  2. O Gateway de Pagamento confirma a aprovação da cobrança.
  3. A Equipe Financeira / Webhook atualiza a inscrição para `Confirmada`.
  4. O sistema envia o comprovante de pagamento e confirmação de vaga.
  5. Retorna ao Passo 7 do fluxo principal.

#### FE01 - Conflito de Horário entre Workshops
- **Desvio no Passo 3:** O sistema detecta que o participante já está inscrito em outro workshop no mesmo horário.
- **Ações:**
  1. O sistema interrompe o processo de inscrição.
  2. Exibe mensagem de erro: "Inscrição não permitida: Você já possui a inscrição no workshop '[Nome do Evento]' que ocorre no mesmo horário ([Horário Start] - [Horário End]).".
  3. O sistema não altera o saldo de vagas.
  4. O caso de uso é encerrado sem efetivar a inscrição.

#### FE02 - Expiração de Tempo de Pagamento
- **Desvio no Passo FA02:** O participante não conclui o pagamento do PIX/Cartão dentro do prazo limite (ex.: 30 minutos).
- **Ações:**
  1. O sistema cancela a reserva temporária da vaga.
  2. Altera o status da inscrição para `Inscrição Cancelada - Pagamento Expirado`.
  3. A vaga retorna ao saldo de vagas disponíveis do evento.

### 4. Pós-condições
- A vaga no evento é reduzida em 1 unidade (para eventos com vagas) OU o participante é inserido na lista de espera.
- O registro de inscrição é gravado no banco de dados com a auditoria completa (data/hora, usuário, status).

---

## UC02 - Cancelar Inscrição e Processar Reembolso

### 1. Descrição do Caso de Uso
- **Identificador:** UC02
- **Nome:** Cancelar Inscrição e Processar Reembolso
- **Objetivo:** Permitir ao participante cancelar uma inscrição prévia e, caso seja um evento pago elegível, acionar o fluxo de reembolso pela Equipe Financeira.
- **Ator Principal:** Participante
- **Atores Secundários:** Equipe Financeira, Sistema de Notificação
- **Pré-condições:** 
  1. O participante possui inscrição no status `Confirmada` ou `Pendente de Pagamento`.
  2. O evento possui o parâmetro `permite_cancelamento = true` (Regra **RN04**).

### 2. Fluxo Principal
1. O participante acessa a área "Minhas Inscrições" no sistema.
2. O sistema exibe a lista de inscrições do participante.
3. O participante clica na opção "Cancelar Inscrição" correspondente ao evento desejado.
4. O sistema verifica a regra do evento e confirma que o cancelamento é permitido (**RN04**).
5. O sistema exibe uma tela de confirmação do cancelamento solicitando o motivo (opcional).
6. O participante confirma o cancelamento.
7. O sistema altera o status da inscrição para `Cancelada`.
8. O sistema incrementa em +1 a quantidade de vagas disponíveis do evento (**RF08**).
9. O sistema verifica se o evento era **Pago** e se houve valor quitado:
   - **Se Sim:** O sistema gera uma solicitação de reembolso no módulo da Equipe Financeira (**RF14**).
10. O sistema envia e-mail de confirmação de cancelamento ao participante.
11. O sistema dispara a rotina de verificação da **Lista de Espera** para convocar o próximo participante da fila (se houver).
12. O caso de uso é encerrado.

### 3. Fluxos Alternativos e de Exceção

#### FA01 - Convocação Automática da Lista de Espera
- **Ponto de Extensão no Passo 11:** Existe pelo menos 1 participante no status `Lista de Espera` para este evento.
- **Ações:**
  1. O sistema busca o participante na posição 1 da lista de espera (FIFO).
  2. O sistema altera o status daquele participante para `Convocado`.
  3. O sistema envia um e-mail de notificação com prazo estipulado para confirmação/pagamento da vaga.

#### FE01 - Evento Não Permite Cancelamento
- **Desvio no Passo 4:** O sistema identifica que `permite_cancelamento == false`.
- **Ações:**
  1. O sistema desabilita a ação de cancelamento na tela do participante.
  2. Exibe mensagem explicativa: "Este evento não permite cancelamento de inscrição conforme o regulamento definido pela organização.".
  3. O caso de uso é encerrado sem alterações.

### 4. Pós-condições
- A inscrição tem seu status alterado para `Cancelada`.
- O saldo de vagas do evento é atualizado (+1 vaga livre).
- Registra-se o pedido de reembolso na fila financeira (se aplicável).

---

## UC03 - Emitir Certificado de Participação

### 1. Descrição do Caso de Uso
- **Identificador:** UC03
- **Nome:** Emitir Certificado de Participação com Validação de Presença
- **Objetivo:** Permitir ao participante a emissão e o download do certificado digital de conclusão em formato PDF.
- **Ator Principal:** Participante
- **Atores Secundários:** Organizador (Validador de Presença)
- **Pré-condições:** 
  1. O evento foi marcado como "Concluído" no sistema.
  2. O participante possui inscrição no status `Confirmada`.

### 2. Fluxo Principal
1. O participante acessa a seção "Meus Certificados" no painel do participante.
2. O sistema lista os eventos concluídos nos quais o participante esteve inscrito.
3. O participante clica no botão "Emitir Certificado".
4. O sistema valida se a presença do participante foi registrada pela organização (Regra **RN06**).
5. O sistema verifica que a presença está confirmada (`presenca_confirmada == true`).
6. O sistema gera dinamicamente o arquivo PDF contendo: Nome do Participante, Nome do Evento, Carga Horária, Data de Realização e Código de Autenticação Digital (Hash SHA-256).
7. O sistema disponibiliza o download do arquivo PDF no navegador do participante.
8. O caso de uso é encerrado.

### 3. Fluxos Alternativos e de Exceção

#### FE01 - Presença Não Registrada no Evento
- **Desvio no Passo 5:** O participante esteve inscrito mas o organizador não confirmou sua presença.
- **Ações:**
  1. O sistema bloqueia a emissão do PDF.
  2. Exibe aviso: "Certificado indisponível: Presença não confirmada pela organização do evento. Caso considere um equívoco, entre em contato com o organizador.".
  3. O caso de uso é encerrado sem gerar o arquivo.

### 4. Pós-condições
- O certificado PDF é gerado e baixado pelo participante.
- A emissão do certificado é registrada no histórico de auditoria do participante.
