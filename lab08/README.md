# Equipe VIRUS

# Subgrupo B
* Guilhermo de Luiggi Mocelim de Oliveira - 223325
* Luiz Fernando Lima Leite - 248405
* Sara Beatriz da Silva Oliveira - 231288


## Análise de Redes em Bancos de Dados em Grafos

### Suponha que um indivíduo goste de uma Receita A. Quais outras Receitas podemos recomendar a ele?
Podemos recomendar uma Receita similar à Raceita A.
Seria necessário criar uma projeção do grafo onde vértices de Receita se relacionam baseado no número de ingredientes em comum.
A partir disso, podemos organizar uma comunidade de Receitas na qual a Receita A faz parte, e então recomendar receitas dessa comunidade.

### Quais são os ingredientes essenciais para a criação de receitas?
Podemos criar uma projeção do grafo onde ingredientes se relacionam baseado no número de receitas. Assim, podemos avaliar a vulnerabilidade de cada ingrediente. Os vértices mais vulneráveis da nossa rede podem ser considerados essenciais para criar receitas.