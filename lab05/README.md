# Modelo para Apresentação do Lab05 - Marcadores e Taxonomia em Cypher

Estrutura de pastas:

~~~
├── README.md  <- arquivo apresentando a tarefa
~~~

# Aluno
* `206457`: `Victor Agozzini Scholze`

## Tarefa de Cypher sobre Marcadores e Taxonomia

## Tarefa 1

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, sem considerar as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador)-[r:Pertence]->(c:Categoria {id:"Serviços"})
RETURN m
~~~

## Tarefa 2

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, considerando as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador)
WHERE EXISTS {
  MATCH (m)-[:Pertence]->(c1:Categoria)
  WHERE EXISTS {
    MATCH (c1)-[:Superior*0..4]->(c2:Categoria)
    WHERE c2.id = 'Serviços'
  }
}
RETURN m
~~~
