# Histórias de Usuário (User Stories - US)

> **Projeto:** Sistema de Gestão de Eventos (Eventus)  
> **Formato Padrão:** Como `<papel>`, quero `<ação>`, para `<benefício>`.  
> **Convenção de ID:** US01, US02, US03...

---

## Módulo do Participante

### US01 - Visualização do Catálogo de Eventos
- **História:** Como **Participante**, quero visualizar a lista de todos os eventos e workshops disponíveis com filtros por data e status de vaga, para que eu possa escolher e me planejar para as atividades de meu interesse.
- **Requisitos Relacionados:** RF01

### US02 - Realização de Inscrição em Eventos
- **História:** Como **Participante**, quero me inscrever em um ou mais eventos/workshops selecionados preenchendo meus dados básicos, para que eu garanta minha vaga na atividade desejada.
- **Requisitos Relacionados:** RF02, RF06, RN01, RN03

### US03 - Recebimento de Comprovante de Inscrição
- **História:** Como **Participante**, quero receber um comprovante digital de inscrição imediatamente após a conclusão do pedido, para que eu tenha uma confirmação formal e segura da minha participação.
- **Requisitos Relacionados:** RF03

### US04 - Autosserviço de Cancelamento de Inscrição
- **História:** Como **Participante**, quero poder cancelar minha inscrição diretamente pelo sistema quando não puder comparecer, para que a vaga seja liberada a outros interessados sem precisar ligar para a organização.
- **Requisitos Relacionados:** RF04, RN04

### US05 - Emissão de Certificado de Participação
- **História:** Como **Participante**, quero emitir e baixar meu certificado digital em PDF após a realização do evento, para que eu possa comprovar minha participação e carga horária acadêmica/profissional.
- **Requisitos Relacionados:** RF05, RN06

### US06 - Entrada Automática em Lista de Espera
- **História:** Como **Participante**, quero ser incluído em uma lista de espera caso o evento de meu interesse esteja esgotado, para que eu possa ter a chance de ser convocado se houver alguma desistência.
- **Requisitos Relacionados:** RF09, RN05

---

## Módulo do Organizador

### US07 - Gestão de Eventos e Controle de Vagas
- **História:** Como **Organizador**, quero cadastrar e configurar os detalhes do evento (data, horário, limite de vagas, valor e permissão de cancelamento), para que o sistema gerencie as inscrições conforme as regras estipuladas.
- **Requisitos Relacionados:** RF07, RF08, RN01, RN04

### US08 - Acompanhamento do Painel de Inscrições em Tempo Real
- **História:** Como **Organizador**, quero visualizar um dashboard com o total de inscritos, vagas restantes e lista de espera em tempo real, para que eu possa acompanhar o engajamento e a ocupação dos eventos.
- **Requisitos Relacionados:** RF10

---

## Módulo Financeiro

### US09 - Confirmação de Pagamento e Liberação de Inscrição
- **História:** Como **Membro da Equipe Financeira**, quero consultar e confirmar o pagamento das inscrições pendentes em eventos pagos, para que a vaga do participante seja efetivamente liberada no sistema.
- **Requisitos Relacionados:** RF12, RF13, RN02

### US10 - Gestão de Reembolsos de Cancelamento
- **História:** Como **Membro da Equipe Financeira**, quero visualizar as solicitações de cancelamento elegíveis a reembolso e registrar o estorno do pagamento, para manter o controle financeiro correto e transparente.
- **Requisitos Relacionados:** RF14, RN07

---

## Módulo do Palestrante

### US11 - Consulta da Agenda e Lista de Participantes pelo Palestrante
- **História:** Como **Palestrante**, quero acessar a lista de participantes inscritos nas minhas palestras/workshops, para que eu possa adequar o conteúdo e dinâmica da apresentação ao perfil do público.
- **Requisitos Relacionados:** RF15
