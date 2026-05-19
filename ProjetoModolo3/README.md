# 📚 SysQuiz — Visão Geral do Projeto

O **SysQuiz** é uma plataforma de estudo baseada em quizzes para **Análise de Sistemas**,
com foco em acompanhamento de desempenho, sequências de estudo e organização
por temas e níveis de dificuldade.

---

## 📄 Páginas (6 no total)

### 1. `index` — Início / Painel Pessoal
Página de boas-vindas personalizada para o usuário logado. Contém:
- Cabeçalho com saudação dinâmica: *"Pronto para o próximo desafio, [nome]?"*
- Métricas rápidas: Quizzes Realizados, Média Recente (30d) e Sequência Atual
- **Semana de Estudos:** Calendário semanal com dias ativos (Seg–Dom)
- **Pontos a Melhorar:** Lista de temas com baixo percentual de acerto, com botão *"Iniciar quiz sugerido"*
- **Acesso Rápido por Tema:** Grade de temas com desempenho por nível (Fácil / Médio / Difícil) e botão *"Praticar [Tema]"*

> ⚡ Workflow: botão `suggestion-cta` redireciona para outra página (`ChangePage`)

---

### 2. `dashboard` — Painel de Desempenho
Página analítica detalhada com visão histórica do progresso:
- **Filtros:** Período, Tema e Nível
- **Cards de métricas:** Quizzes Realizados, Média de Acertos, Evolução Mensal (vs. mês anterior) e Sequência Atual
- Gráfico de Evolução de Desempenho com comparativo *"Média da Turma"*
- Calendário de sequência semanal (Seg–Dom)
- **Desempenho por Tema:** Barras com percentual por área (Eng. de Prompt, Prototipagem, Programação, UX/Jornada)
- **Matriz Tema × Nível:** Tabela com acerto médio e esforço por combinação de tema e dificuldade
- **Pontos a Melhorar:** Combinações com menos de 60% de acerto — botão *"Praticar agora"*
- **Sequência Semanal:** Sequência atual e recorde do mês

> ⚡ Workflow: botão `imp-row-btn` redireciona (`ChangePage`)

---

### 3. `quizzes` — Catálogo de Quizzes
Página central de execução de quizzes:
- Filtro por nível: Fácil, Médio, Difícil
- **Cards de Quiz:** Tema, quantidade de questões, dificuldade, último resultado, status (Concluído / Refeito), botões *"Iniciar"* e *"Refazer"*
- **Modal de execução:** Questão atual (ex: *"Questão 3 de 8"*), texto da pergunta, feedback (*"Correto!" + explicação*), botões *"Confirmar resposta"* e *"Finalizar Quiz"*
- **Modal de resultado final:** Pontuação (acertos/total), percentual de acertos, status e gabarito comentado com resposta selecionada vs. correta

> ⚡ Workflows: 8 botões gerenciam abertura/fechamento de modais, exibição de dados do quiz e resultado

---

### 4. `profile` — Perfil do Usuário
Página de perfil pessoal com conquistas e histórico:
- **Header:** Nome, Turma, Sequência atual e Recorde do mês
- **Conquistas:** Total de Quizzes, Tema Favorito, Nível Mais Praticado e Melhor Desempenho (% máximo)
- **Sequência de Estudos:** Sequência atual e melhor sequência do mês
- **Histórico de Quizzes:** Tabela com todos os quizzes (Data, Tema, Nível, Pontos, Acertos %, Status)
- **Popup "Editar Perfil":** Campos para Foto, Nome e Turma — salva com `ChangeThing(CurrentUser)` e exibe popup de confirmação *"Alterações salvas!"*

> ⚡ Workflows: 5 botões de gerenciamento de edição e confirmação de perfil

---

### 5. `404` — Página Não Encontrada
Página estática de erro com mensagem em inglês e botão **"Go Home"** (`ChangePage`).

---

### 6. `reset_pw` — Redefinir Senha
Página simples com campos *"Nova senha"* e *"Confirmar nova senha"*, botão **"Confirmar"** que aciona `ResetPassword` + `ChangePage`.

---

## ⚠️ Problemas Detectados (23)

O projeto possui **23 erros ativos**. Os principais padrões são:

- **Tipo de dado incorreto em Data Source:** Vários grupos esperam um tipo de dado (ex: `User`, `QuizAttempt`) mas estão recebendo um número ou valor vazio.
  - Exemplos: `group metric-total-quizzes`, `group metric-streak`, `group streak-footer`

- **Filtro com tipo errado:** `Search for QuizAttempts` em vários grupos espera `List of texts` mas recebe um `text` simples — ocorre nas páginas `index` e `profile`

- **Expressões não imprimíveis em texto:** `Text suggestion-accuracy`, `Text topic-card-status` e `Text topic-card-overall-accuracy` possuem expressões dinâmicas que retornam tipos não-texto

- **Data Source não configurada:** `Group suggestions-list` e `Group topics-grid` estão sem fonte de dados configurada corretamente

---

## 🗃️ Tipos de Dados

| Tipo | Campos Identificados |
|------|----------------------|
| `User` | `name_text`, `turma_text`, `current_streak_number`, `best_streak_month_number` |
| `QuizAttempt` | `user_user`, `quiz_custom_quiz`, `attempted_at_date`, `status_text`, `accuracy_percentage_number`, `score_number`, `correct_answers_number`, `total_questions_number` |
| `Quiz` | `topic_text`, `difficulty_text` |
| `Question` | `quiz_custom_quiz`, `question_text_text`, `number_number`, `correct_answer_text`, `explanation_text` |
| `AnswerOption` | `option_text_text`, `question_custom_question` |
| `StreakDay` | `user_user`, `date_date` |

https://xandebrian009.bubbleapps.io/version-test/?debug_mode=true
Alexandre e Mateus
