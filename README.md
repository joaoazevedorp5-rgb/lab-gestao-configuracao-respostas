# Respostas do Laboratório: Git e GitHub (Versão Rápida)

## Parte 3: Fluxo de Trabalho Intermediário - Branches e Merges

### Pergunta: O que acontece com o arquivo alterado quando ocorre o merge de uma branch para a branch principal, considerando que a sua versão anterior está disponível na principal?

**Resposta:** Quando você junta uma branch (tipo `feature-despedida`) na `main`, o Git tenta unir as mudanças. Se não tiver conflito, ele faz a união. A `main` vai ter as mudanças da `feature-despedida`. A versão antiga da `main` fica no histórico, mas o arquivo atual na `main` mostra as novidades. Se der conflito, o Git para e você tem que arrumar na mão antes de finalizar.

## Parte 4: Análise do Repositório do Projeto Integrador

*Lembrando que essa análise é baseada em exemplos, não em um repositório real.* 

### Pergunta 1: Quem Contribuiu Mais para o Projeto?

#### Desafio 1.1: Ranking de Contribuidores

**Pergunta:** Quem é o contribuidor número 1 do projeto? Qual é a distribuição de commits entre os membros da equipe?

**Comando:** `git shortlog -s -n -e`

**Exemplo:**
```
     9        Bily <36426745+bily@users.noreply.github.com>
     2        bily <bily@gmail.com>
```

**Resposta:**
*   **Top Contribuidor:** Bily, com 9 commits.
*   **Distribuição:** Bem concentrada no Bily. Isso pode significar que ele é o principal dev ou que a equipe é pequena. Talvez outros precisem se envolver mais.

#### Desafio 1.2: Contribuições Recentes

**Pergunta:** Quantas pessoas diferentes trabalharam no projeto nas últimas 2 semanas? Quem foi o mais ativo nesse período?

**Comando:** `git log --since="2 weeks ago" --format="%an" | sort | uniq -c`

**Resposta:**
*   **Pessoas nas últimas 2 semanas:** 0 (considerando a data atual e os commits antigos). Se tivesse atividade, seria 1 pessoa (o mais ativo).
*   **Mais ativo:** Ninguém, sem atividade recente. Isso mostra que o projeto está parado ou finalizado.

### Pergunta 2: Qual é o Padrão de Mensagens de Commit?

#### Desafio 2.1: Análise do Histórico de Commits

**Pergunta:** O projeto segue o padrão de Conventional Commits? As mensagens são descritivas e claras?

**Comando:** `git log --oneline`

**Exemplo:**
```
99d03ac Update analysis on inflation and family debt correlation
fc387ff Update README.md
...
c874248 feat: pipeline ETL de indicadores macroeconômicos
...
af6370b Initial commit
```

**Resposta:**
*   **Padrão Conventional Commits:** Só parcialmente. Tem um `feat:` mas a maioria não segue. Ex: `Update README.md` não segue.
*   **Tipo mais comum:** Atualizações de README (documentação).
*   **Mensagens:** Geralmente claras, mas poderiam ser mais padronizadas.

#### Desafio 2.2: Contagem de Tipos de Commit

**Pergunta:** Qual é o tipo de commit mais comum no projeto? Existe algum tipo que não deveria estar no histórico? Qual é a sua recomendação para melhorar o padrão de commits?

**Comando:** `git log --pretty=format:"%s" | grep -o "^[a-z]*:" | sort | uniq -c | sort -rn`

**Exemplo:**
```
      1 feat:
```

**Resposta:**
*   **Tipo mais comum:** Apenas 1 `feat:` explícito. A maioria não tem prefixo.
*   **Commits "ruins":** Não, mas são inconsistentes. Muitos `Update README.md` poderiam ser `docs: update README`.
*   **Recomendação:** Usar Conventional Commits sempre (`feat:`, `fix:`, `docs:`, etc.) e ser mais específico nas mensagens.

### Pergunta 3: Qual Arquivo Recebeu Mais Atenção?

#### Desafio 3.1: Arquivos Mais Modificados

**Pergunta:** Qual é o arquivo mais modificado do projeto? Quantas vezes foi alterado? Por que você acha que recebeu tanta atenção?

**Comando:** `git log --name-only --pretty=format: | sort | uniq -c | sort -rn`

**Exemplo:**
```
      8 README.md
      1 src/transformer.py
...
```

**Resposta:**
*   **Arquivo mais modificado:** `README.md`.
*   **Quantas vezes:** 8 vezes.
*   **Por que:** É a documentação principal. Indica que a doc é bem cuidada, o projeto está ativo ou a equipe valoriza a documentação.

#### Desafio 3.2: Quem Trabalhou em Qual Arquivo?

**Pergunta:** Quem modificou o arquivo mais alterado? Essa pessoa é especialista nessa área?

**Comando:** `git log --pretty=format:"%an" -- README.md | sort | uniq -c`

**Exemplo:**
```
      8 Joás
```

**Resposta:**
*   **Quem mais trabalhou:** Joás, com 8 modificações.
*   **Especialista:** Sim, ele parece ser o responsável pela documentação.

### Pergunta 4: Como é o Fluxo de Trabalho da Equipe?

