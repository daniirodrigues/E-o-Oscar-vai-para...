<h1 align="center">🏆 Desafio MongoDB: Oscar Edition 🎬</h1>

<p align="center">
  <a href="https://www.mongodb.com/"><img src="https://img.shields.io/badge/Database-MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB"></a>
  <a href="#"><img src="https://img.shields.io/badge/Status-resolvendo_4/6-yellow?style=for-the-badge" alt="Status"></a>
</p>


Este repositório contém a resolução de uma série de exercícios práticos utilizando **MongoDB Query Language (MQL)**. O objetivo é explorar uma base de dados histórica sobre as indicações e vitórias do Oscar

## 🛠️ Tecnologias e Ferramentas
*   **Banco de Dados:** MongoDB (NoSQL)
*   **Interface:** MongoDB Compass / Mongosh
*   **Dataset:** Histórico de indicados ao Oscar (1928 - 2026)

## 🗺️ Guia de Consultas

<details>
<summary><h3 style="display: inline-block">📁 Nível 1: Primeiros Passos</h3></summary>
<br>

<details>
<summary><strong>🔎 1.1 Quantos registros existem na coleção de indicados ao Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments()
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 11104 registros
```

</details>
</details>
<br>

<details>
<summary><strong>🔎 1.2 Quais são as diferentes categorias de premiação que existem no banco de dados? Liste todas as categorias únicas.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("categoria").length
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 122 categorias diferentes
```

</details>
</details>
<br>

<details>
<summary><strong>🔎 1.3 Qual foi o primeiro ano de cerimônia do Oscar registrado na base?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({}, { "ano_cerimonia": 1 }).sort({ "ano_cerimonia": 1 }).limit(1)
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  _id: ObjectId('6a047a36dc0838daf8ef97be'),
  ano_cerimonia: 1928
}
```

</details>
</details>
<br>

<details>
<summary><strong>🔎 1.4 Qual foi o último ano de cerimônia registrado na base?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({}, { "ano_cerimonia": 1 }).sort({ "ano_cerimonia": -1 }).limit(1)
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  _id: ObjectId('6a04808edc0838daf8efc2c3'),
  ano_cerimonia: 2026
}
```

</details>
</details>
<br>

<details>
<summary><strong>🔎 1.5 Quantas cerimônias do Oscar estão registradas no total?</strong></summary>

💻 **Query:**
```javascript
db.oscar.distinct("cerimonia").length
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 98
```

</details>
</details>
<br>
</details>


<details>
<summary><h3 style="display: inline-block">📁 Nível 2: Explorando Categorias</h3></summary>
<br>

