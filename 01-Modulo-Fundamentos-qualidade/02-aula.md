<div align="center">
<img src="https://github.com/user-attachments/assets/1aaa5949-931c-4a97-a8e2-df8211927c52" width="220" alt="AWS Logo"/>

# Formação StartQA - MCIO Brasil

</div>


## Módulo 1: Do requisito à produção: QA no ciclo de desenvolvimento
### 02 - Aula 19/10/2026

---
Para esta aula fomos desafiadas a pensar sobre como o QA acompanha e deve estar presente em TODA
a jornada do ciclo de vida do software/produto.

Essa visão de que a Garantia da Qualidade (QA) atua do início ao fim e é conhecida no mercado moderno como Quality Assistance
(ou Shift-Left Testing + Shift-Right Observability).

Historicamente, o QA era visto apenas como a "última porta" (testar o software pronto no item 5/7).
Hoje, nas metodologias ágeis e nos modelos de maturidade como CMMI e ISO/IEC 12207, a qualidade é um processo contínuo, não uma fase final

---

## Exercício
<div align="center">
<img src="https://github.com/user-attachments/assets/3bfd3621-6963-4d39-b336-77a16280ee2a" width="600" alt="AWS Logo"/>
</div>

Nesse exercício, considerando as etapas abaixo como o QA atua em cada uma das etapas dessa jornada?

---

## Etapas


<div align="center">
<img src="https://github.com/user-attachments/assets/e9412352-8e7f-427b-90bc-fb6f7665561d"  width="600" alt="AWS Logo"/>
</div>

---

Neste cenário de troca de endereço de entrega de uma encomenda, o profissional de QA não pensa apenas em "testar a tela de formulário",
mas sim em **evitar fraudes, garantir a entrega no prazo correto e impedir inconsistências entre o sistema e a logística**.

**1. Planejamento (Questiona valor, risco e regras de negócio)**

- Verificações de Segurança/Fraude: A mudança de endereço pode ser feita a qualquer momento?
Existe risco de sequestro de conta ou fraude de redirecionamento de entrega?

- Verificações Logísticas: Qual é o limite de tempo/status do pedido para permitir a alteração?
(Ex: Se o pedido já saiu para entrega ou já teve a Nota Fiscal emitida, o sistema bloqueia?)

- Verificações Financeiras: Se o novo CEP gerar um frete mais caro ou mais barato,
como será tratada a cobrança/estorno da diferença?

**2. Requisitos e Critérios de Aceite (Remove ambiguidade)**

- Validação de CEP/Endereço: O sistema vai validar o CEP automaticamente via API (ex: ViaCEP)?

- Campos Obrigatórios: Quais campos são estritamente obrigatórios (Ex: Número, Bairro, CEP, Cidade, Estado)?
O que acontece se o cliente mora em "Área sem número" ou "Zona Rural"?

- Limitações Regionais: O novo endereço pode estar fora da área de cobertura da transportadora contratada?

- Mensagens de Erro/Sucesso: O critério de aceite especifica claramente o que é exibido ao usuário caso a alteração seja aceita ou recusada?

**3. Análise, Design e Arquitetura (Avalia fluxos e exceções)**

- Comunicação entre Microsserviços/APIs: A alteração do endereço no painel do cliente atualiza instantaneamente o serviço do WMS (Armazém/Estoque) e da Transportadora?

- Tratamento de Exceção: O que acontece se a API da transportadora estiver indisponível no momento em que o cliente salvar o novo endereço?

- Concorrência: Se o cliente alterar o endereço exatamente no mesmo segundo em que o operador do armazém está gerando a etiqueta de envio, qual informação prevalece?

> Olhar para a REGRAS DE NEGÓCIOS

**4. Desenvolvimento (Colabora e antecipa)**

- Testes Unitários: Os testes unitários do backend cobrem o cálculo do novo valor de frete e a alteração de status do pedido?

- Máscaras e Sanitização de Entrada: O código previne caracteres especiais inválidos no campo de logradouro/complemento
que possam quebrar a impressão da etiqueta na impressora térmica do armazém?

- Tratamento de Strings/Tipos: O campo número aceita letras (ex: "100-A")? O CEP trata corretamente o zero à esquerda?

**5. Testes e QA (Protege a entrega)**

- Análise de Valor Limite e Borda (Boundary Testing):

- Tentar alterar o endereço no exato status limite (ex: de "Em Separação" para "Enviado").

- Tentar inserir logradouros com limites mínimos e máximos de caracteres (ex: 2 caracteres vs. 250 caracteres).

- Testes de Integração e Regressão:

