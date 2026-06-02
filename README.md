# Oscar - Exercícios MongoDB Respostas

Nome do aluno: **Daniel Rodrigues da Silva**

## Avaliação

**Objetivo de aprendizado**: Ao completar todos os níveis, você será capaz de trabalhar com bases de dados históricas complexas, realizar análises estatísticas sofisticadas e extrair insights valiosos de grandes volumes de dados.

---

## Nível 1: Primeiros Passos

### Conhecendo a Base de Dados

**1.1** Quantos registros existem na coleção de indicados ao Oscar?

R: 10889 registros
```
db.registros.countDocuments();
```
\
**1.2** Quais são as diferentes categorias de premiação que existem no banco de dados? Liste todas as categorias únicas.

R: 92 registros
```
db.oscar_indicados.distinct("categoria");
```
\
**1.3** Qual foi o primeiro ano de cerimônia do Oscar registrado na base?

R: 1928
Exemplo de resposta:
```
db.registros.findOne ();
```
\
**1.4** Qual foi o último ano de cerimônia registrado na base?

R: 2024
```
db.registros.find().sort({ _id: -1 }).limit(1);
```
    o ".sort" organiza os dados em uma ordem e o "-1" garante que essa ordem será do maior (mais recente) para o menor (mais antigo), e o "_id" diz para ele deixar em primeiro o id de maior valor, que consequentemente é o mais recente.
\
**1.5** Quantas cerimônias do Oscar estão registradas no total?

R: 96
```
db.registros.distinct("ano_cerimonia").length
```
\
**1.6** Atualize os registros da tabela com os dados do Oscar 2025 e 2026 (pesquise os vencedores e adicione-os).
```
"Concluído"
```
---

## Nível 2: Explorando Categorias

**2.1** Quantas indicações existem para cada categoria? Agrupe por categoria e ordene da mais frequente para a menos frequente.

R: A com mais indicações é 'DIRECTING', com o total: 479 indicados\
E com menos indicação é 'AWARD OF COMMENDATION', com total: 1 indicação


```
db.registros.aggregate([
  {
    $group: {
      _id: "$categoria",
      total: {$sum: 1}
    }
  },
  { $sort: {total : -1} }
])
```
\
**2.2** Qual categoria teve mais indicações ao longo da história do Oscar?

R: A com mais indicações é 'DIRECTING', com o total: 479 indicados
```
db.registros.aggregate([
  {
    $group: {
      _id: "$categoria",
      total: {$sum: 1}
    }
  },
  { $sort: {total : -1} }
])
```
\
**2.3** Qual categoria teve menos indicações ao longo da história?

R: E com menos indicação é 'AWARD OF COMMENDATION', com total: 1 indicação
```
db.registros.aggregate([
  {
    $group: {
      _id: "$categoria",
      total: {$sum: 1}
    }
  },
  { $sort: {total : 1} }
])
```
\
**2.4** A partir de que ano a categoria "ACTRESS" deixou de existir? (Dica: procure a última cerimônia com essa categoria)

R: 1976
```
db.registros.find({ "categoria": "ACTRESS" }).sort({ "ano_cerimonia": -1 }).limit(1)
```
\
**2.5** Quais categorias existiam na primeira cerimônia (1928) e não existem mais hoje?

R: OUTSTANDING PICTURE e ART DIRECTION
```
db.registros.distinct("categoria", { "ano_cerimonia": 2026 }); 

db.registros.distinct("categoria", { "ano_cerimonia": 1929 });
```
\
**2.6** Liste todas as categorias que contêm a palavra "DIRECTING" no nome.

R: 'DIRECTING',
'DIRECTING (Comedy Picture)',
'DIRECTING (Dramatic Picture)'
```
db.registros.distinct("categoria", { "categoria": /DIRECTING/ })
```

---

## Nível 3: Atores e Atrizes Famosos

### Natalie Portman

**3.1** Quantas vezes Natalie Portman foi indicada ao Oscar?

R:  3 vezes
```
db.registros.countDocuments({ "nome_do_indicado": /Natalie Portman/ })
```
\
**3.2** Quantos Oscars Natalie Portman ganhou?

R: Uma vez
```
db.registros.countDocuments({ 
  "nome_do_indicado": /Natalie Portman/, 
  "vencedor": "true" 
})
```
\
**3.3** Em quais anos e por quais filmes Natalie Portman foi indicada?

R: 'Closer' (2005); 'Black Swan'(2011); 'Jackie'(2017)
```
db.registros.find(
  { "nome_do_indicado": /Natalie Portman/ },
  { "ano_cerimonia": 1, "nome_do_filme": 1, "categoria": 1, "_id": 0 }
```
\
**3.4** Liste todas as indicações de Natalie Portman mostrando: ano, categoria, filme e se venceu.