<details>
<summary><strong>🎬 2.1 Quantas indicações existem para cada categoria? Agrupe por categoria e ordene da mais frequente para a menos frequente.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { 
    $group: { 
      _id: "$categoria", 
      quantidade: { $sum: 1 } 
    } 
  },
  { 
    $sort: { quantidade: -1 } 
  }
]).toArray()
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
[
  { _id: 'DIRECTING', quantidade: 479 },
  { _id: 'FILM EDITING', quantidade: 460 },
  { _id: 'ACTRESS IN A SUPPORTING ROLE', quantidade: 445 },
  { _id: 'ACTOR IN A SUPPORTING ROLE', quantidade: 445 },
  { _id: 'BEST PICTURE', quantidade: 391 },
  { _id: 'DOCUMENTARY (Short Subject)', quantidade: 378 },
  { _id: 'CINEMATOGRAPHY', quantidade: 348 },
  { _id: 'DOCUMENTARY (Feature)', quantidade: 345 },
  { _id: 'FOREIGN LANGUAGE FILM', quantidade: 315 },
  { _id: 'ART DIRECTION', quantidade: 307 },
  { _id: 'COSTUME DESIGN', quantidade: 305 },
  { _id: 'MUSIC (Original Score)', quantidade: 270 },
  { _id: 'SOUND', quantidade: 255 },
  { _id: 'ACTOR IN A LEADING ROLE', quantidade: 245 },
  { _id: 'ACTRESS IN A LEADING ROLE', quantidade: 245 },
  { _id: 'ACTRESS', quantidade: 236 },
  { _id: 'MUSIC (Original Song)', quantidade: 235 },
  { _id: 'ACTOR', quantidade: 232 },
  { _id: 'SHORT FILM (Live Action)', quantidade: 226 },
  { _id: 'MUSIC (Song)', quantidade: 215 },
  { _id: 'SHORT FILM (Animated)', quantidade: 215 },
  { _id: 'SOUND RECORDING', quantidade: 195 },
  { _id: 'SHORT SUBJECT (Cartoon)', quantidade: 169 },
  { _id: 'VISUAL EFFECTS', quantidade: 165 },
  { _id: 'CINEMATOGRAPHY (Black-and-White)', quantidade: 161 },
  { _id: 'WRITING (Original Screenplay)', quantidade: 160 },
  {
    _id: 'MUSIC (Music Score of a Dramatic or Comedy Picture)',
    quantidade: 148
  },
  { _id: 'ART DIRECTION (Black-and-White)', quantidade: 138 },
  { _id: 'CINEMATOGRAPHY (Color)', quantidade: 135 },
  { _id: 'HONORARY AWARD', quantidade: 133 },
  { _id: 'MUSIC (Scoring of a Musical Picture)', quantidade: 127 },
  {
    _id: 'WRITING (Screenplay Written Directly for the Screen)',
    quantidade: 120
  },
  { _id: 'ART DIRECTION (Color)', quantidade: 112 },
  { _id: 'WRITING (Adapted Screenplay)', quantidade: 110 },
  { _id: 'WRITING (Screenplay)', quantidade: 104 },
  { _id: 'ANIMATED FEATURE FILM', quantidade: 104 },
  { _id: 'OUTSTANDING PRODUCTION', quantidade: 102 },
  {
    _id: 'WRITING (Screenplay--based on material from another medium)',
    quantidade: 95
  },
  { _id: 'SPECIAL EFFECTS', quantidade: 93 },
  { _id: 'SHORT SUBJECT (One-reel)', quantidade: 90 },
  { _id: 'BEST MOTION PICTURE', quantidade: 90 },
  { _id: 'MAKEUP', quantidade: 87 },
  { _id: 'SOUND EDITING', quantidade: 86 },
  { _id: 'SOUND MIXING', quantidade: 85 },
  { _id: 'SHORT SUBJECT (Two-reel)', quantidade: 81 },
  { _id: 'COSTUME DESIGN (Black-and-White)', quantidade: 77 },
  { _id: 'COSTUME DESIGN (Color)', quantidade: 77 },
  { _id: 'PRODUCTION DESIGN', quantidade: 70 },
  { _id: 'SHORT SUBJECT (Live Action)', quantidade: 68 },
  {
    _id: 'WRITING (Screenplay Based on Material from Another Medium)',
    quantidade: 65
  },
  { _id: 'MUSIC (Scoring)', quantidade: 64 },
  {
    _id: 'WRITING (Story and Screenplay--written directly for the screen)',
    quantidade: 60
  },
  { _id: 'SPECIAL AWARD', quantidade: 56 },
  { _id: 'MAKEUP AND HAIRSTYLING', quantidade: 56 },
  {
    _id: 'WRITING (Screenplay Based on Material Previously Produced or Published)',
    quantidade: 55
  },
  { _id: 'WRITING (Original Story)', quantidade: 52 },
  { _id: 'WRITING (Motion Picture Story)', quantidade: 50 },
  { _id: 'SOUND EFFECTS EDITING', quantidade: 47 },
  { _id: 'IRVING G. THALBERG MEMORIAL AWARD', quantidade: 45 },
  { _id: 'JEAN HERSHOLT HUMANITARIAN AWARD', quantidade: 44 },
  { _id: 'MUSIC (Original Dramatic Score)', quantidade: 41 },
  { _id: 'ASSISTANT DIRECTOR', quantidade: 35 },
  { _id: 'WRITING (Story and Screenplay)', quantidade: 35 },
  { _id: 'INTERNATIONAL FEATURE FILM', quantidade: 35 },
  {
    _id: 'MUSIC (Scoring of Music--adaptation or treatment)',
    quantidade: 30
  },
  { _id: 'OUTSTANDING MOTION PICTURE', quantidade: 30 },
  { _id: 'WRITING (Original Motion Picture Story)', quantidade: 25 },
  { _id: 'DOCUMENTARY', quantidade: 25 },
  { _id: 'MUSIC (Song--Original for the Picture)', quantidade: 25 },
  { _id: 'DANCE DIRECTION', quantidade: 21 },
  {
    _id: 'WRITING (Story and Screenplay--based on factual material or material not previously published or produced)',
    quantidade: 20
  },
  { _id: 'DOCUMENTARY FEATURE FILM', quantidade: 20 },
  { _id: 'MUSIC (Music Score of a Dramatic Picture)', quantidade: 20 },
  { _id: 'MUSIC (Original Musical or Comedy Score)', quantidade: 20 },
  { _id: 'DOCUMENTARY SHORT FILM', quantidade: 20 },
  { _id: 'MUSIC (Music Score--substantially original)', quantidade: 20 },
  { _id: 'WRITING (Adaptation)', quantidade: 17 },
  { _id: 'SPECIAL VISUAL EFFECTS', quantidade: 16 },
  { _id: 'SHORT SUBJECT (Comedy)', quantidade: 13 },
  { _id: 'SHORT SUBJECT (Novelty)', quantidade: 12 },
  { _id: 'WRITING', quantidade: 11 },
  {
    _id: 'WRITING (Screenplay Adapted from Other Material)',
    quantidade: 10
  },
  { _id: 'LIVE ACTION SHORT FILM', quantidade: 10 },
  { _id: 'MUSIC (Original Music Score)', quantidade: 10 },
  {
    _id: 'MUSIC (Score of a Musical Picture--original or adaptation)',
    quantidade: 10
  },
  {
    _id: 'WRITING (Screenplay Written Directly for the Screen--based on factual material or on story material not previously published or produced)',
    quantidade: 10
  },
  { _id: 'SOUND EFFECTS', quantidade: 10 },
  { _id: 'WRITING (ORIGINAL SCREENPLAY)', quantidade: 10 },
  { _id: 'MUSIC (ORIGINAL SONG)', quantidade: 10 },
  {
    _id: 'MUSIC (Original Score--for a motion picture [not a musical])',
    quantidade: 10
  },
  { _id: 'MUSIC (ORIGINAL SCORE)', quantidade: 10 },
  { _id: 'WRITING (ADAPTED SCREENPLAY)', quantidade: 10 },
  {
    _id: 'MUSIC (Scoring: Original Song Score and Adaptation -or- Scoring: Adaptation)',
    quantidade: 9
  },
  { _id: 'SHORT SUBJECT (Animated)', quantidade: 9 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD (Visual Effects)', quantidade: 9 },
  { _id: 'MUSIC (Original Song Score)', quantidade: 8 },
  { _id: 'OUTSTANDING PICTURE', quantidade: 8 },
  {
    _id: 'MUSIC (Scoring: Adaptation and Original Song Score)',
    quantidade: 8
  },
  {
    _id: 'MUSIC (Original Song Score and Its Adaptation -or- Adaptation Score)',
    quantidade: 6
  },
  {
    _id: 'MUSIC (Original Song Score and Its Adaptation or Adaptation Score)',
    quantidade: 6
  },
  { _id: 'SHORT SUBJECT (Color)', quantidade: 6 },
  { _id: 'ANIMATED SHORT FILM', quantidade: 5 },
  { _id: 'WRITING (Screenplay--Original)', quantidade: 5 },
  {
    _id: 'WRITING (Story and Screenplay--based on material not previously published or produced)',
    quantidade: 5
  },
  { _id: 'WRITING (Screenplay--Adapted)', quantidade: 5 },
  { _id: 'CASTING', quantidade: 5 },
  { _id: 'HONORARY FOREIGN LANGUAGE FILM AWARD', quantidade: 5 },
  {
    _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Effects Editing)',
    quantidade: 4
  },
  { _id: 'SHORT FILM (Dramatic Live Action)', quantidade: 3 },
  { _id: 'WRITING (Title Writing)', quantidade: 3 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD', quantidade: 3 },
  { _id: 'UNIQUE AND ARTISTIC PICTURE', quantidade: 3 },
  { _id: 'MUSIC (Adaptation Score)', quantidade: 3 },
  { _id: 'ENGINEERING EFFECTS', quantidade: 3 },
  { _id: 'DIRECTING (Dramatic Picture)', quantidade: 3 },
  {
    _id: 'MUSIC (Original Song Score or Adaptation Score)',
    quantidade: 3
  },
  { _id: 'DIRECTING (Comedy Picture)', quantidade: 2 },
  { _id: 'SPECIAL FOREIGN LANGUAGE FILM AWARD', quantidade: 2 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Editing)', quantidade: 1 },
  { _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Effects)', quantidade: 1 },
  { _id: 'GORDON E. SAWYER AWARD', quantidade: 1 },
  { _id: 'AWARD OF COMMENDATION', quantidade: 1 }
]
```

</details>
</details>
<br>

<details>
<summary><strong>🎬 2.2 Qual categoria teve mais indicações ao longo da história do Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { 
    $group: { 
      _id: "$categoria", 
      quantidade: { $sum: 1 } 
    } 
  },
  { 
    $sort: { quantidade: -1 }
  },
  {
    $limit: 1
  }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  _id: 'DIRECTING',
  quantidade: 479
}
```

</details>
</details>
<br>

<details>
<summary><strong>🎬 2.3 Qual categoria teve menos indicações ao longo da história?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { 
    $group: { 
      _id: "$categoria", 
      quantidade: { $sum: 1 } 
    } 
  },
  { 
    $sort: { quantidade: 1 }
  },
  {
    $limit: 1
  }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  _id: 'SPECIAL ACHIEVEMENT AWARD (Sound Effects)',
  quantidade: 1
}
```

</details>
</details>
<br>

<details>
<summary><strong>🎬 2.4 A partir de que ano a categoria "ACTRESS" deixou de existir? (Dica: procure a última cerimônia com essa categoria)</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
    {
    $match: {
      categoria: 'ACTRESS'
    }
  },
  { 
    $group: { 
      _id: "$categoria", 
      ano_cerimonia: { $max: "$ano_cerimonia" }
    } 
  },
  {
    $limit: 1
  }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  _id: 'ACTRESS',
  ano_cerimonia: 1976
}
```

