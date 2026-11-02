# Regras de Contribuição — ALFAS

## 1. Branch principal
A branch `main` contém a versão principal do projeto. Não devem ser feitas alterações diretamente nesta branch.

## 2. Criação de branches
Cada elemento deve criar uma branch para a tarefa que vai desenvolver.

Convenção de nomes:
- `feature/descricao` — novas funcionalidades
- `fix/descricao` — correção de erros
- `docs/descricao` — documentação
- `ci/descricao` — configuração de integração contínua

Exemplos:
- `docs/requisitos`
- `feature/autenticacao`
- `ci/github-actions`

## 3. Pull Requests
Quando uma tarefa estiver concluída:
1. Enviar as alterações para o GitHub.
2. Criar um Pull Request para a branch `main`.
3. Explicar resumidamente as alterações realizadas.
4. Pedir a revisão de, pelo menos, outro elemento da equipa.
5. Integrar as alterações depois da aprovação.

## 4. Boas práticas
- Utilizar mensagens de commit claras e descritivas.
- Evitar incluir ficheiros temporários ou credenciais.
- Manter a documentação atualizada.
- Resolver conflitos antes de integrar um Pull Request.
