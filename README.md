# Respostas do Laboratório: Gestão de Configuração Moderna com Git e GitHub

Este documento apresenta as respostas detalhadas para as perguntas e desafios propostos no laboratório de Gestão de Configuração Moderna com Git e GitHub.

## Parte 3: Fluxo de Trabalho Intermediário - Branches e Merges

### Pergunta: O que acontece com o arquivo alterado quando ocorre o merge de uma branch para a branch principal, considerando que a sua versão anterior está disponível na principal?

Quando uma branch (por exemplo, `feature-despedida`) é mesclada na branch principal (`main`), o Git tenta integrar as alterações de forma inteligente. Se as alterações na `feature-despedida` não entrarem em conflito com as alterações na `main` (ou seja, se as mesmas linhas de código não foram modificadas de forma diferente em ambas as branches), o Git realizará um *fast-forward merge* (se possível) ou um *three-way merge*.

No caso de um *three-way merge*, o Git cria um novo commit de merge na branch `main` que incorpora as mudanças de ambas as branches. As alterações feitas na `feature-despedida` (como a adição da mensagem "Adeus!") serão aplicadas ao arquivo na `main`. A versão anterior do arquivo na `main` é preservada no histórico de commits, mas o estado atual do arquivo na `main` após o merge refletirá as mudanças da `feature-despedida`.

Se houver conflitos (as mesmas linhas foram alteradas de forma diferente), o Git pausará o merge e exigirá que o desenvolvedor resolva manualmente os conflitos antes de finalizar o commit de merge. Após a resolução, o arquivo na `main` conterá as alterações combinadas de ambas as branches.

## Parte 4: Análise do Repositório do Projeto Integrador

Para as análises a seguir, consideraremos um repositório hipotético com o histórico de commits fornecido nos exemplos do laboratório. É importante notar que, na prática, seria necessário clonar um repositório real para obter os dados exatos.

### Pergunta 1: Quem Contribuiu Mais para o Projeto?

#### Desafio 1.1: Ranking de Contribuidores

**Pergunta:** Quem é o contribuidor número 1 do projeto? Qual é a distribuição de commits entre os membros da equipe?

**Comando Utilizado:**
```bash
git shortlog -s -n -e
```

**Exemplo de Saída (conforme o laboratório):**
```
     9        Bily <36426745+bily@users.noreply.github.com>
     2        bily <bily@gmail.com>
```

**Análise e Resposta:**

*   **Contribuidor número 1:** Bily, com 9 commits.
*   **Distribuição de commits:** A distribuição de commits é **concentrada**. Bily é o contribuidor dominante com a maioria dos commits (9 de 11 commits totais, considerando o exemplo). Isso pode indicar que Bily é o desenvolvedor principal, o líder técnico, ou que a equipe é pequena e o esforço está centralizado em um único membro. Também pode sugerir a necessidade de envolver mais membros da equipe no desenvolvimento para distribuir o conhecimento e a carga de trabalho.

#### Desafio 1.2: Contribuições Recentes

**Pergunta:** Quantas pessoas diferentes trabalharam no projeto nas últimas 2 semanas? Quem foi o mais ativo nesse período?

**Comando Utilizado:**
```bash
git log --since="2 weeks ago" --format="%an" | sort | uniq -c
```

**Exemplo de Saída (não fornecido diretamente, mas inferido pela análise):**
Considerando que a análise do laboratório indica que o projeto teve atividade recente, mas apenas um desenvolvedor trabalhou nele, e que os commits são de abril de 2024, para a data atual (15 de junho de 2026), não haveria commits nas últimas 2 semanas. No entanto, para fins de demonstração e seguindo a lógica do laboratório, se houvesse atividade, a saída seria algo como:
```
     X        NomeDoAutor
```

**Análise e Resposta:**

*   **Pessoas diferentes nas últimas 2 semanas:** 0 pessoas (assumindo a data atual de 15 de junho de 2026 e os commits de abril de 2024). Se considerarmos o contexto do laboratório onde a atividade é recente, a resposta seria "n pessoas", onde 'n' é o número de autores únicos. No exemplo de análise, é mencionado "apenas n desenvolvedor", sugerindo 1 desenvolvedor.
*   **Mais ativo nesse período:** Não houve atividade recente. Se houvesse, seria o "autor com n commits" conforme a saída do comando.
*   **Indicação sobre a atividade do projeto:** O projeto não teve atividade nas últimas 2 semanas, o que, combinado com a análise da Pergunta 5, sugere que o projeto está finalizado ou em pausa, o que é comum para projetos integradores de disciplina.