</details>
</details>
<br>

<details>
<summary><strong>🎬 2.5 Quais categorias existiam na primeira cerimônia (1928) e não existem mais hoje?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("categoria", {ano_cerimonia: 1928}).filter(categoria => !db.oscar.distinct("categoria", {ano_cerimonia: 2026}).includes(categoria));
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
[
  'ACTOR',
  'ACTRESS',
  'ART DIRECTION',
  'DIRECTING (Comedy Picture)',
  'DIRECTING (Dramatic Picture)',
  'ENGINEERING EFFECTS',
  'OUTSTANDING PICTURE',
  'SPECIAL AWARD',
  'UNIQUE AND ARTISTIC PICTURE',
  'WRITING (Adaptation)',
  'WRITING (Original Story)',
  'WRITING (Title Writing)'
]
```

</details>
</details>
<br>

<details>
<summary><strong>🎬 2.6 Liste todas as categorias que contêm a palavra "DIRECTING" no nome.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("categoria").filter(categoria => categoria.includes("DIRECTING"))
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
[
  'DIRECTING',
  'DIRECTING (Comedy Picture)',
  'DIRECTING (Dramatic Picture)'
]
```

</details>
</details>
<br>
</details>

<details>
<summary><h3 style="display: inline-block">📁 Nível 3: Atores e Atrizes Famosos</h3></summary>
<br>

