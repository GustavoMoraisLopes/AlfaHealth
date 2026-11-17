# Dicionário de Dados — ALFAS

Este dicionário acompanha o Modelo Relacional v1.1 usado no projeto. Os nomes das tabelas e dos campos ficam em inglês para poderem ser comparados diretamente com o ficheiro `modelos-dados.drawio`.

## Convenções e limites

- `PK` é chave primária, `FK` é chave estrangeira e `UK` indica um valor único.
- `—*` significa que o tipo SQL, o tamanho e o default não estão especificados no MRD; ficam para a Sprint B, quando for definida a base de dados física. A nulabilidade só é indicada nos campos em que as regras do modelo a definem; nos restantes, não está especificada no MRD.
- As relações e regras abaixo seguem o MRD. Quando uma regra vem de uma nota do diagrama, é indicada junto da tabela correspondente.

## Utilizadores e permissões

### `users`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica a conta. |
| `name` | —* |  | Nome do utilizador. |
| `gender_id` | —* | FK → `genders.id` | Género escolhido no perfil. |
| `schoolyear_id` | —* | FK → `schoolyears.id` | Ano de escolaridade indicado no perfil. |
| `birth_date` | —* |  | Data de nascimento, usada para determinar menoridade. |
| `language_id` | —* | FK → `languages.id` | Idioma preferido. O MRD indica PT como valor por omissão. |
| `email` | —* |  | Endereço de email do utilizador. |
| `img_url` | —* |  | URL da imagem do utilizador. |
| `email_verified_at` | —* | NULL permitido | Data/hora de confirmação do email; fica NULL enquanto o email não for confirmado. |
| `password` | —* |  | Palavra-passe da conta. O requisito do projeto exige que seja guardada de forma segura. |
| `remember_token` | —* |  | Token usado para manter a sessão, quando aplicável. |
| `userstate_id` | —* | FK → `userstates.id` | Estado atual da conta. A nota P5 enumera os estados usados no registo e no consentimento. |

### `genders`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica o registo de género. |
| `gender` | —* |  | Nome do género apresentado. |

**Valores:** Masculino, Feminino, Outro, PrefiroNãoDizer.

### `schoolyears`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica o ano de escolaridade. |
| `schoolyear` | —* |  | Ano de escolaridade apresentado. |

**Valores:** 7.º, 8.º, 9.º, 10.º, 11.º e 12.º ano.

### `userstates`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do estado da conta. |
| `state` | —* |  | Estado da conta. A nota P5 menciona PendenteEmail, PendenteConsentimento, Ativo e Bloqueado. |

**Valores:** PendenteEmail, PendenteConsentimento, Ativo, Bloqueado.

### `roles`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica o papel. |
| `name` | —* |  | Nome do papel. Valores: `UtilizadorRegistado`, `Manager`, `Administrador`. |

**Valores:** UtilizadorRegistado, Manager, Administrador.

### `role_user`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `role_id` | —* | PK composta, FK1 → `roles.id` | Papel associado ao utilizador. |
| `user_id` | —* | PK composta, FK2 → `users.id` | Utilizador associado ao papel. |

## Recursos e conteúdos

### `resources`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica o recurso. |
| `name` | —* |  | Nome do recurso. |
| `description` | —* |  | Descrição do recurso. |
| `healtharea_id` | —* | FK → `healthareas.id` | Área de saúde do recurso. |
| `resourcetype_id` | —* | FK → `resourcetypes.id` | Tipo do recurso. |
| `resourcestate_id` | —* | FK → `resourcestates.id` | Estado de publicação/gestão do recurso. |
| `img_url` | —* |  | URL da imagem do recurso. |
| `badge_url` | —* |  | Endereço da imagem do badge do recurso. |

### `healthareas`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica a área de saúde. |
| `title` | —* |  | Título da área. |
| `subtitle` | —* |  | Subtítulo da área. |
| `description` | —* |  | Descrição da área. |
| `icon` | —* |  | Ícone associado à área. |
| `img_url` | —* |  | URL da imagem da área. |
| `video_url` | —* |  | URL do vídeo associado à área. |
| `resourcestate_id` | —* | FK → `resourcestates.id` | Estado de publicação da área. |

### `resourcetypes`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica o tipo de recurso. |
| `type` | —* |  | Nome do tipo de recurso. |