```
{ "nome_do_indicado": /Natalie Portman/ },
  { "ano_cerimonia": 1, "categoria": 1, "nome_do_filme": 1, "vencedor": 1, "_id": 0 }
```

### Viola Davis

**3.5** Quantas vezes Viola Davis foi indicada ao Oscar?

R: 4 vezes
```
db.registros.countDocuments({ "nome_do_indicado": /Viola Davis/ })
```
\
**3.6** Quantos Oscars Viola Davis ganhou?

R: Uma vez
```
db.registros.countDocuments({ 
  "nome_do_indicado": /Viola Davis/, 
  "vencedor": "true"
```
\
**3.7** Por quais filmes Viola Davis foi indicada?

R: Doubt; The Help; Fences; Ma Rainey's Black Bottom.
```
db.registros.find(
  { "nome_do_indicado": /Viola Davis/ },
  { "ano_cerimonia": 1, "nome_do_filme": 1, "categoria": 1, "_id": 0 }
```
### Amy Adams

**3.8** Amy Adams já ganhou algum Oscar?

R: Não
```
db.registros.find(
  { "nome_do_indicado": /Amy Adams/ },
  { "vencedor": true }
```
\
**3.9** Quantas vezes Amy Adams foi indicada sem ganhar?

R: 6 vezes
```
db.registros.countDocuments({ 
  "nome_do_indicado": /Amy Adams/,
```

### Denzel Washington

**3.10** Denzel Washington já ganhou algum Oscar?

R: Sim
```
db.registros.countDocuments({ 
  "nome_do_indicado": /Denzel Washington/, 
  "vencedor": "true" 
})
```
\
**3.11** Quantas vezes Denzel Washington foi indicado ao Oscar?

R: 10 vezes
```
db.registros.countDocuments({ "nome_do_indicado": /Denzel Washington/ })
```
\
**3.12** Liste todos os Oscars que Denzel Washington ganhou (ano, categoria, filme).
```
db.registros.find(
  { "nome_do_indicado": /Denzel Washington/, "vencedor": "true" },
  { "ano_cerimonia": 1, "nome_do_filme": 1, "categoria": 1, "_id": 0 })
```
---

## Nível 4: Vencedores Históricos

**4.1** Quem ganhou o primeiro Oscar para Melhor Atriz (ACTRESS)? Em que ano e por qual filme?

R: 'Janet Gaynor'
```
db.registros.findOne(
  { "categoria": "ACTRESS", "vencedor": "true" },
  { "ano_cerimonia": 1, "nome_do_indicado": 1, "nome_do_filme": 1, "_id": 0 },
  { sort: { "ano_cerimonia": 1 } }
)
```
\
**4.2** Quem ganhou o primeiro Oscar para Melhor Ator (ACTOR)? Em que ano e por qual filme?

R: 'Emil Jannings'
```
db.registros.findOne(
  { "categoria": "ACTOR", "vencedor": "true" },
  { "ano_cerimonia": 1, "nome_do_indicado": 1, "nome_do_filme": 1, "_id": 0 },
  { sort: { "ano_cerimonia": 1 } }
)
```
\
**4.3** Quantos vencedores existem ao todo na base de dados?

R: 2513 registros
```
db.registros.countDocuments({ "vencedor": "true" })
```
\
**4.4** Liste todos os filmes que ganharam o Oscar de Melhor Filme (categoria "OUTSTANDING PICTURE" ou "BEST PICTURE").

```
db.registros.distinct("nome_do_filme", {
  "categoria": { "$in": ["OUTSTANDING PICTURE", "BEST PICTURE"] },
  "vencedor": "true"
})
```
\
**4.5** Quantos filmes diferentes já ganharam o Oscar?

R: 1358
```
db.registros.aggregate([
  { "$match": { "vencedor": "true" } },
  { "$group": { "_id": "$nome_do_filme" } },
  { "$count": "total_filmes_vencedores" }
])
```
---

## Nível 5: Análise de Indicações

**5.1** Quais atores/atrizes foram indicados mais de uma vez? Liste o nome e o número de indicações.

R:
```
db.registros.aggregate([
  { "$group": { "_id": "$nome_do_indicado", "total_indicacoes": { "$sum": 1 } } },
  { "$match": { "total_indicacoes": { "$gt": 1 } } },
  { "$sort": { "total_indicacoes": -1 } }
])
```
\
**5.2** Qual ator ou atriz tem o maior número de indicações na história do Oscar?

R: 'Metro-Goldwyn-Mayer' com 64 indicações
```
([
  {"$group": { "_id": "$nome_do_indicado","total_indicacoes": { "$sum": 1 } } },
  { "$sort": { "total_indicacoes": -1 } },
  { "$limit": 1}
])
```
\
**5.3** Quais atores foram indicados mais de 3 vezes mas nunca ganharam?