### Pergunta 2: Qual é o Padrão de Mensagens de Commit?

#### Desafio 2.1: Análise do Histórico de Commits

**Pergunta:** O projeto segue o padrão de Conventional Commits? As mensagens são descritivas e claras?

**Comando Utilizado:**
```bash
git log --oneline
```

**Exemplo de Saída (conforme o laboratório):**
```
99d03ac Update analysis on inflation and family debt correlation
fc387ff Update README.md
cd6c743 Enhance README with ML model details and project structure
6352a73 Revise dashboard section in README
977fe66 Update dashboard image and add interactive link
f4811d8 Update README.md
8bedda3 Merge branch 'main' of https://github.com/joasweslei/FinancialSense
db78ae0 Update repository URL in README
c874248 feat: pipeline ETL de indicadores macroeconômicos
daac49f Enhance README with project details and insights
af6370b Initial commit
```

**Análise e Resposta:**

*   **Padrão de Conventional Commits:** O projeto segue o padrão de Conventional Commits **parcialmente**. Existe um commit que adere ao padrão (`c874248 feat: pipeline ETL de indicadores macroeconômicos`), mas a maioria dos commits não o faz. Exemplos de commits que não seguem o padrão incluem `Update README.md` e `Enhance README with ML model details...`.
*   **Tipo de commit mais frequente:** O tipo de commit mais frequente são as **atualizações de documentação (README updates)**, representando uma parcela significativa (aproximadamente 70%) dos commits no exemplo fornecido.
*   **Mensagens descritivas e claras:** Sim, as mensagens são geralmente **claras e descritivas**. Elas comunicam bem o propósito das alterações. No entanto, poderiam ser mais consistentes e aderir ao padrão Conventional Commits para melhorar a padronização e a automação de ferramentas.

#### Desafio 2.2: Contagem de Tipos de Commit

**Pergunta:** Qual é o tipo de commit mais comum no projeto? Existe algum tipo que não deveria estar no histórico? Qual é a sua recomendação para melhorar o padrão de commits?

**Comando Utilizado:**
```bash
git log --pretty=format:"%s" | grep -o "^[a-z]*:" | sort | uniq -c | sort -rn
```

**Exemplo de Saída (não fornecido diretamente, mas inferido pela análise):**
```
      1 feat:
```
(Isso representa apenas o commit `feat:` explícito. Os outros commits não teriam um prefixo `tipo:` e, portanto, não seriam contados por este `grep` específico).

**Análise e Resposta:**

*   **Tipo de commit mais comum:** Apenas 1 commit segue explicitamente o padrão Conventional Commits (`feat:`). A maioria dos commits não possui um prefixo de tipo, o que indica uma falta de padronização.
*   **Tipo de commit que não deveria estar no histórico:** Não há commits intrinsecamente "ruins" no sentido de serem maliciosos ou irrelevantes. No entanto, há uma **inconsistência** no uso do padrão. Muitos commits são atualizações de README que poderiam ser agrupados ou ter um padrão melhor (ex: `docs: update README`). Mensagens genéricas como `Update README.md` poderiam ser mais específicas.
*   **Recomendação para melhorar o padrão de commits:** A principal recomendação é **adotar o padrão Conventional Commits de forma consistente** em todos os commits futuros. Isso inclui o uso de prefixos como `feat:`, `fix:`, `docs:`, `style:`, `refactor:`, etc., seguidos de uma descrição concisa e clara. Por exemplo, em vez de `Update README.md`, usar `docs: update README with ML model details`.

### Pergunta 3: Qual Arquivo Recebeu Mais Atenção?

#### Desafio 3.1: Arquivos Mais Modificados

**Pergunta:** Qual é o arquivo mais modificado do projeto? Quantas vezes foi alterado? Por que você acha que recebeu tanta atenção?

**Comando Utilizado:**
```bash
git log --name-only --pretty=format: | sort | uniq -c | sort -rn
```

**Exemplo de Saída (conforme o laboratório):**
```
      8 README.md
      1 src/transformer.py
      1 src/extractor.py
      1 requirements.txt
      1 main.py
      1 LICENSE
      1 .gitignore
```