**Valores:** Workshop, Webinar.

### `resourcestates`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identifica o estado do recurso. |
| `state` | —* |  | Nome do estado do recurso. |

**Valores:** Rascunho, Publicado, Arquivado.

### `resourcelevels`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do nível do recurso. |
| `level` | —* |  | Número ou designação do nível. |
| `title` | —* |  | Título do nível. |
| `description` | —* |  | Descrição do nível. |
| `video_url` | —* |  | URL do vídeo do nível. |
| `pdf_url` | —* |  | URL do PDF do nível. |
| `resource_id` | —* | FK → `resources.id` | Recurso a que pertence o nível. |
| `resourcestate_id` | —* | FK → `resourcestates.id` | Estado do nível. |

### `contents`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do conteúdo. |
| `title` | —* |  | Título do conteúdo. |
| `description` | —* |  | Descrição do conteúdo. |
| `author` | —* |  | Autor do conteúdo. |
| `url` | —* |  | URL do conteúdo. |
| `healtharea_id` | —* | FK → `healthareas.id` | Área de saúde associada ao conteúdo. |
| `resourcestate_id` | —* | FK → `resourcestates.id` | Estado do conteúdo. |
| `contenttype_id` | —* | FK → `contenttypes.id` | Tipo do conteúdo. |

### `contenttypes`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do tipo de conteúdo. |
| `type` | —* |  | Designação do tipo de conteúdo. |

**Valores:** Artigo, Vídeo, Documento, Infografia, Podcast.

### `news`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da notícia. |
| `title` | —* |  | Título da notícia. |
| `description` | —* |  | Texto descritivo da notícia. |
| `author` | —* |  | Autor da notícia. |
| `news_date` | —* |  | Data da notícia. |
| `img_url` | —* |  | URL da imagem da notícia. |
| `healtharea_id` | —* | FK → `healthareas.id` | Área de saúde associada à notícia. |
| `resourcestate_id` | —* | FK → `resourcestates.id` | Estado da notícia. |

### `activities`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da atividade. |
| `title` | —* |  | Título da atividade. |
| `description` | —* |  | Descrição da atividade. |
| `activity_datetime` | —* |  | Data e hora da atividade. |
| `url` | —* |  | URL relacionada com a atividade. |
| `healtharea_id` | —* | FK → `healthareas.id` | Área de saúde associada à atividade. |
| `resourcestate_id` | —* | FK → `resourcestates.id` | Estado da atividade. |

## Questionários e avaliação

### `quizzes`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do questionário. |
| `name` | —* |  | Nome do questionário. |
| `description` | —* |  | Descrição do questionário. |
| `resource_id` | —* | FK → `resources.id` | Recurso a que pertence o questionário. |
| `quiztype_id` | —* | FK → `quiztypes.id` | Tipo do questionário, por exemplo diagnóstico ou final. |
| `qastate_id` | —* | FK → `qastates.id` | Estado do questionário. |
| `max_attempts` | —* |  | Número máximo de tentativas; a nota P2 indica 2 para diagnóstico e 1 para final. |
| `pass_grade` | —* |  | Nota mínima de aprovação; a nota P4 indica default de 85%. |

**Regra indicada no MRD:** existe no máximo um questionário de cada tipo por recurso (`UNIQUE(resource_id, quiztype_id)`).

### `quiztypes`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do tipo de questionário. |
| `type` | —* |  | Designação do tipo de questionário. |

**Valores:** Diagnóstico, Final.

### `qastates`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do estado de questionário/pergunta/resposta. |
| `state` | —* |  | Designação do estado. |

**Valores:** Ativa, Inativa.

### `questions`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da pergunta. |
| `title` | —* |  | Enunciado da pergunta. |
| `quiz_id` | —* | FK → `quizzes.id` | Questionário a que pertence a pergunta. |
| `qastate_id` | —* | FK → `qastates.id` | Estado da pergunta. |

### `answers`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da resposta possível. |
| `answer` | —* |  | Texto da resposta possível. |
| `question_id` | —* | FK → `questions.id` | Pergunta a que pertence a resposta. |
| `correct` | —* |  | Indica se a resposta é considerada correta. |
| `qastate_id` | —* | FK → `qastates.id` | Estado da resposta. |

