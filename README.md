# Anotações NoSQL

Anotações sobre NoSQL

Banco de dados não relacional entende-se errado sua sigla onde o mais correto seria Not Only SQL.

## Diferenças SQL x NoSQL

Escalabilidade:

Banco de dados relacional teria um crescimento vertical.

- Aumento da capacidade para um unico recurso
- Processador, memoria e disco rigido

Banco de dados não relacional por padrão sua estrutura seria horizontal,

sendo que na sua escalabilidade, ele particiona os dados (sharding) entre os nós é o mais conhecido. Fornecendo maior desempenho.

Schemas:

BD relacional possui suas regras de estruturas, tabelas, linhas, colunas, chaves primarias e estrangeiras.

NoSQL, não é definido regras ou padrão de estrutura, Schema-free/schemaless

Performance:

BD Relacional, SQL, depende do disco rigido, equipamento fisico, servidor.

NoSQL, depende do Cluster e da rede

Transações

SQL - ACID

Atomicidade - uma ação executa por completo ou não executa.

Consistencia - Quando executa uma ação, ele vai estar de acordo com o schema predefinido

Isolamento - Uma ação nunca vai interferir na outra

Durabilidade - Uma vez a ação concluída, o dado já estara disponivel.

NoSQL - BASE

Basically Available

Soft-State

Eventually Consistent

Prioridade e priorização de dados que não precise ser  consistente o tempo todo, e serão consistente em tempo inderterminado

Principais vantagens do NoSQL

Flexibilidade 

Escalabilidade

Alta performance

## Tipos de banco NoSQL

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccdabaa4-be8b-4661-8077-6c2b3915e786/Untitled.png)

Orientado a documento, ex. MongoDB

Orientado a chave valor, ex. Redis

Orientado a coluna, ex. Cassandra

Orientado a Grafo, ex. Neo4J

Grafos

Estruturas matematicas compostas de nos e vertices.

nos dados

vertices relacionamentos

Comum em detecção de fraudes, mecanismos de recomendação, redes sociais, sistemas de arquivos, games, etc,

# MongoDB

Caracteristicas do MongoDB 

Código aberto, alta performance, Schema-free, Utiliza JSON para armazenamento dos dados, Suporte a indices, Auto-Sharding (Escalamento horizontal), Map-Reduce, GRIDFS (Armazenamento de arquivos)

Document → Tupla/Registro

Collection → Tabela

Embedding/linking → Join

Quando usar:

Grande volume de dados

Dados não necessariamente estruturados

Quando não usar:

Necessidade de relacionamentos / joins

Propriedades ACID e transações são importantes

- Curiosidade: Diversas entidades de pagamento não homologam sistemas cujos dados financeiros dos clientes não estejam em bancos de dados relacionais tradicionais.

## Schama Design

### **Embedding**

Documentos autocontido, todas as informações que precisam estão nos documentos sem referencias.

Pros

Consulta informações em uma unica query

Atualiza o registro em uma unica operação

Contra

Limite de 16MB por documento

### **Referencias**

Documentos com dependência de outros documentos ou collections

Pros:

Documentos pequenos

Não duplica informações

Usado quando os dados não são acessados em todas as consultas

Contra

Duas ou mais queries ou utilização do $lookup

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2134f8e2-3c38-425d-b07b-9d742fa28a4d/Untitled.png)

Recomendações de acordo com os relacionamentos:

One-to-One - Prefira atributos chave-valor do documento 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f14f46b-4947-4848-ae9e-bc24dbd0d0a2/Untitled.png)

One-to-few - prefira embedding

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/647c6665-f6f6-49cf-8fc9-54d26cc67604/Untitled.png)

One-to-Many ou Many-to-Many

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e599ebb6-e4a0-483f-a4d6-ffff1e922cf6/Untitled.png)

![[https://www.mon](https://www.mongodb.com/blog/post/building-with-patterns-a-summary)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0df6a57d-5039-47a1-aedf-b936ea9bd136/Untitled.png)

[https://www.mon](https://www.mongodb.com/blog/post/building-with-patterns-a-summary)

### Boas Praticas

Evitar documentos muito grandes

Usar nome campos objetivos e curtos

Analise as suas queries utilizando explain()

Atualize apenas os campos alterados

Evite negações em queries

Listas / Arrays dentro dos documentos não podem crescer sem limites

### Diferenças BSON vs JSON

BSON

- É uma serialização codificada em binario de documentos semelhantes a JSON
- Contém extensões que permitem a representação de tipos de dados que não fazem parte da especificação JSON. Por exemplo, BSON tem um tipo Data, ObjectID

JSON

- Possui apenas tipos primitivos.

## **Operações MongoDB**

Junto aos comandos utilizados podemos usar o .explain(true) para apresentar dados mais detalhes para analisar a requisição

- $eq - Retorna os objetos que tem o valor igual ao especificado.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f827eda2-f647-4f5d-9d07-23ee6480fb4c/Untitled.png)

- também é possível criar uma variável com a query criada
    - var query = {”age”: {$eq: 20}}
        
        
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54da6a7d-67c2-476d-a054-4b787870017f/Untitled.png)
    
- $gt: Retorna os objetos que tem o valor maior ao especificado.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5392a1bb-b579-4046-a1b5-427d90bd7531/Untitled.png)