**Análise e Resposta:**

*   **Arquivo mais modificado:** O arquivo mais modificado do projeto é o `README.md`.
*   **Quantas vezes foi alterado:** Foi alterado **8 vezes**.
*   **Por que recebeu tanta atenção:** O `README.md` é a documentação principal do projeto e, frequentemente, o primeiro ponto de contato para novos colaboradores ou usuários. Receber muitas atualizações indica que:
    *   A documentação está sendo **constantemente melhorada e mantida atualizada**.
    *   O projeto está em uma fase de **desenvolvimento ativo**, com mudanças frequentes que exigem a atualização da documentação.
    *   A equipe **valoriza a documentação** e se preocupa em fornecer informações claras e completas sobre o projeto.

#### Desafio 3.2: Quem Trabalhou em Qual Arquivo?

**Pergunta:** Quem modificou o arquivo mais alterado? Essa pessoa é especialista nessa área?

**Comando Utilizado:**
```bash
git log --pretty=format:"%an" -- README.md | sort | uniq -c
```

**Exemplo de Saída (conforme o laboratório):**
```
      8 Joás
```

**Análise e Resposta:**

*   **Quem trabalhou mais nesse arquivo:** Joás, com 8 modificações.
*   **Especialista nessa área:** Sim, a análise sugere que Joás é o responsável pela documentação do projeto. Isso indica que ele é um **especialista ou o principal mantenedor da documentação**, garantindo que ela esteja sempre atualizada e alinhada com o desenvolvimento do projeto.

### Pergunta 4: Como é o Fluxo de Trabalho da Equipe?

#### Desafio 4.1: Análise de Branches

**Pergunta:** Quantas branches existem no repositório? Qual é a principal branch de desenvolvimento? Existem branches de feature ou hotfix ativas?

**Comando Utilizado:**
```bash
git branch -a
```

**Exemplo de Saída (não fornecido diretamente, mas inferido pela análise):**
```
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```
(Considerando o exemplo de análise do laboratório, que menciona apenas a `main` como branch principal e não mostra outras branches ativas no histórico de commits.)

**Análise e Resposta:**

*   **Número de branches:** Considerando o histórico de commits fornecido e a análise do laboratório, o repositório parece ter **uma branch principal (`main`)** e, possivelmente, branches remotas correspondentes. Se o laboratório tivesse sido executado completamente, haveria também `feature-despedida` e `hotfix-readme`.
*   **Principal branch de desenvolvimento:** A principal branch de desenvolvimento é a `main`.
*   **Branches de feature ou hotfix ativas:** No exemplo de saída, não há branches de feature ou hotfix ativas visíveis. No entanto, o laboratório descreve a criação e merge de `feature-despedida` e `hotfix-readme`, indicando que essas branches foram usadas e posteriormente mescladas na `main`.

#### Desafio 4.2: Frequência de Merges

**Pergunta:** Com que frequência as branches são mescladas na principal? Isso indica um fluxo de trabalho contínuo ou baseado em releases?

**Comando Utilizado:**
```bash
git log --oneline --merges
```

**Exemplo de Saída (não fornecido diretamente, mas inferido pela análise):**
```
8bedda3 Merge branch 'main' of https://github.com/joasweslei/FinancialSense
```
(Apenas um commit de merge explícito é mostrado no histórico de exemplo do laboratório, que é um merge da própria `main` consigo mesma, o que pode ser um merge de pull request ou um merge de uma branch remota para a local.)

**Análise e Resposta:**

*   **Frequência de merges:** Com base no histórico de exemplo, há **poucos merges explícitos** (`Merge branch 'main' of...`). O laboratório descreve merges de `feature-despedida` e `hotfix-readme` na `main`, mas estes não aparecem como commits de merge distintos no `git log --oneline` fornecido como exemplo de saída para a Pergunta 2.1. Se considerarmos apenas o exemplo, a frequência é baixa.
*   **Indicação sobre o fluxo de trabalho:** A baixa frequência de merges explícitos (ou a ausência de múltiplos merges de feature branches) pode indicar um fluxo de trabalho **mais baseado em releases ou em desenvolvimento centralizado**, onde as integrações são menos frequentes. Se o projeto tivesse um fluxo de trabalho contínuo com muitas features sendo desenvolvidas em paralelo, esperaríamos ver mais commits de merge. No contexto de um projeto integrador de disciplina, é comum que o fluxo seja mais linear ou com poucas branches de curta duração.

