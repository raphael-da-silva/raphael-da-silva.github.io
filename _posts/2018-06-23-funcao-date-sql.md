---
layout: post
title: SQL - Comparando de campos de data descartando a hora
date: 2018-06-23 14:39
---

Em uma determinada situação precisei comparar as datas em uma busca, entretanto os resultados obtidos não eram os esperados. Depois de tentar descobrir o problema, percebi que a hora estava influenciando na busca, já que o tipo do campo era datetime. Consegui resolver o problema com a função DATE do MySQL, que serve para pegar somente a data sem a hora do jeito que eu precisava, pois no caso era utilizado apenas o dia, mês e ano para fazer a busca.

```sql
#
# Comparação de data quando o campo é datetime.
# É necessário utilizar a função DATE para pegar apenas a data (sem horário).
#
SELECT * FROM news 
WHERE DATE(CreationDate) >= '2018-06-23'
AND DATE(CreationDate) <= '2018-06-23'
ORDER BY CreationDate DESC
```

### Escrevendo para fixar

Esse post veio de bug de tive em um projeto, portanto achei válido escrever para fixar na mente o que aconteceu e lembrar mais facilmente depois.