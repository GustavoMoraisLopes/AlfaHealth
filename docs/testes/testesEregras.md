# Regras para concluir tarefas e testar funcionalidades

## Quando podemos considerar uma tarefa concluída

Esta proposta deve ser revista e aprovada pela equipa.

Uma tarefa pode ser marcada como concluída quando:

- O que foi combinado para a tarefa está feito.
- A documentação relacionada está atualizada, quando necessário.
- Os testes e as verificações que se aplicam foram feitos e passaram.
- As alterações foram enviadas num Pull Request para a branch `main`.
- O Pull Request recebeu duas aprovações e os comentários de revisão foram resolvidos.
- As verificações aplicáveis do GitHub Actions passaram.

Nas tarefas de documentação e diagramas, confirma-se que o resultado está de acordo com o enunciado e com os restantes documentos do projeto. As verificações de build e os testes da aplicação serão acrescentados quando existir código executável.

## Testes previstos para as funcionalidades

Os testes abaixo foram preparados a partir dos requisitos atuais do projeto. Ainda não foram executados, porque a aplicação não está implementada.

| ID | Requisito | Funcionalidade | O que fazer | Dados de teste | O que deve acontecer | Estado |
|---|---|---|---|---|---|---|
| T01 | RF02 | Consentimento parental | Iniciar o registo sem confirmar o consentimento e, depois, confirmar o consentimento. | Utilizador com 15 anos; consentimento primeiro pendente e depois confirmado. | A conta não fica ativa enquanto o consentimento estiver pendente. Depois da confirmação, pode ser ativada. | Por testar |
| T02 | RF05–RF07 | Percurso de aprendizagem | Responder ao diagnóstico, consultar os materiais e responder ao questionário final. | Utilizador registado; recurso com diagnóstico, materiais e questionário final. | O utilizador consegue seguir as etapas pela ordem prevista. | Por testar |
| T03 | RF05 | Tentativas de diagnóstico | Responder duas vezes ao diagnóstico e tentar uma terceira vez. | Tentativas 1, 2 e 3 para o mesmo utilizador e diagnóstico. | As duas primeiras tentativas são permitidas; a terceira é recusada. | Por testar |
| T04 | RF09 | Badge e certificado | Submeter o questionário final com 84% e depois com 85%. | Notas finais de 84% e 85%. | Com 84%, não são atribuídos badge nem certificado. Com 85%, são atribuídos. | Por testar |
| T05 | RF15 / RNF-U02 | Mudança de idioma | Selecionar português e depois inglês. | Recurso com tradução disponível em PT e EN. | Os conteúdos aparecem no idioma selecionado. | Por testar |
| T06 | RF14 | Exportação de resultados | Exportar respostas e notas em CSV. | Respostas e notas fictícias associadas a um utilizador com nome e email registados. | O CSV contém respostas e notas, mas não inclui o nome nem o email do utilizador. | Por testar |
| T07 | RF07 | Limite de tentativas do questionário final | Tentar submeter o questionário final duas vezes. | Utilizador registado; questionário final com `max_attempts = 1`. | A primeira submissão é aceite; a segunda é recusada. | Por testar |
| T08 | RF02 | Consentimento parental expirado | Deixar expirar o pedido de consentimento sem confirmação. | Utilizador com 15 anos; consentimento não confirmado até `expires_at`. | A conta e os dados pessoais são apagados. | Por testar |
| T09 | MRD v1.1, P5 | Revogação do consentimento | Revogar o consentimento de uma conta ativa e não dar novo consentimento durante 30 dias. | Conta ativa; data de revogação; sem novo consentimento durante 30 dias. | A conta fica bloqueada após a revogação; ao fim de 30 dias sem novo consentimento, a conta e os dados pessoais são apagados. | Por testar |
| T10 | RF08 | Resposta em branco | Submeter um questionário deixando uma pergunta sem resposta. | Uma pergunta sem resposta; `answer_id` vazio. | A resposta em branco é registada como errada. | Por testar |
| T11 | RF01 | Email por confirmar | Tentar autenticar uma conta cujo email ainda não foi confirmado. | Conta com `email_verified_at` vazio. | A autenticação é recusada. | Por testar |

Quando a equipa definir as User Stories das Sprints B e C, cada teste será associado à User Story correspondente. Os passos e resultados serão ajustados se os critérios dessas User Stories acrescentarem detalhes.