### Pergunta 5: Qual é o Padrão de Atividade do Projeto?

#### Desafio 5.1: Atividade por Data

**Pergunta:** Em qual data houve mais commits? Qual é o padrão de atividade? O projeto está em desenvolvimento ativo ou finalizado?

**Comando Utilizado:**
```bash
git log --pretty=format:"%ad" --date=format:"%Y-%m-%d" | sort | uniq -c | sort -rn
```

**Exemplo de Saída (conforme o laboratório):**
```
     10 2024-04-21
      1 2024-04-20
```

**Análise e Resposta:**

*   **Data com mais commits:** Houve mais commits em **2024-04-21**, com 10 commits.
*   **Padrão de atividade:** A atividade é **concentrada em um curto período de tempo**, especificamente em dois dias (2024-04-20 e 2024-04-21). Isso sugere que o projeto foi desenvolvido em uma **sprint intensa ou um período de desenvolvimento focado**, o que é comum para projetos com prazos definidos, como projetos de conclusão de disciplina.
*   **Projeto em desenvolvimento ativo ou finalizado:** O projeto parece estar **finalizado ou em pausa**. Todos os commits são do mesmo período (abril de 2024), e não há atividade recente (considerando a data atual de 15 de junho de 2026). Isso é típico de um projeto integrador que foi entregue e não está mais em desenvolvimento ativo.

#### Desafio 5.2: Tempo Desde o Último Commit

**Pergunta:** Quando foi o último commit? Quanto tempo se passou desde então? O que isso indica sobre o status do projeto?

**Comando Utilizado:**
```bash
git log -1 --pretty=format:"%ai"
```

**Exemplo de Saída (conforme o laboratório):**
```
2024-04-21 12:34:56 -0300
```

**Análise e Resposta:**

*   **Último commit:** O último commit foi em **2024-04-21 às 12:34:56 (horário de Brasília)**.
*   **Tempo desde então:** Considerando a data atual de 15 de junho de 2026, aproximadamente **8 semanas** se passaram desde o último commit.
*   **Indicação sobre o status do projeto:** O fato de não haver atualizações recentes por um período de 8 semanas indica que o projeto **não está em desenvolvimento ativo**. Isso é esperado para um projeto integrador que já foi entregue e concluído, confirmando a análise do desafio anterior.

### Pergunta 6: Qual é a Qualidade do Histórico de Commits?

#### Desafio 6.1: Tamanho Médio dos Commits

**Pergunta:** Quantos arquivos foram modificados no total? Qual é a média de arquivos por commit? Os commits são "pequenos e focados" ou "grandes e complexos"?

**Comando Utilizado:**
```bash
git log --name-only --pretty=format: | grep -v "^$" | wc -l
```

**Exemplo de Saída (conforme o laboratório):**
```
14
```

**Análise e Resposta:**

*   **Arquivos modificados no total:** Foram 14 modificações de arquivo (contando repetições).
*   **Média de arquivos por commit:** Considerando 11 commits (conforme o exemplo de `git log --oneline` na Pergunta 2.1), a média é de 14 modificações ÷ 11 commits ≈ **1,27 arquivos por commit**.
*   **Commits "pequenos e focados" ou "grandes e complexos":** Os commits são **pequenos e focados**. Uma média de 1,27 arquivos por commit é um indicador excelente de que cada commit se concentra em uma única alteração ou funcionalidade. Isso facilita significativamente a revisão de código, a identificação de bugs e a reversão de alterações, se necessário.

#### Desafio 6.2: Análise Qualitativa

**Pergunta:** As mensagens de commit são específicas e descritivas? Existem commits com mensagens genéricas?

**Comando Utilizado:**
```bash
git log --pretty=format:"%h - %an, %ar : %s" | head -20
```

**Exemplo de Saída (conforme o laboratório):**
```
99d03ac - Joás, 8 weeks ago : Update analysis on inflation and family debt correlation
fc387ff - Joás, 8 weeks ago : Update README.md
cd6c743 - Joás, 8 weeks ago : Enhance README with ML model details and project structure
6352a73 - Joás, 8 weeks ago : Revise dashboard section in README
977fe66 - Joás, 8 weeks ago : Update dashboard image and add interactive link
f4811d8 - Joás, 8 weeks ago : Update README.md
8bedda3 - joasweslei, 8 weeks ago : Merge branch 'main' of https://github.com/joasweslei/FinancialSense
db78ae0 - Joás, 8 weeks ago : Update repository URL in README
c874248 - joasweslei, 8 weeks ago : feat: pipeline ETL de indicadores macroeconômicos
daac49f - Joás, 8 weeks ago : Enhance README with project details and insights
af6370b - Joás, 8 weeks ago : Initial commit
```

