# Equipe VIRUS

# Subgrupo B
* Guilhermo de Luiggi Mocelim de Oliveira - 223325
* Luiz Fernando Lima Leite - 248405
* Sara Beatriz da Silva Oliveira - 231288

## Tarefa de Cypher sobre Patologias, Medicamentos e Efeitos Colaterais

## Exercício

Faça a projeção em relação a Patologia, ou seja, conecte patologias que são tratadas pela mesma droga.

### Resolução
~~~cypher
match (p1:Pathology) <-[a]-(d:Drug)-[b]->(p2:Pathology)
where a.weight > 20 AND b.weight > 20
merge (p1)<-[r:Relates]->(p2)
on create set r.weight=1
on match set r.weight=r.weight+1

match (p1:Pathology) <-[r:Relates]->(p2:Pathology)
return p1, r, p2
~~~

# Trabalhando com Efeitos Colaterais

## Exercício

Construa um grafo ligando os medicamentos aos efeitos colaterais (com pesos associados) a partir dos registros das pessoas, ou seja, se uma pessoa usa um medicamento e ela teve um efeito colateral, o medicamento deve ser ligado ao efeito colateral.

### Resolução
~~~cypher
load csv with headers from 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' as druguse
merge (:Person {code: druguse.idperson})

create index for (p:Person) on (p:code)

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

match (d:Drug)<-[u:Used]-(pe:Person)-[co:Contracted]->(pa:Pathology)
merge (d)-[ca:Causes]->(pa)
on create set ca.weight=1
on match set ca.weight=ca.weight+1

match (a)-[c:Causes]->(b)
where c.weight > 20
return a, c, b
~~~

## Exercício

Que tipo de análise interessante pode ser feita com esse grafo?

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução

Fazemos uma nova análise dos sintomas de uma doença de forma a englobar todos os efeitos sentidos pelo paciente desde o início da enfermidade até alcançar novamente o estado são. Nessa perspectiva, surpreendentemente, percebemos que patologias podem ganhar "novos" sintomas artificialmente causados pelos remédios que as tratam. Assim, se a doença X causa febre naturalmente e é tratada frequentemente com drogas que têm como efeito colateral dor de cabeça, na prática essa enfermidade causa tanto febre quanto dor de cabeça. Temos, então, uma visão mais abrangente e real de como as doenças afetam as pessoas que aflingem

~~~cypher
match (p1:Pathology)<-[t:Treats]-(d:Drug)-[c:Causes]->(p2:Pathology)
where t.weight > 20 and c.weight > 20
merge (p1)-[x:ArtificiallyCauses]->(p2)
on create set x.weight=1
on match set x.weight=x.weight+1

match (a)-[c:ArtificiallyCauses]->(b)
return a, c, b
~~~