#### Desafio 4.1: Análise de Branches

**Pergunta:** Quantas branches existem no repositório? Qual é a principal branch de desenvolvimento? Existem branches de feature ou hotfix ativas?

**Comando:** `git branch -a`

**Exemplo:**
```
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```

**Resposta:**
*   **Branches:** Uma principal (`main`). As branches de feature/hotfix foram criadas e unidas, então não estão ativas agora.
*   **Principal:** `main`.
*   **Ativas:** Nenhuma feature/hotfix ativa no momento.

#### Desafio 4.2: Frequência de Merges

**Pergunta:** Com que frequência as branches são mescladas na principal? Isso indica um fluxo de trabalho contínuo ou baseado em releases?

**Comando:** `git log --oneline --merges`

**Exemplo:**
```
8bedda3 Merge branch 'main' of https://github.com/joasweslei/FinancialSense
```

**Resposta:**
*   **Frequência de merges:** Poucos merges explícitos no histórico de exemplo.
*   **Fluxo de trabalho:** Parece mais baseado em releases ou desenvolvimento centralizado, com menos integrações. Para um projeto de disciplina, é normal.

### Pergunta 5: Qual é o Padrão de Atividade do Projeto?

#### Desafio 5.1: Atividade por Data

**Pergunta:** Em qual data houve mais commits? Qual é o padrão de atividade? O projeto está em desenvolvimento ativo ou finalizado?

**Comando:** `git log --pretty=format:"%ad" --date=format:"%Y-%m-%d" | sort | uniq -c | sort -rn`

**Exemplo:**
```
     10 2024-04-21
      1 2024-04-20
```

**Resposta:**
*   **Mais commits:** 21/04/2024, com 10 commits.
*   **Padrão:** Atividade concentrada em 2 dias. Parece uma sprint intensa ou período focado.
*   **Status:** Parece finalizado ou em pausa. Todos os commits são de abril de 2024, sem atividade recente (considerando hoje, 15/06/2026).

#### Desafio 5.2: Tempo Desde o Último Commit

**Pergunta:** Quando foi o último commit? Quanto tempo se passou desde então? O que isso indica sobre o status do projeto?

**Comando:** `git log -1 --pretty=format:"%ai"`

**Exemplo:**
```
2024-04-21 12:34:56 -0300
```

**Resposta:**
*   **Último commit:** 21/04/2024, 12:34:56 (BRT).
*   **Tempo desde então:** Umas 8 semanas (até 15/06/2026).
*   **Status:** Não está ativo. Normal para um projeto de disciplina já entregue.

### Pergunta 6: Qual é a Qualidade do Histórico de Commits?

#### Desafio 6.1: Tamanho Médio dos Commits

**Pergunta:** Quantos arquivos foram modificados no total? Qual é a média de arquivos por commit? Os commits são "pequenos e focados" ou "grandes e complexos"?

**Comando:** `git log --name-only --pretty=format: | grep -v "^$" | wc -l`

**Exemplo:**
```
14
```

**Resposta:**
*   **Arquivos modificados:** 14 (contando repetições).
*   **Média por commit:** ~1,27 arquivos por commit (14 modificações / 11 commits).
*   **Tamanho:** Pequenos e focados. Ótimo para revisão e debug.

#### Desafio 6.2: Análise Qualitativa

**Pergunta:** As mensagens de commit são específicas e descritivas? Existem commits com mensagens genéricas?

**Comando:** `git log --pretty=format:"%h - %an, %ar : %s" | head -20`

**Exemplo:**
```
99d03ac - Joás, 8 weeks ago : Update analysis on inflation and family debt correlation
fc387ff - Joás, 8 weeks ago : Update README.md
...
```

**Resposta:**
*   **Mensagens:** A maioria é boa e descritiva. Ex: `Update analysis...`.
*   **Genéricas:** Sim, algumas como `Update README.md` poderiam ser mais detalhadas.
*   **Qualidade geral:** Boa. O ideal seria usar Conventional Commits sempre e evitar mensagens genéricas.

### Pergunta 7: Quais São os Indicadores de Saúde do Projeto?

#### Desafio 7.2: Recomendações de Melhoria

**Pergunta:** Quais são os pontos fortes e fracos do projeto? Que ações você recomendaria?

**Resposta:**

**3 Pontos Fortes:**

1.  **Commits Pequenos:** Facilita revisão e debug.
2.  **Mensagens Descritivas:** Ajuda a entender o histórico.
3.  **Doc Ativa (README):** Mostra que a documentação é valorizada.

**3 Pontos a Melhorar:**

1.  **Conventional Commits Inconsistente:** Dificulta automação e padronização.
2.  **Mensagens Genéricas:** Podem ser mais específicas.
3.  **Atividade Parada:** Projeto não está mais ativo (normal para projetos de disciplina).

**Ações Recomendadas:**

1.  **Forçar Conventional Commits:** Usar sempre `feat:`, `fix:`, etc.
2.  **Mensagens Mais Detalhadas:** Explicar o "porquê" da mudança.
3.  **Fluxo de Branching Melhor (se o projeto continuar):** Pensar em Git Flow ou GitHub Flow para projetos maiores.
