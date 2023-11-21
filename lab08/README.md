# Equipe VIRUS

# Subgrupo B
* Guilhermo de Luiggi Mocelim de Oliveira - 223325
* Luiz Fernando Lima Leite - 248405
* Sara Beatriz da Silva Oliveira - 231288

## Modelo Lógico do Banco de Dados de Grafos
![Modelo Lógico de Grafos](images/modelo-logico.png)

## Perguntas de Pesquisa/Análise Combinadas e Respectivas Análises

### Pergunta/Análise 1
* Suponha que um indivíduo goste de uma Receita A. Quais outras Receitas podemos recomendar a ele?
  * Podemos recomendar uma Receita similar à Raceita A.
Seria necessário criar uma projeção do grafo onde vértices de Receita se relacionam baseado no número de ingredientes em comum.
A partir disso, podemos organizar uma comunidade de Receitas na qual a Receita A faz parte, e então recomendar receitas dessa comunida

### Pergunta/Análise 2
 * Dado um ingrediente, quais outros alimentos poderíamos combinar para gerar novas receitas?
   * Podemos criar uma projeção do grafo onde ingredientes se relacionam baseado no número de receitas. A partir de métodos de Link Prediction, poderíamos descobrir novas relações com esse ingrediente que provavelmente resultariam em uma boa receita.

### Pergunta/Análise 3
 * Quais alimentos são mais consumidos juntos?
   * Podemos realizar uma análise dos grafos utilizando o conceito de comunidade. Essa análise seria feita considerando as arestas entre um ingrediente e outro, representando a frequência com que eles aparecem juntos em receitas. Assim, poderíamos agrupar os ingredientes em comunidades, e identificar quais estão frequentemente conectados.

### Pergunta/Análise 4
* Quais são os ingredientes mais populares?
   * É possível verificar quais os ingredientes mais populares pelo grau de centralidade dos ingredientes, o que ajudaria a identificar quais os ingredientes mais conectados (e, portanto, mais populares) entre as pessoas.