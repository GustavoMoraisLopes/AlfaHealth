# Métricas de aprendizagem — A009

## Base de cálculo

O MRD liga cada questionário a um recurso e distingue os tipos Diagnóstico e Final. Assim, a comparação é feita por utilizador e recurso, usando a nota do diagnóstico e a nota final correspondentes. As notas (`quiz_attempts.grade`) estão na escala de 0 a 100.

No diagnóstico, usa-se a primeira tentativa (`attempt_number = 1`): a segunda já pode refletir aprendizagem e não serve como ponto de partida. O questionário final permite uma tentativa (`quizzes.max_attempts = 1`). Só entram nos cálculos as tentativas submetidas, com `submitted_at` e `grade` preenchidos. Para calcular o ganho, têm de existir as duas notas do mesmo utilizador e recurso; sem esse par, o ganho fica por calcular.

As métricas são calculadas a partir dos registos da base de dados. Não se devem fixar resultados estatísticos no código.

## Métricas e origem dos dados

| Métrica | Cálculo / interpretação | Dados do MRD |
|---|---|---|
| Nota do diagnóstico | `grade` da tentativa `attempt_number = 1` do questionário do tipo Diagnóstico, se tiver sido submetida. | `quiz_attempts.grade`, `attempt_number`, `submitted_at`, `user_id`, `quiz_id`; `quizzes.quiztype_id`; `quiztypes.type`. |
| Nota final | `grade` da tentativa submetida do questionário do tipo Final do mesmo recurso. | `quiz_attempts.grade`, `submitted_at`, `user_id`, `quiz_id`; `quizzes.quiztype_id`, `resource_id`; `quiztypes.type`. |
| Ganho absoluto | `pós − pré`, em pontos percentuais. Pode ser negativo se a nota final for inferior à inicial. | Notas de `quiz_attempts`, ligadas ao mesmo `user_id` e ao mesmo `resources.id` através de `quizzes.resource_id`. |
| Ganho normalizado | `g = (pós − pré) / (100 − pré)`. Como o máximo da escala é 100, corresponde à fórmula geral `(pós − pré) / (máximo − pré)`. | As mesmas notas usadas no ganho absoluto. |
| Distribuição das notas | Média, mediana, desvio-padrão, mínimo e máximo, calculados separadamente para notas de diagnóstico e finais submetidas. | `quiz_attempts.grade`; agrupamentos via questionário e recurso. |
| Resultados por recurso | Distribuição das notas e ganhos para cada recurso. | `quizzes.resource_id` → `resources.id`. |
| Resultados por área de saúde | Distribuição das notas e ganhos dos recursos de cada área. | `resources.healtharea_id` → `healthareas.id`. |
| Resultados por género | Distribuição das notas e ganhos por género. | `users.gender_id` → `genders.id`. |
| Resultados por ano escolar | Distribuição das notas e ganhos por ano escolar. | `quiz_attempts.user_id` → `users.schoolyear_id` → `schoolyears.id`. |
| Percentagem de respostas certas por pergunta | `n.º de respostas certas / n.º de respostas registadas para a pergunta × 100`. A nota P1 determina que uma pergunta em branco conta como errada. | `attempt_answers.is_correct`, `quiz_attempt_id`, `question_id`; `quiz_attempts` identifica questionário, utilizador e tentativa. |
| Comparação entre grupos | Comparar notas ou ganhos entre grupos, mostrando estimativa, intervalo de confiança e teste estatístico escolhido. | Notas/ganhos, `quiz_attempts.submitted_at` e atributos de grupo, como `genders.gender`, `schoolyears.schoolyear`, recurso e área de saúde. |
| Amostras pequenas | Usar reamostragem ou simulação para estimar a incerteza quando a amostra for pequena; apresentar o tamanho da amostra junto dos resultados. Não apresentar estatísticas de grupos com menos de 10 participantes. | Os mesmos registos elegíveis para a métrica analisada. |

## Regras de cálculo e interpretação

### Tentativas e notas

Uma tentativa abandonada continua no modelo, mas não representa um resultado. Por isso, as estatísticas usam apenas registos com `submitted_at` e `grade` preenchidos. No diagnóstico seleciona-se `attempt_number = 1`, desde que tenha sido submetida; não se substitui por uma segunda tentativa se a primeira foi abandonada. No final, considera-se a tentativa submetida do questionário Final.