```
db.registros.aggregate([
  { "$group": {
      "_id": "$nome_do_indicado",
      "total_indicacoes": { "$sum": 1 },
      "vitorias": { "$sum": { "$cond": [{ "$eq": ["$vencedor", "true"] }, 1, 0] } } } },
  { "$match": {
      "total_indicacoes": { "$gt": 3 },
      "vitorias": 0 } },
  { "$sort": { "total_indicacoes": -1 } }
])
```
\
**5.4** Encontre todos os artistas que foram indicados em categorias diferentes (ex: ator e diretor).

R: Metro-Goldwyn-Mayer, Alex North, Walt Disney e mais
```
db.registros.aggregate([
  { "$group": {
      "_id": "$nome_do_indicado",
      "categorias_distintas": { "$addToSet": "$categoria" } } },
  { "$project": {
      "_id": 1,
      "categorias_distintas": 1,
      "total_categorias": { "$size": "$categorias_distintas" } } },
  { "$match": {
      "total_categorias": { "$gt": 1 } } },
  { "$sort": { "total_categorias": -1 } }
])
```
\
**5.5** Quantos indicados têm exatamente 1 indicação na história?

R: 5750 indicados
```
db.registros.aggregate([
  { "$group": {
      "_id": "$nome_do_indicado",
      "total_indicacoes": { "$sum": 1 } } },
  { "$match": { "total_indicacoes": 1 } },
  { "$count": "total_artistas_com_uma_indicacao" }
])
```
\
**5.6** Qual o maior números de indicados em um único ano? Essa é uma pergunta franca.  

R: 1943 com 186 indicações.
```
db.registros.aggregate([
  { "$group": { 
      "_id": "$ano_cerimonia", 
      "total_indicados": { "$sum": 1 } } },
  { "$sort": { "total_indicados": -1 } },
  { "$limit": 1 }
])
```
---

## Nível 6: Análise de Filmes

### Toy Story

**6.1** A série de filmes Toy Story ganhou Oscars em quais anos?


R: Toy Sotry 3 (2011) e Toy Story 4 (2020)
```
db.registros.find(
  { 
    "nome_do_filme": /Toy Story/, 
    "vencedor": "true" 
  },
  { "ano_cerimonia": 1, "nome_do_filme": 1, "categoria": 1, "_id": 0 }
).sort({ "ano_cerimonia": 1 })
```
\
**6.2** Quantas indicações a franquia Toy Story recebeu no total?

R: 11
```
db.registros.countDocuments({ "nome_do_filme": /Toy Story/ })
```
\
**6.3** Em quais categorias os filmes Toy Story foram indicados?

R: 
'ANIMATED FEATURE FILM',
'BEST PICTURE',

'MUSIC (Original Musical or Comedy Score)',

'MUSIC (Original Song)',

'SOUND EDITING',

'WRITING (Adapted Screenplay)',

'WRITING (Screenplay Written Directly for the Screen)'
```
db.registros.distinct("categoria", { "nome_do_filme": /Toy Story/ })
```

### Crash


**6.4** Em qual edição do Oscar o filme "Crash" concorreu?

R: Cerimonia 78 (2006)
```
db.registros.findOne(
  { "nome_do_filme": "Crash" },
  { "ano_cerimonia": 1, "cerimonia": 1, "_id": 0 }
)
```
\
**6.5** Quantas indicações o filme "Crash" recebeu?

R: 6 indicações
```
db.registros.countDocuments({ "nome_do_filme": "Crash" })
```
\
**6.6** "Crash" ganhou o Oscar de Melhor Filme?

R: Sim
```
db.registros.find({
  "nome_do_filme": "Crash",
  "categoria": "BEST PICTURE",
  "vencedor": "true"
})
```
### Central do Brasil

**6.7** O filme "Central do Brasil" aparece no banco de dados?

R: Não aparece
```
db.registros.find({ "nome_do_filme": "Central do Brasil" })
```
\
**6.8** Se sim, quantas indicações "Central do Brasil" recebeu?

R: O filme não aparece, porém, tiveram 2 indicações.
```
db.registros.insertMany([
  {
    "ano_filmagem": 1998,
    "ano_cerimonia": 1999,
    "cerimonia": 71,
    "categoria": "FOREIGN LANGUAGE FILM",
    "nome_do_indicado": "Brazil",
    "nome_do_filme": "Central Station",
    "vencedor": "false"
  },
  {
    "ano_filmagem": 1998,
    "ano_cerimonia": 1999,
    "cerimonia": 71,
    "categoria": "ACTRESS IN A LEADING ROLE",
    "nome_do_indicado": "Fernanda Montenegro",
    "nome_do_filme": "Central Station",
    "vencedor": "false"
  }
])
```

---