**Análise e Resposta:**

*   **Mensagens de commit específicas e descritivas:** Sim, a **maioria das mensagens é descritiva e específica**. Exemplos notáveis incluem: `Update analysis on inflation and family debt correlation` e `Enhance README with ML model details and project structure`. Essas mensagens fornecem um bom contexto sobre as alterações realizadas.
*   **Commits com mensagens genéricas:** Sim, existem alguns commits com mensagens mais genéricas, como `Update README.md` (que aparece duas vezes). Embora não sejam totalmente inúteis, poderiam ser mais específicas para indicar exatamente o que foi atualizado no README.
*   **Parecer geral sobre a qualidade do histórico:** A qualidade geral do histórico de commits é **boa**. As mensagens são, em sua maioria, claras e informativas, o que facilita o entendimento do desenvolvimento do projeto. O principal ponto de melhoria seria a **adoção consistente do padrão Conventional Commits** e a **evitação de mensagens genéricas**, buscando sempre a maior especificidade possível para cada alteração.

### Pergunta 7: Quais São os Indicadores de Saúde do Projeto?

#### Desafio 7.2: Recomendações de Melhoria

**Pergunta:** Quais são os pontos fortes e fracos do projeto? Que ações você recomendaria?

**Análise e Resposta:**

**3 Principais Pontos Fortes:**

1.  **Commits Pequenos e Focados:** A baixa média de arquivos por commit (aproximadamente 1,27) indica que os desenvolvedores estão fazendo commits atômicos, o que facilita a revisão, o rastreamento de bugs e a manutenção do código.
2.  **Mensagens de Commit Geralmente Descritivas:** A maioria das mensagens de commit é clara e fornece um bom contexto sobre as alterações, o que é crucial para a compreensão do histórico do projeto.
3.  **Documentação Ativa (README.md):** O `README.md` é o arquivo mais modificado, sugerindo que a equipe valoriza e mantém a documentação atualizada, um ponto forte para a onboarding de novos membros e para a compreensão externa do projeto.

**3 Principais Pontos a Melhorar:**

1.  **Inconsistência no Padrão de Conventional Commits:** A adesão ao padrão Conventional Commits é parcial, o que dificulta a automação de ferramentas (como geração de changelogs) e a padronização da comunicação.
2.  **Mensagens de Commit Genéricas:** A presença de mensagens como `Update README.md` indica uma oportunidade para maior especificidade e detalhamento, mesmo em atualizações de documentação.
3.  **Atividade Concentrada e Inativa Recente:** A atividade do projeto está concentrada em um período curto e não há commits recentes, o que pode ser um ponto fraco se o projeto precisar de manutenção contínua ou evolução futura. No entanto, para um projeto de disciplina, isso é esperado.

**Ações Recomendadas:**

1.  **Implementar e Reforçar o Padrão Conventional Commits:** Estabelecer e seguir rigorosamente o padrão Conventional Commits para todos os commits. Isso pode ser feito através de ferramentas de linting de commits ou revisões de código que garantam a conformidade.
2.  **Incentivar Mensagens de Commit Mais Detalhadas:** Mesmo para atualizações de documentação ou pequenas correções, encorajar mensagens de commit que expliquem o "porquê" da mudança, além do "o quê".
3.  **Considerar um Fluxo de Trabalho de Branching Mais Robusto (se o projeto continuar):** Se o projeto for além de um contexto acadêmico, considerar a adoção de um fluxo de trabalho de branching mais formal (como Git Flow ou GitHub Flow) para gerenciar o desenvolvimento de features e releases de forma mais estruturada. No contexto atual, o fluxo simples é adequado.

## Parte 5: Entrega no Canvas LMS

Para que o professor possa avaliar seu trabalho, você deve compartilhar o link do seu repositório no Canvas, bem como as respostas da análise do Projeto Integrador. O link para o repositório GitHub será fornecido ao final deste processo.