### Ganho normalizado

O ganho normalizado usa `g = (pós − pré) / (100 − pré)`, conforme a escala definida no MRD. Se a nota pré for 100, o denominador é zero e o resultado deve ser **não calculável (N/A)**. Não se substitui por zero. Também não há ganho quando falta uma das notas do par.

### Análise das perguntas

Em `attempt_answers` há uma linha por pergunta em cada tentativa (`UNIQUE(quiz_attempt_id, question_id)`). O campo `is_correct` guarda o resultado no momento da submissão; assim, uma correção posterior em `answers.correct` não altera o histórico. Se `answer_id` for `NULL`, a pergunta ficou em branco e conta como errada. Por isso, a percentagem de acerto inclui as respostas em branco no denominador.

A percentagem de acertos por pergunta é o resultado pedido na A009. Para este cálculo, considerar apenas as tentativas submetidas, para não misturar respostas parciais de tentativas abandonadas. Classificar perguntas como fáceis ou difíceis é um extra: se a equipa o incluir, pode usar como referência fácil acima de 80% e difícil abaixo de 30%. A discriminação fica como trabalho futuro; medidas possíveis são comparar os 27% com melhores notas aos 27% com piores notas, ou calcular a correlação ponto-bisserial. Estes indicadores não fazem parte da A009.

### Comparações e amostras

No relatório da A009 basta indicar a abordagem; a implementação calculará os testes e intervalos. Para pré/pós da mesma pessoa, usar teste t emparelhado ou Wilcoxon se os dados não forem normais. Entre dois grupos, usar teste t de Welch ou Mann–Whitney; para mais de dois, ANOVA ou Kruskal–Wallis. Reportar intervalos de confiança de 95%.

Considerar pequena uma amostra com `n < 30`. Nesses casos, usar bootstrap com cerca de 1000 reamostragens e intervalo por percentis, ou um teste não paramétrico. Para reduzir o risco de identificar alunos, não apresentar estatísticas de um grupo quando este tiver menos de 10 participantes. O limite aplica-se também a cada combinação de filtros, como género e ano escolar; nesses casos, indicar “amostra insuficiente” sem revelar o número de participantes nem resultados que permitam deduzi-lo.

## Apresentação e acesso

- **Perfil do utilizador:** nota de cada questionário, comparação pré/pós e badge/certificado quando as regras do projeto forem cumpridas.
- **Backoffice:** indicadores agregados por recurso, área de saúde, género, ano escolar e período, incluindo distribuição das notas e evolução temporal em gráficos.
- **CSV:** incluir recurso, tipo de questionário, número da tentativa, nota, respostas por pergunta, género e ano escolar. Não incluir nome nem email. A exportação é permitida a Manager e Admin.
- **Filtros:** permitir selecionar um intervalo de datas pela data de submissão da tentativa (`quiz_attempts.submitted_at`), além dos filtros de recurso, área, género e ano escolar.
- As métricas são recalculadas a partir dos dados guardados; o MRD não prevê armazenar agregados estatísticos como valores fixos.

A A009 reporta as notas e a elegibilidade para badge/certificado; não redefine a regra de emissão, já descrita no RF09 e na nota P4 do MRD.

## Mapeamento das relações

```text
users ──< quiz_attempts >── quizzes >── resources >── healthareas
                 │               │
                 │               └── quiztypes (Diagnóstico / Final)
                 └──< attempt_answers >── questions
                                      └── answers (NULL quando em branco)

users ── genders
  └── schoolyears
```

Para formar o par pré/pós, as duas notas têm de corresponder ao mesmo utilizador e a questionários associados ao mesmo recurso, diferenciados por `quiztypes.type`.

## Limites do modelo atual

- O MRD guarda `is_correct` por tentativa, mas não define peso por pergunta. A nota `grade` é usada como resultado do questionário.
- A percentagem de acerto por pergunta é calculável com `attempt_answers`; a análise de discriminação exige uma métrica estatística própria.
- A comparação por área de saúde depende do recurso associado ao questionário, não de uma área guardada diretamente na tentativa.
