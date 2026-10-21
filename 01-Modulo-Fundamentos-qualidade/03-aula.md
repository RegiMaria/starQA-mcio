# Aula 03 - Construindo certo a coisa certa

*A mensagem central da aula é: "Construir certo não basta. Um software pode estar tecnicamente perfeito... e ainda assim ser a solução errada."*

O foco da aula foi ensinar como o QA atua na prevenção de bugs e na eliminação da ambiguidade logo no início do ciclo (no Refinamento), garantindo
que o time construa não apenas um código sem erros, mas um produto que realmente resolva o problema do usuário.

## Validação vs Verificação

```
                     ┌─────────────────────────────────────────────────────────┐
                     │            PRECISAMOS DAS DUAS (V&V)                    │
                     └────────────────────┬────────────────────────────────────┘
                                               │
                       ┌───────────────────────┴───────────────────────┐
                       ▼                                               ▼
         【 VERIFICAÇÃO 】                                【 VALIDAÇÃO 】
   "Estamos construindo a solução                   "A solução atende à necessidade
 de acordo com os requisitos?"                    real do usuário e do negócio?
                  │                                               │
Foco: Construir O PRODUTO CORRETAMENTE                 • Foco: Construir O PRODUTO CERTO
Olha para: Regras, códigos e especificações           • Olha para: Valor, problema do usuário e utilidade
```

---

## O Ciclo Contínuo de V&V nas Etapas do Produto

Verificação e Validação não são etapas isoladas no final, mas acontecem juntas ao longo de todo o desenvolvimento:

01. Necessidade: Estamos resolvendo o problema certo? (Validação)

02. Requisito: O requisito está claro e consistente? (Verificação)

03. Solução: O desenho da solução atende à necessidade? (Validação)

04. Software: Foi implementado corretamente conforme o código/especificação? (Verificação)

05. Uso Real: Entrega o valor esperado para o usuário? (Validação)

---

## O Perigo dos requisitos ambíguos

Um requisito aparentemente simples como "O sistema deve permitir desconto para bons clientes" é um prato cheio para gerar bugs em produção.
O papel do QA é fazer as perguntas certas no refinamento para desmembrar essa frase ambígua:

1.O que é um "bom cliente"?   
2.Qual o percentual do desconto?  
3.Existe limite máximo?   
4.Vale para todos os produtos?  
5.Pode acumular com outras promoções?  
6. Quem pode conceder o desconto?   
7.Quando começa e termina?   
9.O que acontece na devolução do produto?  

---

## O que constitui um BOM Requisito?
Para o QA, um bom requisito passa por um funil que reduz interpretações e deve ser:

- Claro: Duas pessoas leem e entendem exatamente a mesma coisa.

- Consistente: Não entra em contradição com outras regras existentes no sistema.

- Testável: É possível observar o comportamento e validar matematicamente/visualmente se funcionou ou falhou.

- Rastreável: Sabemos de onde veio a necessidade e qual problema de negócio ela resolve.


*"Quanto mais ambiguidade no início, maior o espaço para retrabalho depois."*

---

## O Papel do QA no Refinamento (Shift-Left)
Completo: Contém informação suficiente para construir e testar sem inventar regras.

Estudamos o Rfinamento como a mudandança de paradigma do QA moderno:  

Antes (QA isolado no final): Requisito chega pronto → Dev começa a codar → Dúvidas e bugs explodem durante a implementação ou nos testes finais → Retrabalho alto.   

Depois (QA no Refinamento): QA questiona regras, riscos, exceções, dependências e testabilidade antes da construção → Entendimento compartilhado → Menos surpresas, 
menos retrabalho e testes muito mais eficientes.


*Nesta aula aprendemos ue o QA atua ativamente desde o refinamento eliminando ambiguidades dos requisitos.
Garantimos a Verificação (se o software foi feito do jeito certo conforme a regra) e a Validação (se a solução
realmente resolve o problema do usuário no uso real).*