- Alterar o endereço e verificar se a Nota Fiscal gerada posteriormente traz o novo endereço ou o antigo.

- Verificar se o e-mail/WhatsApp de confirmação enviado ao cliente reflete o novo endereço.

- Testes de Segurança (Security Testing):

- Tentar alterar o endereço de entrega de um pedido de outro usuário alterando o ID da requisição na API (Vulnerabilidade IDOR).

**6. Deploy e Entrega (Validação do ambiente)**

- Smoke Test em Staging/Production: Executar uma simulação end-to-end de troca de endereço no ambiente de homologação e produção antes da liberação geral.

- Feature Flag/Toggle: A funcionalidade de alteração de endereço pode ser desativada rapidamente via painel se identificarmos um bug crítico após o deploy?

**7. Operações, Manutenção e Feedback (Aprende com dados)**

- Métricas e Logs: O sistema registra logs auditáveis de quem alterou o endereço e quando (Cliente, Atendente do SAC ou Sistema)?

- Observabilidade: Existe alerta configurado se a taxa de falha na API de validação de CEP ou integração com a transportadora subir repentinamente?

- Feedback do SAC: Quantos chamados foram abertos no suporte por erro de entrega após o cliente ter "alterado o endereço" no app? (Alimentar o backlog para melhoria contínua do processo).




## O desafio da aula

<div align="center">
<img src="https://github.com/user-attachments/assets/fc68346a-62fa-4e7a-a6a9-e138419e86e5" width="600" alt="AWS Logo"/>
</div>

## Resolução


Para resolver esse desafio nos olhamos para o ciclo de vida do software
<div align="center">
<img src="https://github.com/user-attachments/assets/09cce6bf-59cc-437f-9615-de14360465ee"  width="600" alt="AWS Logo"/>
</div>

**1. "Quem realmente precisa dessa funcionalidade?"**

Etapa: 1. Planejamento / Descoberta (Discovery)

Por quê: Esta pergunta avalia o **propósito do produto e valor de negócio**.
Ela **evita o desperdício de tempo e recursos** desenvolvendo algo que não atende
às reais necessidades do usuário ou da empresa.

**2. "E se o CEP não existir?"**

Etapas: 2. Requisitos / Refinamento (3Refinement/Grooming) e 4. Desenvolvimento (Dev)

Por quê: É a busca por cenários de exceção e fluxos alternativos antes da escrita do código.
Fazer essa pergunta no refinamento remove a ambiguidade nos critérios de aceite; durante o dev, 
garante que o código trate o erro (trata o erro de API/404) em vez de quebrar a aplicação.

**3. "Como saberemos que todos os sistemas atualizaram?"**

Etapa: 3. Análise, Design e Arquitetura / Testes de Integração

Por quê: Questiona a interoperabilidade e sincronismo da arquitetura. 
Em um sistema com microsserviços (ex: site, armazém e transportadora), 
essa pergunta garante que haja rastreabilidade e confirmação (acknowledgement)
entre as pontas.


**4. "Qual mensagem aparece se falhar?"**

Etapas: 2. Requisitos / Critérios de Aceite e 3. UX/UI Design

Por quê: Foco na Usabilidade e Experiência do Usuário (UX). 
A pergunta evita que o usuário final veja telas com erros genéricos ("Erro 500" ou NullPointer) 
e garante que receba uma mensagem clara e instrucional caso a operação falhe.

**5. "Como voltamos atrás se o deploy der problema?"**

Etapa: 5. Deploy / Preparação para Release (DevOps & QA)

Por quê: Foco no Plano de Rollback e Gestão de Risco. Antes de colocar qualquer alteração em produção,
a equipe precisa garantir estratégias de reversão segura (como o uso de Feature Flags/Toggles ou rollback
de versão sem perda de dados).


**6. "Como saberemos em produção se aumentaram os erros?"**

Etapa: 6. Operações, Manutenção e Observabilidade (Produção)

Por quê: Foco em Observabilidade (Shift-Right). Questiona quais métricas, 
dashboards (Grafana/Datadog) e alertas serão configurados para monitorar 
a saúde da aplicação em tempo real e identificar anomalias antes que os 
clientes comecem a reclamar.

> Resumo do desafio:
> *"Cada pergunta representa o papel ativo do QA atuando como guardião da qualidade em toda a jornada
> do produto: do Entendimento do Valor (Planejamento), passando pela Prevenção de Bugs (Requisitos/Arquitetura),
> até a Segurança da Entrega (Deploy) e a Observabilidade (Produção)."*

---



## Desafio aula 19-10

## O desafio

