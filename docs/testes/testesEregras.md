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

| ID | Funcionalidade | O que fazer | O que deve acontecer | Estado |
|---|---|---|---|---|
| T01 | Consentimento parental | Iniciar o registo de um menor sem confirmar o consentimento parental. Depois, confirmar o consentimento. | A conta não fica ativa antes da confirmação. Depois de o consentimento ser confirmado, a conta pode ser ativada. | Por testar |
| T02 | Percurso de aprendizagem | Responder ao questionário de diagnóstico, consultar os materiais e responder ao questionário final. | O utilizador consegue seguir as etapas pela ordem prevista. | Por testar |
| T03 | Segunda tentativa de diagnóstico | Responder uma vez ao questionário de diagnóstico e tentar responder novamente. | O sistema permite uma segunda tentativa de diagnóstico. | Por testar |
| T04 | Badge e certificado | Submeter o questionário final com uma nota de 85% ou superior e repetir o teste com uma nota inferior a 85%. | Com 85% ou mais, são atribuídos o badge e o certificado. Abaixo de 85%, não são atribuídos. | Por testar |
| T05 | Mudança de idioma | Selecionar português e depois inglês. | Os conteúdos disponíveis são apresentados no idioma selecionado. | Por testar |
| T06 | Exportação de resultados | Pedir a exportação das respostas e notas em CSV. | É gerado um ficheiro CSV com as respostas e notas registadas. | Por testar |

Quando a equipa definir as User Stories das Sprints B e C, cada teste será associado à User Story correspondente. Os passos e resultados serão ajustados se os critérios dessas User Stories acrescentarem detalhes.