<details>
<summary><strong>🎭 3.1 Quantas vezes Natalie Portman foi indicada ao Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Natalie Portman"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 3 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.2 Quantos Oscars Natalie Portman ganhou?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Natalie Portman", vencedor: true})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 1 vez
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.3 Em quais anos e por quais filmes Natalie Portman foi indicada?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({nome_do_indicado: "Natalie Portman"}, {ano_cerimonia:1, nome_do_filme:1, _id:0}).toArray()
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
[
  { ano_cerimonia: 2005, nome_do_filme: 'Closer' },
  { ano_cerimonia: 2011, nome_do_filme: 'Black Swan' },
  { ano_cerimonia: 2017, nome_do_filme: 'Jackie' }
]
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.4 Liste todas as indicações de Natalie Portman mostrando: ano, categoria, filme e se venceu.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({nome_do_indicado: "Natalie Portman"}, {ano_cerimonia:1, categoria:1, nome_do_filme:1, vencedor:1, _id:0}).toArray()
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
[
  {
    ano_cerimonia: 2005,
    categoria: 'ACTRESS IN A SUPPORTING ROLE',
    nome_do_filme: 'Closer',
    vencedor: false
  },
  {
    ano_cerimonia: 2011,
    categoria: 'ACTRESS IN A LEADING ROLE',
    nome_do_filme: 'Black Swan',
    vencedor: true
  },
  {
    ano_cerimonia: 2017,
    categoria: 'ACTRESS IN A LEADING ROLE',
    nome_do_filme: 'Jackie',
    vencedor: false
  }
]
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.5 Quantas vezes Viola Davis foi indicada ao Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Viola Davis"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.6 Quantos Oscars Viola Davis ganhou?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Viola Davis", vencedor: "true"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 1 vez
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.7 Por quais filmes Viola Davis foi indicada?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({nome_do_indicado: "Viola Davis"}, {nome_do_filme:1, _id:0})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  { nome_do_filme: 'Doubt' },
  { nome_do_filme: 'The Help' },
  { nome_do_filme: 'Fences' },
  { nome_do_filme: "Ma Rainey's Black Bottom" }
}
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.8 Amy Adams já ganhou algum Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Amy Adams", vencedor: true})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: Não
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.9 Quantas vezes Amy Adams foi indicada sem ganhar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Amy Adams", vencedor: false})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 6 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.10 Denzel Washington já ganhou algum Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Denzel Washington", vencedor: true})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: Sim
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.11 Quantas vezes Denzel Washington foi indicado ao Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({nome_do_indicado: "Denzel Washington"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 9 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎭 3.12 Liste todos os Oscars que Denzel Washington ganhou (ano, categoria, filme).</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({nome_do_indicado: "Denzel Washington", vencedor: true}, {ano_cerimonia:1, categoria:1, nome_do_filme:1, _id:0})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  {
    ano_cerimonia: 1990,
    categoria: 'ACTOR IN A SUPPORTING ROLE',
    nome_do_filme: 'Glory'
  },
  {
    ano_cerimonia: 2002,
    categoria: 'ACTOR IN A LEADING ROLE',
    nome_do_filme: 'Training Day'
  }
}
```

</details>
</details>
<br>

</details>

<details>
<summary><h3 style="display: inline-block">📁 Nível 4: Vencedores Históricos 🏆</h3></summary>
<br>

<details>
<summary><strong>🏆 4.1 Quem ganhou o primeiro Oscar para Melhor Atriz (ACTRESS)?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({categoria: "ACTRESS", vencedor:true}, {nome_do_indicado:1, _id:0}).sort({ano_cerimonia:1}).limit(1)
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  nome_do_indicado: 'Janet Gaynor'
}
```

</details>
</details>
<br>

<details>
<summary><strong>🏆 4.2 Quem ganhou o primeiro Oscar para Melhor Ator (ACTOR)?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({categoria: "ACTOR", vencedor: true}, {nome_do_indicado:1, _id:0}).sort({ano_cerimonia:1}).limit(1)
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
{
  nome_do_indicado: 'Emil Jannings'
}
```

</details>
</details>
<br>

<details>
<summary><strong>🏆 4.3 Quantos vencedores existem ao todo na base de dados?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({vencedor: true})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 2464 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🏆 4.4 Liste todos os filmes que ganharam o Oscar de Melhor Filme (categoria "OUTSTANDING PICTURE" ou "BEST PICTURE").</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({categoria: {$in: ["OUTSTANDING PICTURE", "BEST PICTURE"]}, vencedor: true})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
[
  {
    _id: ObjectId('6a047a36dc0838daf8ef97fe'),
    id_registro: 65,
    ano_filmagem: 1928,
    ano_cerimonia: 1929,
    cerimonia: 2,
    categoria: 'OUTSTANDING PICTURE',
    nome_do_indicado: 'Metro-Goldwyn-Mayer',
    nome_do_filme: 'The Broadway Melody',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8ef97d3'),
    id_registro: 22,
    ano_filmagem: 1927,
    ano_cerimonia: 1928,
    cerimonia: 1,
    categoria: 'OUTSTANDING PICTURE',
    nome_do_indicado: 'Paramount Famous Lasky',
    nome_do_filme: 'Wings',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efa711'),
    id_registro: 3924,
    ano_filmagem: 1962,
    ano_cerimonia: 1963,
    cerimonia: 35,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Sam Spiegel, Producer',
    nome_do_filme: 'Lawrence of Arabia',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efa885'),
    id_registro: 4296,
    ano_filmagem: 1965,
    ano_cerimonia: 1966,
    cerimonia: 38,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Robert Wise, Producer',
    nome_do_filme: 'The Sound of Music',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efa900'),
    id_registro: 4419,
    ano_filmagem: 1966,
    ano_cerimonia: 1967,
    cerimonia: 39,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Fred Zinnemann, Producer',
    nome_do_filme: 'A Man for All Seasons',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efa80b'),
    id_registro: 4174,
    ano_filmagem: 1964,
    ano_cerimonia: 1965,
    cerimonia: 37,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Jack L. Warner, Producer',
    nome_do_filme: 'My Fair Lady',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efa78f'),
    id_registro: 4050,
    ano_filmagem: 1963,
    ano_cerimonia: 1964,
    cerimonia: 36,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Tony Richardson, Producer',
    nome_do_filme: 'Tom Jones',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efa970'),
    id_registro: 4531,
    ano_filmagem: 1967,
    ano_cerimonia: 1968,
    cerimonia: 40,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Walter Mirisch, Producer',
    nome_do_filme: 'In the Heat of the Night',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efa9db'),
    id_registro: 4638,
    ano_filmagem: 1968,
    ano_cerimonia: 1969,
    cerimonia: 41,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'John Woolf, Producer',
    nome_do_filme: 'Oliver!',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efaa48'),
    id_registro: 4747,
    ano_filmagem: 1969,
    ano_cerimonia: 1970,
    cerimonia: 42,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Jerome Hellman, Producer',
    nome_do_filme: 'Midnight Cowboy',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efab1b'),
    id_registro: 4958,
    ano_filmagem: 1971,
    ano_cerimonia: 1972,
    cerimonia: 44,
    categoria: 'BEST PICTURE',
    nome_do_indicado: "Philip D'Antoni, Producer",
    nome_do_filme: 'The French Connection',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efaab2'),
    id_registro: 4853,
    ano_filmagem: 1970,
    ano_cerimonia: 1971,
    cerimonia: 43,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Frank McCarthy, Producer',
    nome_do_filme: 'Patton',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efab83'),
    id_registro: 5062,
    ano_filmagem: 1972,
    ano_cerimonia: 1973,
    cerimonia: 45,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Albert S. Ruddy, Producer',
    nome_do_filme: 'The Godfather',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efabea'),
    id_registro: 5165,
    ano_filmagem: 1973,
    ano_cerimonia: 1974,
    cerimonia: 46,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Tony Bill, Michael Phillips and Julia Phillips, Producers',
    nome_do_filme: 'The Sting',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efac50'),
    id_registro: 5267,
    ano_filmagem: 1974,
    ano_cerimonia: 1975,
    cerimonia: 47,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Francis Ford Coppola, Producer;  Gray Frederickson and Fred Roos, Co-Producers',
    nome_do_filme: 'The Godfather Part II',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efacbd'),
    id_registro: 5376,
    ano_filmagem: 1975,
    ano_cerimonia: 1976,
    cerimonia: 48,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Saul Zaentz and Michael Douglas, Producers',
    nome_do_filme: "One Flew over the Cuckoo's Nest",
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efad27'),
    id_registro: 5482,
    ano_filmagem: 1976,
    ano_cerimonia: 1977,
    cerimonia: 49,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Irwin Winkler and Robert Chartoff, Producers',
    nome_do_filme: 'Rocky',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efad8c'),
    id_registro: 5583,
    ano_filmagem: 1977,
    ano_cerimonia: 1978,
    cerimonia: 50,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Charles H. Joffe, Producer',
    nome_do_filme: 'Annie Hall',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efadfa'),
    id_registro: 5693,
    ano_filmagem: 1978,
    ano_cerimonia: 1979,
    cerimonia: 51,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Barry Spikings, Michael Deeley, Michael Cimino and John Peverall, Producers',
    nome_do_filme: 'The Deer Hunter',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efae66'),
    id_registro: 5801,
    ano_filmagem: 1979,
    ano_cerimonia: 1980,
    cerimonia: 52,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Stanley R. Jaffe, Producer',
    nome_do_filme: 'Kramer vs. Kramer',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efaed1'),
    id_registro: 5908,
    ano_filmagem: 1980,
    ano_cerimonia: 1981,
    cerimonia: 53,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Ronald L. Schwary, Producer',
    nome_do_filme: 'Ordinary People',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb00f'),
    id_registro: 6226,
    ano_filmagem: 1983,
    ano_cerimonia: 1984,
    cerimonia: 56,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'James L. Brooks, Producer',
    nome_do_filme: 'Terms of Endearment',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb076'),
    id_registro: 6329,
    ano_filmagem: 1984,
    ano_cerimonia: 1985,
    cerimonia: 57,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Saul Zaentz, Producer',
    nome_do_filme: 'Amadeus',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efaf9f'),
    id_registro: 6114,
    ano_filmagem: 1982,
    ano_cerimonia: 1983,
    cerimonia: 55,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Richard Attenborough, Producer',
    nome_do_filme: 'Gandhi',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efaf34'),
    id_registro: 6007,
    ano_filmagem: 1981,
    ano_cerimonia: 1982,
    cerimonia: 54,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'David Puttnam, Producer',
    nome_do_filme: 'Chariots of Fire',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb0e2'),
    id_registro: 6437,
    ano_filmagem: 1985,
    ano_cerimonia: 1986,
    cerimonia: 58,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Sydney Pollack, Producer',
    nome_do_filme: 'Out of Africa',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb14f'),
    id_registro: 6546,
    ano_filmagem: 1986,
    ano_cerimonia: 1987,
    cerimonia: 59,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Arnold Kopelson, Producer',
    nome_do_filme: 'Platoon',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb21e'),
    id_registro: 6753,
    ano_filmagem: 1988,
    ano_cerimonia: 1989,
    cerimonia: 61,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Mark Johnson, Producer',
    nome_do_filme: 'Rain Man',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb1b9'),
    id_registro: 6652,
    ano_filmagem: 1987,
    ano_cerimonia: 1988,
    cerimonia: 60,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Jeremy Thomas, Producer',
    nome_do_filme: 'The Last Emperor',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb287'),
    id_registro: 6858,
    ano_filmagem: 1989,
    ano_cerimonia: 1990,
    cerimonia: 62,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Richard D. Zanuck and Lili Fini Zanuck, Producers',
    nome_do_filme: 'Driving Miss Daisy',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb2f1'),
    id_registro: 6964,
    ano_filmagem: 1990,
    ano_cerimonia: 1991,
    cerimonia: 63,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Jim Wilson and Kevin Costner, Producers',
    nome_do_filme: 'Dances With Wolves',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb360'),
    id_registro: 7075,
    ano_filmagem: 1991,
    ano_cerimonia: 1992,
    cerimonia: 64,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Edward Saxon, Kenneth Utt and Ron Bozman, Producers',
    nome_do_filme: 'The Silence of the Lambs',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb3cb'),
    id_registro: 7182,
    ano_filmagem: 1992,
    ano_cerimonia: 1993,
    cerimonia: 65,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Clint Eastwood, Producer',
    nome_do_filme: 'Unforgiven',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb439'),
    id_registro: 7292,
    ano_filmagem: 1993,
    ano_cerimonia: 1994,
    cerimonia: 66,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Steven Spielberg, Gerald R. Molen and Branko Lustig, Producers',
    nome_do_filme: "Schindler's List",
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb4a4'),
    id_registro: 7399,
    ano_filmagem: 1994,
    ano_cerimonia: 1995,
    cerimonia: 67,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Wendy Finerman, Steve Tisch and Steve Starkey, Producers',
    nome_do_filme: 'Forrest Gump',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb604'),
    id_registro: 7751,
    ano_filmagem: 1997,
    ano_cerimonia: 1998,
    cerimonia: 70,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'James Cameron and Jon Landau, Producers',
    nome_do_filme: 'Titanic',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb58d'),
    id_registro: 7632,
    ano_filmagem: 1996,
    ano_cerimonia: 1997,
    cerimonia: 69,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Saul Zaentz, Producer',
    nome_do_filme: 'The English Patient',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb6df'),
    id_registro: 7970,
    ano_filmagem: 1999,
    ano_cerimonia: 2000,
    cerimonia: 72,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Bruce Cohen and Dan Jinks, Producers',
    nome_do_filme: 'American Beauty',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb51b'),
    id_registro: 7518,
    ano_filmagem: 1995,
    ano_cerimonia: 1996,
    cerimonia: 68,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Mel Gibson, Alan Ladd, Jr. and Bruce Davey, Producers',
    nome_do_filme: 'Braveheart',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb674'),
    id_registro: 7863,
    ano_filmagem: 1998,
    ano_cerimonia: 1999,
    cerimonia: 71,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'David Parfitt, Donna Gigliotti, Harvey Weinstein, Edward Zwick and Marc Norman, Producers',
    nome_do_filme: 'Shakespeare in Love',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb7bc'),
    id_registro: 8191,
    ano_filmagem: 2001,
    ano_cerimonia: 2002,
    cerimonia: 74,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Brian Grazer and Ron Howard, Producers',
    nome_do_filme: 'A Beautiful Mind',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb82e'),
    id_registro: 8305,
    ano_filmagem: 2002,
    ano_cerimonia: 2003,
    cerimonia: 75,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Martin Richards, Producer',
    nome_do_filme: 'Chicago',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb751'),
    id_registro: 8084,
    ano_filmagem: 2000,
    ano_cerimonia: 2001,
    cerimonia: 73,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Douglas Wick, David Franzoni and Branko Lustig, Producers',
    nome_do_filme: 'Gladiator',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb89d'),
    id_registro: 8416,
    ano_filmagem: 2003,
    ano_cerimonia: 2004,
    cerimonia: 76,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Barrie M. Osborne, Peter Jackson and Fran Walsh, Producers',
    nome_do_filme: 'The Lord of the Rings: The Return of the King',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb9ee'),
    id_registro: 8753,
    ano_filmagem: 2006,
    ano_cerimonia: 2007,
    cerimonia: 79,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Graham King, Producer',
    nome_do_filme: 'The Departed',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb910'),
    id_registro: 8531,
    ano_filmagem: 2004,
    ano_cerimonia: 2005,
    cerimonia: 77,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Clint Eastwood, Albert S. Ruddy and Tom Rosenberg, Producers',
    nome_do_filme: 'Million Dollar Baby',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efb97f'),
    id_registro: 8642,
    ano_filmagem: 2005,
    ano_cerimonia: 2006,
    cerimonia: 78,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Paul Haggis and Cathy Schulman, Producers',
    nome_do_filme: 'Crash',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efba63'),
    id_registro: 8870,
    ano_filmagem: 2007,
    ano_cerimonia: 2008,
    cerimonia: 80,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Scott Rudin, Ethan Coen and Joel Coen, Producers',
    nome_do_filme: 'No Country for Old Men',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbad4'),
    id_registro: 8983,
    ano_filmagem: 2008,
    ano_cerimonia: 2009,
    cerimonia: 81,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Christian Colson, Producer',
    nome_do_filme: 'Slumdog Millionaire',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbbc3'),
    id_registro: 9222,
    ano_filmagem: 2010,
    ano_cerimonia: 2011,
    cerimonia: 83,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Iain Canning, Emile Sherman and Gareth Unwin, Producers',
    nome_do_filme: "The King's Speech",
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbcb4'),
    id_registro: 9463,
    ano_filmagem: 2012,
    ano_cerimonia: 2013,
    cerimonia: 85,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Grant Heslov, Ben Affleck and George Clooney, Producers',
    nome_do_filme: 'Argo',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbc3b'),
    id_registro: 9342,
    ano_filmagem: 2011,
    ano_cerimonia: 2012,
    cerimonia: 84,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Thomas Langmann, Producer',
    nome_do_filme: 'The Artist',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbb49'),
    id_registro: 9100,
    ano_filmagem: 2009,
    ano_cerimonia: 2010,
    cerimonia: 82,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Kathryn Bigelow, Mark Boal, Nicolas Chartier and Greg Shapiro, Producers',
    nome_do_filme: 'The Hurt Locker',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbdb0'),
    id_registro: 9715,
    ano_filmagem: 2014,
    ano_cerimonia: 2015,
    cerimonia: 87,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Alejandro G. Iñárritu, John Lesher and James W. Skotchdopole, Producers',
    nome_do_filme: 'Birdman or (The Unexpected Virtue of Ignorance)',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbeb0'),
    id_registro: 9971,
    ano_filmagem: 2016,
    ano_cerimonia: 2017,
    cerimonia: 89,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Adele Romanski, Dede Gardner and Jeremy Kleiner, Producers',
    nome_do_filme: 'Moonlight',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbd38'),
    id_registro: 9595,
    ano_filmagem: 2013,
    ano_cerimonia: 2014,
    cerimonia: 86,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Brad Pitt, Dede Gardner, Jeremy Kleiner, Steve McQueen and Anthony Katagas, Producers',
    nome_do_filme: '12 Years a Slave',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbe33'),
    id_registro: 9846,
    ano_filmagem: 2015,
    ano_cerimonia: 2016,
    cerimonia: 88,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Michael Sugar, Steve Golin, Nicole Rocklin and Blye Pagon Faust, Producers',
    nome_do_filme: 'Spotlight',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbfa9'),
    id_registro: 10220,
    ano_filmagem: 2018,
    ano_cerimonia: 2019,
    cerimonia: 91,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Jim Burke, Charles B. Wessler, Brian Currie, Peter Farrelly and Nick Vallelonga, Producers',
    nome_do_filme: 'Green Book',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efc02c'),
    id_registro: 10351,
    ano_filmagem: 2019,
    ano_cerimonia: 2020,
    cerimonia: 92,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Kwak Sin Ae and Bong Joon Ho, Producers',
    nome_do_filme: 'Parasite',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efc0a8'),
    id_registro: 10475,
    ano_filmagem: 2020,
    ano_cerimonia: 2021,
    cerimonia: 93,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Frances McDormand, Peter Spears, Mollye Asher, Dan Janvey and Chloé Zhao, Producers',
    nome_do_filme: 'Nomadland',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efbf2d'),
    id_registro: 10096,
    ano_filmagem: 2017,
    ano_cerimonia: 2018,
    cerimonia: 90,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Guillermo del Toro and J. Miles Dale, Producers',
    nome_do_filme: 'The Shape of Water',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efc11d'),
    id_registro: 10592,
    ano_filmagem: 2021,
    ano_cerimonia: 2022,
    cerimonia: 94,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Philippe Rousselet, Fabrice Gianfermi and Patrick Wachsberger, Producers',
    nome_do_filme: 'CODA',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efc19c'),
    id_registro: 10719,
    ano_filmagem: 2022,
    ano_cerimonia: 2023,
    cerimonia: 95,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Daniel Kwan, Daniel Scheinert and Jonathan Wang, Producers',
    nome_do_filme: 'Everything Everywhere All at Once',
    vencedor: true
  },
  {
    _id: ObjectId('6a047a36dc0838daf8efc21c'),
    id_registro: 10847,
    ano_filmagem: 2023,
    ano_cerimonia: 2024,
    cerimonia: 96,
    categoria: 'BEST PICTURE',
    nome_do_indicado: 'Emma Thomas, Charles Roven and Christopher Nolan, Producers',
    nome_do_filme: 'Oppenheimer',
    vencedor: true
  }
]
```

</details>
</details>
<br>

<details>
<summary><strong>🏆 4.5 Quantos filmes diferentes já ganharam o Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("nome_do_filme").length
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 5130 vezes
```

</details>
</details>
<br>
</details>

<details>
<summary><h3 style="display: inline-block">📁 Nível 5: Análise de Indicações 📊</h3></summary>
<br>

<details>
<summary><strong>📊 5.1 Quais atores/atrizes foram indicados mais de uma vez? Liste o nome e o número de indicações.</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { $group: { _id: "$nome_do_indicado", count: { $sum: 1 } } },
  { $match: { count: { $gt: 1 } } },
  { $sort: { count: -1 } }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>📊 5.2 Qual ator ou atriz tem o maior número de indicações na história do Oscar?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { $group: { _id: "$nome_do_indicado", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 1 }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>📊 5.3 Quais atores foram indicados mais de 3 vezes, mas nunca ganharam?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { $group: { _id: "$nome_do_indicado", total: { $sum: 1 }, wins: { $sum: { $cond: [{ $eq: ["$vencedor", "true"] }, 1, 0] } } } },
  { $match: { total: { $gt: 3 }, wins: 0 } }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>📊 5.4 Encontre todos os artistas que foram indicados em categorias diferentes (ex: ator e diretor).</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { $group: { _id: "$nome_do_indicado", categorias: { $addToSet: "$categoria" } } },
  { $match: { $expr: { $gt: [{ $size: "$categorias" }, 1] } } }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>📊 5.5 Quantos indicados têm exatamente 1 indicação na história?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { $group: { _id: "$nome_do_indicado", count: { $sum: 1 } } },
  { $match: { count: 1 } },
  { $count: "total" }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>📊 5.6 Qual o maior número de indicados em um único ano? (Considerar total de documentos por ano.)</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.aggregate([
  { $group: { _id: "$ano_cerimonia", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 1 }
])
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>
</details>

<details>
<summary><h3 style="display: inline-block">📁 Nível 6: Análise de Filmes 🎥</h3></summary>
<br>

<details>
<summary><strong>🎥 6.1 A série de filmes Toy Story ganhou Oscars em quais anos?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({filme: /Toy Story/i, vencedor: "true"}, {ano_cerimonia:1, _id:0})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 6.2 Quantas indicações a franquia Toy Story recebeu no total?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({filme: /Toy Story/i})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 6.3 Em quais categorias os filmes Toy Story foram indicados?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.distinct("categoria", {filme: /Toy Story/i})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 6.4 Em qual edição do Oscar o filme "Crash" concorreu?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.find({filme: "Crash"}, {ano_cerimonia:1, _id:0})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 6.5 Quantas indicações o filme "Crash" recebeu?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({filme: "Crash"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 6.6 "Crash" ganhou o Oscar de Melhor Filme?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.findOne({filme: "Crash", categoria: {$in: ["OUTSTANDING PICTURE", "BEST PICTURE"]}, vencedor: "true"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 6.7 O filme "Central do Brasil" aparece no banco de dados?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.findOne({filme: "Central do Brasil"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>

<details>
<summary><strong>🎥 6.8 Se sim, quantas indicações "Central do Brasil" recebeu?</strong></summary>
<br>

💻 **Query:**
```javascript
db.oscar.countDocuments({filme: "Central do Brasil"})
```

<details>
<summary><strong>Ver Resposta</strong></summary>
<br>

```json
R: 4 vezes
```

</details>
</details>
<br>
</details>
<br>