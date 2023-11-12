# Comandos Avançados em Cypher

## Exercício

Faça a projeção em relação a Patologia, ou seja, conecte patologias que são tratadas pela mesma droga.

### Resolução
~~~cypher
match (p1:Pathology) <-[a]-(d:Drug)-[b]->(p2:Pathology)
where a.weight > 20 AND b.weight > 20
merge (p1)<-[r:Relates]->(p2)
on create set r.weight=1
on match set r.weight=r.weight+1
~~~

# Trabalhando com Efeitos Colaterais

## Exercício

Construa um grafo ligando os medicamentos aos efeitos colaterais (com pesos associados) a partir dos registros das pessoas, ou seja, se uma pessoa usa um medicamento e ela teve um efeito colateral, o medicamento deve ser ligado ao efeito colateral.

### Resolução
~~~cypher
load csv with headers from 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' as druguse
match (d:Drug {code: druguse.codedrug})
match (p:Person {code: druguse.idperson})
merge (p)-[u:Used]->(d)
on create set u.weight=1
on match set u.weight=u.weight+1

load csv with headers from 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' as sideeffect
match (pe:Person {code: sideeffect.idPerson})
match (pa:Pathology {code: sideeffect.codePathology})
merge (pe)-[c:Contracted]->(pa)
on create set c.weight=1
on match set c.weight=c.weight+1

match (d:Drug)<-[u:Used]-(pe:Person)-[c:Contracted]->(pa:Pathology)
merge (d)-[c:Causes]->(pa)
on create set c.weight=1
on match set c.weight=c.weight+1

match (a)-[c:Causes]->(b)
where c.weight > 20
return a, b
~~~

## Exercício

Que tipo de análise interessante pode ser feita com esse grafo?

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução
~~~cypher
(escreva aqui a resolução em Cypher)
~~~