### `quiz_attempts`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tentativa. |
| `grade` | —* | NULL permitido | Nota da tentativa; fica NULL se a tentativa for abandonada antes da submissão. A nota P2 indica escala de 0 a 100%. |
| `submitted_at` | —* | NULL permitido | Data e hora de submissão; fica NULL se a tentativa for abandonada. |
| `user_id` | —* | FK → `users.id` | Utilizador que respondeu. |
| `quiz_id` | —* | FK → `quizzes.id` | Questionário respondido. |
| `attempt_number` | —* |  | Número sequencial da tentativa do utilizador. |
| `started_at` | —* |  | Data e hora de início. |

**Regra indicada no MRD:** `UNIQUE(user_id, quiz_id, attempt_number)`. O cálculo do ganho usa a primeira tentativa do diagnóstico.

### `attempt_answers`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do registo de resposta. |
| `quiz_attempt_id` | —* | FK → `quiz_attempts.id` | Tentativa a que pertence a resposta. |
| `question_id` | —* | FK → `questions.id` | Pergunta respondida ou deixada em branco. |
| `answer_id` | —* | FK → `answers.id`, NULL permitido | Resposta escolhida. Fica NULL quando a pergunta é deixada em branco; essa resposta conta como errada. |
| `is_correct` | —* |  | Resultado de correção guardado na submissão, preservando o histórico. |

**Regra indicada no MRD:** `UNIQUE(quiz_attempt_id, question_id)`. A coerência entre `question_id` e `answer_id` é validada no backend.

## Inscrições e conclusão de formações

### `enrollments`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da inscrição. |
| `user_id` | —* | FK → `users.id` | Utilizador inscrito. |
| `resource_id` | —* | FK → `resources.id` | Recurso em que o utilizador se inscreveu. |
| `enrollmentstate_id` | —* | FK → `enrollmentstates.id` | Estado da inscrição. |
| `enrolled_at` | —* |  | Data e hora da inscrição. |
| `completed_at` | —* | NULL permitido | Data e hora da conclusão; fica NULL enquanto a inscrição não estiver concluída. |

**Regras indicadas no MRD:** `UNIQUE(user_id, resource_id)`. Estados indicados: inscrito, em curso, concluído e cancelado.

### `enrollmentstates`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do estado da inscrição. |
| `state` | —* |  | Designação do estado da inscrição. |

**Valores:** Inscrito, EmCurso, Concluído, Cancelado.

### `favorites`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `user_id` | —* | PK composta, FK1 → `users.id` | Utilizador que marcou o recurso como favorito. |
| `resource_id` | —* | PK composta, FK2 → `resources.id` | Recurso marcado como favorito. |
| `created_at` | —* |  | Data e hora em que o favorito foi criado. |

### `resourcelevel_user`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do progresso no nível. |
| `enrollment_id` | —* | FK → `enrollments.id` | Inscrição a que pertence o progresso. |
| `resourcelevel_id` | —* | FK → `resourcelevels.id` | Nível cujo progresso é acompanhado. |
| `progress` | —* |  | Progresso do utilizador nesse nível. |

### `completions`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do registo de conclusão/certificação. |
| `enrollment_id` | —* | FK → `enrollments.id` | Inscrição concluída. |
| `quiz_attempt_id` | —* | FK → `quiz_attempts.id` | Tentativa associada à emissão. |
| `certificate_code` | —* | UK | Código único do certificado. |
| `issued_at` | —* |  | Data e hora de emissão do certificado. |

**Nota do MRD:** o badge usa `resources.badge_url`; a regra de aprovação é definida em `quizzes.pass_grade` e aplicada no backend.

## Notícias, atividades e destaques

### `highlights`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do destaque. |
| `resource_id` | —* | FK → `resources.id`, NULL se não selecionado | Recurso destacado, quando este é o tipo escolhido. |
| `news_id` | —* | FK → `news.id`, NULL se não selecionado | Notícia destacada, quando este é o tipo escolhido. |
| `activity_id` | —* | FK → `activities.id`, NULL se não selecionado | Atividade destacada, quando este é o tipo escolhido. |
| `content_id` | —* | FK → `contents.id`, NULL se não selecionado | Conteúdo destacado, quando este é o tipo escolhido. |
| `starts_at` | —* |  | Início do período do destaque. |
| `ends_at` | —* |  | Fim do período do destaque. |
| `position` | —* |  | Posição de apresentação do destaque. |
| `created_by` | —* | FK → `users.id` | Utilizador que criou o destaque. |

