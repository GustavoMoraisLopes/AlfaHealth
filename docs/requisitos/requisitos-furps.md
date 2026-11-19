# Levantamento de Requisitos — ALFAS

## 1. Introdução

O presente documento identifica e organiza os requisitos funcionais e não funcionais da plataforma ALFAS — Plataforma de Literacia em Saúde para Jovens.

O levantamento é realizado segundo o método FURPS+, permitindo organizar os requisitos de acordo com a sua natureza e características de qualidade.

Este documento serve de referência para a análise, conceção, desenvolvimento e validação do sistema ao longo do projeto.

## 2. Âmbito do Sistema

A plataforma ALFAS é uma aplicação web de literacia em saúde destinada a alunos do 3.º ciclo e do ensino secundário, utilizada também por professores e profissionais de saúde. A plataforma disponibiliza webinars e workshops e apoia um percurso de aprendizagem com questionários de diagnóstico e avaliação final, materiais educativos e apresentação de resultados. Inclui ainda gestão de conteúdos e utilizadores, consulta de recursos de saúde, emissão de badges e certificados e análise estatística dos dados registados.

## 3. Requisitos segundo FURPS+

### 3.1. Functionality (Funcionalidade)

- RF01 — O sistema deve permitir o registo e a autenticação de utilizadores.
- RF02 — O sistema deve permitir o pedido e o registo do consentimento parental antes da ativação da conta de um menor.
- RF03 — O sistema deve permitir consultar webinars, workshops e outros recursos educativos.
- RF04 — O sistema deve permitir a inscrição de utilizadores nos recursos.
- RF05 — O sistema deve disponibilizar um questionário de diagnóstico associado a um recurso, com possibilidade de uma segunda tentativa.
- RF06 — O sistema deve disponibilizar os materiais do recurso após o diagnóstico.
- RF07 — O sistema deve disponibilizar o questionário final associado ao recurso.
- RF08 — O sistema deve registar as tentativas, respostas e notas dos questionários.
- RF09 — O sistema deve atribuir o badge e emitir um certificado quando a nota do questionário final for igual ou superior a 85%.
- RF10 — O sistema deve permitir consultar no perfil as notas, a comparação entre os resultados pré e pós, os badges e os certificados.
- RF11 — O sistema deve disponibilizar biblioteca virtual, notícias e agenda.
- RF12 — O sistema deve permitir gerir conteúdos e utilizadores através do backoffice.
- RF13 — O sistema deve apresentar estatísticas de utilização e aprendizagem a Manager/Admin.
- RF14 — O sistema deve permitir exportar respostas e notas em formato CSV.
- RF15 — O sistema deve disponibilizar os conteúdos em português e inglês.
- RF16 — O sistema deve permitir que o utilizador adicione e remova recursos dos seus favoritos.
- RF17 — O sistema deve apresentar os destaques da semana definidos pelo Manager.
- RF18 — O sistema deve permitir ao encarregado de educação revogar o consentimento através do link recebido por email e ao Administrador revogá-lo no backoffice. Após a revogação, a conta fica bloqueada; se não houver novo consentimento em 30 dias, a conta e os dados pessoais são apagados.
- RF19 — O sistema deve permitir ao utilizador eliminar a própria conta e os dados pessoais associados.

### 3.2. Usability (Usabilidade)

- RNF-U01 — A interface deve ser clara e responsiva, permitindo a utilização em diferentes tamanhos de ecrã.
- RNF-U02 — A interface deve apresentar os conteúdos em português ou inglês, de acordo com o idioma selecionado pelo utilizador.
- RNF-U03 — Quando ocorre um erro, o sistema deve apresentar uma mensagem útil para orientar o utilizador.

### 3.3. Reliability (Fiabilidade)

- RNF-R01 — Se a sessão expirar ou o utilizador abandonar o questionário antes de o submeter, a tentativa não deve ter nota nem contar para as estatísticas.
- RNF-R02 — Se ocorrer um erro ao guardar uma submissão, o sistema não deve guardar uma tentativa parcial; deve manter as respostas no ecrã e permitir nova submissão.
- RNF-R03 — Depois da submissão, alterações posteriores às respostas corretas do questionário não devem modificar as respostas nem a nota já registadas.

### 3.4. Performance (Desempenho)

- Qual é o tempo de resposta aceitável para as operações principais da plataforma?
- Quantos utilizadores simultâneos a plataforma deverá suportar?
- Existem limites esperados para o volume ou o tempo de geração das exportações CSV?

### 3.5. Supportability (Suportabilidade)

- Que requisitos existem para facilitar a manutenção e atualização do sistema?
- É necessário manter registos de erros para apoiar o diagnóstico de problemas?
- Quem será responsável por gerir utilizadores e conteúdos após a entrada em funcionamento?

### 3.6. Plus (+) — Restrições e requisitos adicionais

- R+01 — O frontend deve ser desenvolvido em React.
- R+02 — O backend deve ser desenvolvido em Python com Flask.
- R+03 — A arquitetura prevista para o sistema é MVC.
- R+04 — A base de dados prevista é MySQL ou SQL Server; a escolha final está por confirmar.
- R+05 — As palavras-passe devem ser armazenadas de forma segura.
- R+06 — O tratamento de dados deve considerar o RGPD, com atenção especial aos dados de menores.

## 4. Rastreabilidade dos Requisitos

| ID | Fonte / justificação |
|---|---|
| RF01–RF02 | Enunciado do projeto: registo, autenticação e consentimento parental |
| RF03–RF07 | Enunciado do projeto: webinars/workshops e percurso de aprendizagem pré → materiais → pós |
| RF08 | Modelo Relacional v1.1: `quiz_attempts` e `attempt_answers` |
| RF09 | Enunciado do projeto: atribuição de badge e certificado com nota final ≥ 85% |
| RF10 | Enunciado do projeto: informação disponível no perfil do utilizador |
| RF11–RF12 | Enunciado do projeto: biblioteca, notícias, agenda e gestão no backoffice |
| RF13–RF14 | Enunciado do projeto: estatísticas para Manager/Admin e exportação CSV |
| RF15 / RNF-U02 | Enunciado do projeto e Modelo Relacional v1.1: suporte PT/EN |
| RF16 | MRD v1.1 (`favorites`) e caso de uso Frontoffice: marcar recurso como favorito |
| RF17 | MRD v1.1, P7, e casos de uso: gerir e consultar destaques da semana |
| RF18 | MRD v1.1, P5, mapa RGPD da A016 e casos de uso de consentimento parental |
| RF19 | Caso de uso Frontoffice: eliminar a própria conta; mapa RGPD da A016 |
| RNF-U01 / RNF-U03 | Enunciado do projeto: interface clara e responsiva; feedback útil de erros |
| RNF-R01–RNF-R03 | UC-F09: fluxos alternativos A7 e A10 e regra de negócio 3 |
| R+01–R+06 | Enunciado/contexto do projeto: tecnologias, arquitetura, segurança e RGPD |

## 5. Observações e Questões em Aberto

- A equipa vai escolher MySQL ou SQL Server?
- Que permissões terá cada perfil de utilizador?
- Qual é a disponibilidade esperada e quanto tempo podem demorar as operações?
- Quantos utilizadores simultâneos a plataforma deve suportar?
- Se ocorrer um erro durante um questionário, como devem ser tratadas as respostas ainda não submetidas?
- Que medidas de manutenção e registo de erros serão necessárias?
- Durante quanto tempo serão guardados os dados pessoais e quem poderá aceder-lhes?
- O que deve acontecer quando uma tradução ainda não estiver disponível?
