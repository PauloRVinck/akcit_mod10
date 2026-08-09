# Requisitos Não Funcionais (RNF) - Proposta Candidata

> **Projeto:** Sistema de Gestão de Eventos (Eventus)  
> **Status:** CANDIDATOS A VALIDAÇÃO COM STAKEHOLDERS

---

> [!IMPORTANT]
> **NOTA DE ANÁLISE:**  
> O documento de elicitação inicial **não apresentou requisitos não funcionais explícitos**, conforme ressaltado no ponto 4 das observações ("*Não foram levantados requisitos relacionados a segurança, desempenho, disponibilidade, acessibilidade e privacidade dos dados*").  
>  
> Como boa prática de Engenharia de Requisitos, a equipe de análise elaborou a lista **proposta** abaixo com requisitos candidatos essenciais para garantir a qualidade, segurança e viabilidade do sistema. **Estes requisitos DEVEM ser revisados e homologados formalmente junto à Equipe de TI, Organizadores e Jurídico antes da linha de base de desenvolvimento.**

---

## Tabela de Requisitos Não Funcionais Candidatos

| ID | Categoria | Descrição do Requisito Candidato | Métrica / Critério de Aceite (Verificável) | Prioridade Proposta |
| :--- | :--- | :--- | :--- | :--- |
| **RNF01** | **Segurança** | O sistema deve utilizar protocolo de comunicação cifrado HTTPS/TLS 1.3 em todas as requisições e armazenar senhas de usuários com hash seguro (ex.: Argon2id ou bcrypt). | Auditoria de segurança e verificação de certificados TLS e hashes no banco de dados. | Alta |
| **RNF02** | **Segurança / Autenticação** | O sistema deve implementar controle de acesso baseado em papéis (RBAC - Role-Based Access Control) garantindo que Participantes, Organizadores, Financeiro e Palestrantes acessem apenas suas respetivas visões e recursos. | Testes de penetração (pentest) e testes de permissão de endpoints por perfil. | Alta |
| **RNF03** | **Privacidade / LGPD** | O sistema deve estar em conformidade com a Lei Geral de Proteção de Dados (LGPD - Lei nº 13.709/2018), coletando consentimento explícito do participante e permitindo a gestão de preferências e solicitação de exclusão/anonimização de dados pessoais. | Verificação da presença de termo de consentimento e funcionalidade de opt-out/exclusão de conta. | Alta |
| **RNF04** | **Desempenho** | O sistema deve responder a 95% das requisições de consulta de eventos e confirmação de inscrição em um tempo inferior a 2,0 segundos sob carga normal (até 500 usuários simultâneos). | Teste de carga e estresse automatizado (ex.: k6 / JMeter). | Média |
| **RNF05** | **Disponibilidade** | O sistema deve apresentar disponibilidade mínima de 99,5% (uptime) em regime de 24/7, com janelas de manutenção programadas previamente fora de horários de pico de inscrições. | Monitoramento contínuo de uptime via APM / Health Check. | Alta |
| **RNF06** | **Acessibilidade** | A interface web do participante deve estar em conformidade com as diretrizes WCAG 2.1 nível AA (Web Content Accessibility Guidelines), suportando leitores de tela e navegação via teclado. | Validação via ferramentas automatizadas (Lighthouse / AXE) e testes com leitores de tela. | Média |
| **RNF07** | **Escalabilidade** | A arquitetura da aplicação deve suportar picos de tráfego de inscrições de até 3.000 requisições por minuto durante a abertura de inscrições de eventos de grande porte, utilizando containerização (Docker) e auto-scaling. | Teste de estresse com aumento progressivo de carga até o limite de pico. | Alta |
| **RNF08** | **Usabilidade / Responsividade** | A interface de usuário (UI) do participante deve ser responsiva, adaptando-se a dispositivos móveis (smartphones), tablets e desktops com resolução mínima de 360px de largura. | Teste em múltiplos navegadores e tamanhos de tela (Viewports). | Alta |

---

## Ações Necessárias para Homologação
1. **Validar com a TI:** Confirmar a infraestrutura necessária para suportar RNF04, RNF05 e RNF07 (ex.: uso de infraestrutura em nuvem containerizada via Docker).
2. **Validar com o Jurídico/DPO:** Confirmar os termos de consentimento e política de retenção de dados pessoais exigidos pela LGPD (RNF03).
3. **Validar com a Equipe Financeira:** Verificar normas de segurança PCI-DSS para o processamento e retenção de dados de pagamento (RNF01 / RNF02).
