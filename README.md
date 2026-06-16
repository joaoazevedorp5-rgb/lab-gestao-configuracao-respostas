Pergunta: O que acontece com o arquivo alterado quando ocorre o merge de uma branch para a branch principal, considerando que a sua versão anterior está disponível na principal?
Resposta: Quando você junta uma branch na main, o Git tenta unir as mudanças. Se não tiver conflito, ele faz a união. A main vai ter as mudanças da outra branch. A versão antiga da main fica no histórico, mas o arquivo atual na main mostra as novidades. Se der conflito, o Git para e você tem que arrumar na mão antes de finalizar.

Pergunta: Quem é o contribuidor número 1 do projeto? Qual é a distribuição de commits entre os membros da equipe?
Resposta:
Top Contribuidor: Bily, com 9 commits.
Distribuição: Bem concentrada no Bily. Isso pode significar que ele é o principal dev ou que a equipe é pequena. Talvez outros precisem se envolver mais.

Pergunta: Quantas pessoas diferentes trabalharam no projeto nas últimas 2 semanas? Quem foi o mais ativo nesse período?
Resposta:
Pessoas nas últimas 2 semanas: 0. Sem atividade recente. Isso mostra que o projeto está parado ou finalizado.
Mais ativo: Ninguém, sem atividade recente.

Pergunta: O projeto segue o padrão de Conventional Commits? As mensagens são descritivas e claras?
Resposta:
Padrão Conventional Commits: Só parcialmente. Tem um feat: mas a maioria não segue. Ex: Update README.md não segue.
Tipo mais comum: Atualizações de README.
Mensagens: Geralmente claras, mas poderiam ser mais padronizadas.

Pergunta: Qual é o tipo de commit mais comum no projeto? Existe algum tipo que não deveria estar no histórico? Qual é a sua recomendação para melhorar o padrão de commits?
Resposta:
Tipo mais comum: Apenas 1 feat: explícito. A maioria não tem prefixo.
Commits "ruins": Não, mas são inconsistentes. Muitos Update README.md poderiam ser docs: update README.
Recomendação: Usar Conventional Commits sempre (feat:, fix:, docs:, etc.) e ser mais específico nas mensagens.

Pergunta: Qual é o arquivo mais modificado do projeto? Quantas vezes foi alterado? Por que você acha que recebeu tanta atenção?
Resposta:
Arquivo mais modificado: README.md.
Quantas vezes: 8 vezes.
Por que: É a documentação principal. Indica que a doc é bem cuidada, o projeto está ativo ou a equipe valoriza a documentação.

Pergunta: Quem modificou o arquivo mais alterado? Essa pessoa é especialista nessa área?
Resposta:
Quem mais trabalhou: Joás, com 8 modificações.
Especialista: Sim, ele parece ser o responsável pela documentação.

Pergunta: Quantas branches existem no repositório? Qual é a principal branch de desenvolvimento? Existem branches de feature ou hotfix ativas?
Resposta:
Branches: Uma principal (main). As branches de feature/hotfix foram criadas e unidas, então não estão ativas agora.
Principal: main.
Ativas: Nenhuma feature/hotfix ativa no momento.

Pergunta: Com que frequência as branches são mescladas na principal? Isso indica um fluxo de trabalho contínuo ou baseado em releases?
Resposta:
Frequência de merges: Poucos merges explícitos no histórico de exemplo.
Fluxo de trabalho: Parece mais baseado em releases ou desenvolvimento centralizado, com menos integrações. Para um projeto de disciplina, é normal.

Pergunta: Em qual data houve mais commits? Qual é o padrão de atividade? O projeto está em desenvolvimento ativo ou finalizado?
Resposta:
Mais commits: 21/04/2024, com 10 commits.
Padrão: Atividade concentrada em 2 dias. Parece uma sprint intensa ou período focado.
Status: Parece finalizado ou em pausa. Todos os commits são de abril de 2024, sem atividade recente.

Pergunta: Quando foi o último commit? Quanto tempo se passou desde então? O que isso indica sobre o status do projeto?
Resposta:
Último commit: 21/04/2024, 12:34:56 (BRT).
Tempo desde então: Umas 8 semanas (até 15/06/2026).
Status: Não está ativo. Normal para um projeto de disciplina já entregue.

Pergunta: Quantos arquivos foram modificados no total? Qual é a média de arquivos por commit? Os commits são "pequenos e focados" ou "grandes e complexos"?
Resposta:
Arquivos modificados: 14 (contando repetições).
Média por commit: ~1,27 arquivos por commit.
Tamanho: Pequenos e focados. Ótimo para revisão e debug.

Pergunta: As mensagens de commit são específicas e descritivas? Existem commits com mensagens genéricas?
Resposta:
Mensagens: A maioria é boa e descritiva. Ex: Update analysis....
Genéricas: Sim, algumas como Update README.md poderiam ser mais detalhadas.
Qualidade geral: Boa. O ideal seria usar Conventional Commits sempre e evitar mensagens genéricas.

Pergunta: Quais são os pontos fortes e fracos do projeto? Que ações você recomendaria?
Resposta:

3 Pontos Fortes:
1. Commits Pequenos: Facilita revisão e debug.
2. Mensagens Descritivas: Ajuda a entender o histórico.
3. Doc Ativa (README): Mostra que a documentação é valorizada.

3 Pontos a Melhorar:
1. Conventional Commits Inconsistente: Dificulta automação e padronização.
2. Mensagens Genéricas: Podem ser mais específicas.
3. Atividade Parada: Projeto não está mais ativo (normal para projetos de disciplina).

Ações Recomendadas:
1. Forçar Conventional Commits: Usar sempre feat:, fix:, etc.
2. Mensagens Mais Detalhadas: Explicar o "porquê" da mudança.
3. Fluxo de Branching Melhor (se o projeto continuar): Pensar em Git Flow ou GitHub Flow para projetos maiores.