**Regra indicada no MRD:** exatamente uma das quatro referências (`resource_id`, `news_id`, `activity_id`, `content_id`) deve estar preenchida.

## Consentimento parental e idiomas

### `parental_consents`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do registo de consentimento. |
| `user_id` | —* | FK → `users.id` | Conta de menor a que o consentimento se refere. |
| `guardian_name` | —* |  | Nome do encarregado de educação. |
| `guardian_email` | —* |  | Email do encarregado de educação. |
| `token_hash` | —* |  | Hash do token usado no pedido de consentimento. |
| `requested_at` | —* |  | Data e hora do pedido. |
| `expires_at` | —* |  | Data e hora de expiração do pedido. |
| `consented_at` | —* | NULL permitido | Data e hora em que o consentimento foi dado; fica NULL enquanto não houver consentimento. |
| `revoked_at` | —* | NULL permitido | Data e hora da revogação; fica NULL enquanto o consentimento não for revogado. |

**Regra indicada no MRD:** a renovação é registada numa nova linha, preservando a linha anterior e o histórico. Após revogação, a conta fica bloqueada; sem novo consentimento em 30 dias, a conta e os dados pessoais são apagados.

### `languages`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador do idioma. |
| `code` | —* | UK | Código único do idioma. |
| `name` | —* |  | Nome do idioma. |

**Idiomas previstos inicialmente:** PT e EN. A nota P6 prevê que possam ser acrescentados outros idiomas.

## Tabelas de tradução

As tabelas de tradução guardam valores localizados associados à entidade original e ao idioma. O MRD indica unicidade por par entidade/idioma (`UNIQUE(entidade_id, language_id)`). O texto base das tabelas originais é PT; as tabelas abaixo suportam EN e futuros idiomas.

### `resource_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `resource_id` | —* | FK → `resources.id` | Recurso traduzido. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `name` | —* |  | Nome traduzido do recurso. |
| `description` | —* |  | Descrição traduzida do recurso. |

### `resourcelevel_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `resourcelevel_id` | —* | FK → `resourcelevels.id` | Nível traduzido. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `title` | —* |  | Título traduzido do nível. |
| `description` | —* |  | Descrição traduzida do nível. |

### `healtharea_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `healtharea_id` | —* | FK → `healthareas.id` | Área de saúde traduzida. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `title` | —* |  | Título traduzido da área. |
| `subtitle` | —* |  | Subtítulo traduzido da área. |
| `description` | —* |  | Descrição traduzida da área. |

### `news_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `news_id` | —* | FK → `news.id` | Notícia traduzida. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `title` | —* |  | Título traduzido da notícia. |
| `description` | —* |  | Descrição traduzida da notícia. |

### `activity_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `activity_id` | —* | FK → `activities.id` | Atividade traduzida. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `title` | —* |  | Título traduzido da atividade. |
| `description` | —* |  | Descrição traduzida da atividade. |

### `content_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `content_id` | —* | FK → `contents.id` | Conteúdo traduzido. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `title` | —* |  | Título traduzido do conteúdo. |
| `description` | —* |  | Descrição traduzida do conteúdo. |

### `quiz_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `quiz_id` | —* | FK → `quizzes.id` | Questionário traduzido. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `name` | —* |  | Nome traduzido do questionário. |
| `description` | —* |  | Descrição traduzida do questionário. |

### `question_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `question_id` | —* | FK → `questions.id` | Pergunta traduzida. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `title` | —* |  | Enunciado traduzido da pergunta. |

### `answer_translations`

| Campo | Tipo | Chave / relação | Significado |
|---|---|---|---|
| `id` | —* | PK | Identificador da tradução. |
| `answer_id` | —* | FK → `answers.id` | Resposta traduzida. |
| `language_id` | —* | FK → `languages.id` | Idioma da tradução. |
| `answer` | —* |  | Texto traduzido da resposta. |

## Definido para a Sprint B

O MRD v1.1 ainda não especifica os tipos SQL, tamanhos ou defaults dos campos. Segundo a equipa, esses detalhes serão definidos na Sprint B, quando for criada a base de dados física. Por isso, os campos estão marcados com `—*` e não lhes foram atribuídos tipos por inferência.