- $gte: Retorna os objetos que tem o valor maior ou igual ao especificado.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab5eafe9-4782-44db-9726-227ffbf162c5/Untitled.png)

- $it: Retorna os objetos que tem o valor menor que ao especificado.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fb2e7c7d-6e9e-4fcf-a661-e1351fd924b8/Untitled.png)

- $lte: Retorna os objetos que tem o valor menor ou igual que ao especificado

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/265a3ae2-0e84-42c7-9095-62f078bd528d/Untitled.png)

- $ne: Retorna os objetos com valor diferentes ao especificado

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43eb8118-486b-4fd7-821e-4d3cb94b27fd/Untitled.png)

- $in: Retorna os objetos que tem o valor dentre os especificados no array

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7b59445a-1658-408d-bedc-a37d904e59c6/Untitled.png)

- $nin: Retorna os objetos que não tem o valor dentre os especificados no array

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5252d3a4-9240-4a71-95c4-d55be74911eb/Untitled.png)

```sql
Exercicios

- Adicione cinco novas pessoas
- Busque todas as pessoas com idade maior que 30
- Busque todas as pessoas com idade menor ou igual a 30
- Busque todas as pessoas com idade menor que 23
- Busque todas as pessoas com idades iguais a 20,21,22,23,25
```

### Operadores Lógicos

- $or: Executa a comparação de duas expressões ou mais e retorna os objetos que cumpram com ao menos uma destas.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/59755bb7-8dc0-4d7f-a030-7fb46f8a8c13/Untitled.png)

- $and: Executa a comparação de duas expressões e retorna os objetos que cumpram todas elas, sendo que no mongo pode ser omitida apenas separando as expressões dentro do find apenas pela virgula

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef5e4784-b4ea-4355-b396-70ada864f96c/Untitled.png)

- $not: Retorna os objetos que não compreendem as expressões

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f4e700a0-f88f-4fbe-bfed-52608e478b0f/Untitled.png)

- $nor: Retorna todos os objetos que não estão de acordo com as expressões no array.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/472dd722-6534-4742-afbe-29db2d0ea171/Untitled.png)

- $exists: Junta clausulas e retorna todos os documentos que não estão de acordo

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0aee0f0a-68e1-48d5-b22d-f66453239356/Untitled.png)

- $text: Realiza busca textual no campo especificado

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ff30fae4-f2da-4a3d-840e-125cff45a943/Untitled.png)

Para o comando de pesquisa por texto, nós precisamos criar um index com o campo de texto que faremos a pesquisa.

```sql
db.pessoas.createindex({name: 1}, {"name": "nameIndex"})

Dois parametros, primeiro o campo a ser indexado e o nome do indice

```

- $search: Realiza busca  textual no campo especificado

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36bbe5bb-1e1d-4712-ac04-9233456edaf0/Untitled.png)

Para buscarmos partes de uma palavra, podemos usar o próprio find();

```sql
db.pessoas.find({"name": /G/})
```

Fazemos o pipe para separar a letra. Por padrão esta como CaseSensitive.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9e1bbe61-4355-427e-9d2e-2b3bdb1c6338/Untitled.png)

```sql
db.pessoas.find({"name": /G/i})

Assim tornamos a pesquisa como CaseInsensitive
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9bd6cccb-67ad-4bb1-9bbc-6fc4fa038cfe/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62779b5e-1191-478e-ac46-d988b147266d/Untitled.png)

## Agregações

Agregação é o procedimento de processar dados em uma ou mais etapas, onde o resultado de cada etapa é utilizado na etapa seguinte, de modo a retornar um resultado combinado.

- Agregações de pipeline onde podem ser feitas várias customizações.
- Agregações de proposito único
    
    count
    
    distinct
    

Elas não permitem as customizações das agregações utilizando pipeline

Pipelines mais básicas fornecem “filtros” e “Operadores”

$group - Usado quando planeja agrupar os dados de acordo com determinado campo

```sql
db.getCollection("collection").aggregate([{$group: {_id: "$cuisine", total: {$sum: 1}}}}])

-- primeiro parametro - id do grupo (campo que sera realizado o agrupamento)
-- segundo paramentro - acumulador, ação que sera realizado no agrupamento

```

$addFields - ele adiciona para o resultado um novo campo sem alterar a collection de origem

```sql
db.getCollection("collection").aggregate([{$addField: {"Teste": true}}])
 
-- primeiro parametro - nome do parametro
-- segundo parametro - valor desejado ao resultado
```

Funções: 

$sum - soma o conteudo do campo

$avg - media do campo que foi feito a busca

$max - o maior valor

$min - o menor valor