<div align="center">
<img src="https://github.com/user-attachments/assets/8b72f813-eb8f-40d7-b678-c52a7d3023ba" width="600" alt="AWS Logo"/>
</div>

## Resolução

Para a funcionalidade de aumento de limite de cartão de crédito no app bancário, as validações
e perguntas essenciais em cada etapa são:

**1. Descoberta (O que perguntar?)**

**Análise de Risco e Negócio:**

- O aumento é instantâneo (pré-aprovado) ou passa por uma análise de crédito em tempo real/assíncrona?

- Há um valor limite máximo diário/mensal que o cliente pode solicitar pelo app?

- Qual é o público-alvo (todos os clientes, apenas conta corrente, apenas clientes sem inadimplência)?

- Se a análise for recusada, o app exibirá o motivo exato ou uma mensagem genérica?

- Como a funcionalidade se comporta para cartões adicionais (dependente vs. titular)?

**2. Requisitos (Quais regras precisam estar claras?)**

**Critérios de Aceite e Regras de Borda:**

- Regras de Intervalo: Qual o valor mínimo e máximo configurável na barra/campo de limite?

 Regra de Elegibilidade: O cliente precisa ter tempo mínimo de conta ou estar sem faturas em atraso?

- Validação de Segurança: O aumento exige confirmação por biometria facial, senha do cartão ou token/OTP?

- Ajuste Provisório vs. Permanente: O cliente pode solicitar um aumento temporário (ex: para uma viagem) ou todo aumento é definitivo?

- Notificação e Comprovante: O cliente deve receber e-mail, SMS ou push notification confirmando a alteração com o novo comprovante em PDF/tela?


**3. Design / Dev (Quais riscos antecipar?)**

**Fraude e Segurança (Security/IDOR):**

- Risco de um atacante manipular a requisição da API e solicitar um limite maior do que o pré-aprovado (Parameter Tampering).

- Risco de sequestro de conta (Account Takeover) para aumento de limite imediato seguido de fraude.

**Integridade e Concorrência:**

- Se o cliente fizer duas solicitações simultâneas (duplo clique no app ou requisições paralelas), o backend processará ambas? (Injeção de regra de Idempotência).

**Interoperabilidade e Resiliência:**

 O que acontece se o microsserviço de Análise de Crédito ou o Core Bancário estiver fora 
 do ar no momento do clique? O app deve lidar com graceful degradation (tratamento amigável do erro sem travar o app).

**4. Testes (Que cenários validar?)**

**Análise de Valor Limite (Boundary Testing / BVA):**

- Tentar solicitar R$ 0,00, R$ 0,01 a mais que o limite atual, exatamente o valor pré-aprovado máximo e R$ 0,01 acima do valor pré-aprovado.

**Cenários de Exceção e Fluxos Alternativos:**

- Cliente elegível com conta bloqueada ou fatura atrasada.

- Solicitante sendo cartão adicional tentando alterar limite do titular.

- Perda de conexão de internet durante o processamento do envio do formulário.

**Testes de Segurança e Integração:**

- Tentar alterar o ID da conta na chamada da API para aumentar o limite de outro usuário (vulnerabilidade IDOR).

- Teste end-to-end: alterar o limite pelo app e realizar uma compra imediatamente no cartão (físico ou virtual)
para validar se o novo limite já foi sincronizado com a adquirente/processadora.

**5. Deploy (O que precisa estar pronto?)**

**Controle e Reversibilidade:**

- Feature Flag / Toggle: A funcionalidade deve estar protegida por uma chave de configuração para poder ser ativada/desativada instantaneamente sem precisar subir nova versão do app.

- Rollback Plan: Estratégia clara de rollback caso o microsserviço no backend apresente inconsistências.

**Validação de Ambiente:**

- Execução de Smoke Tests em staging e produção controlada (Canary Release / Liberação gradativa para 5%, 10%, 50% dos usuários).

- Scripts de migração de banco de dados e sincronização de contratos de API finalizados e homologados.

**6. Produção (O que monitorar / Observabilidade?)**

**Métricas de Negócio e Suporte:**

- Taxa de sucesso vs. erro nas solicitações de aumento de limite.

- Volume de chamados abertos no SAC/Chat relacionados a "Aumento de limite recusado" ou "Limite não atualizado".

**Métricas Técnicas e Alertas:**

- Latência/tempo de resposta da API de Análise de Crédito e do Core Bancário.

- Taxa de erros HTTP 5xx (falha interna do servidor) e 4xx (falha do cliente ou validação) na rota de ajuste de limite.

- Logs auditáveis para fins regulatórios (registrando quem alterou, qual era o limite anterior, o novo limite, IP e timestamp).
