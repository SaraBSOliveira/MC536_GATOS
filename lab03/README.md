# Equipe VIRUS

# Subgrupo B
* Guilhermo de Luiggi Mocelim de Oliveira - 223325
* Luiz Fernando Lima Leite - 248405
* Sara Beatriz da Silva Oliveira - 231288

## Modelo Conceitual ER Revisado
<img src="images/Diagrama ER lab03.png" width="700px" height="auto">


## Modelo Relacional
~~~
ALUNO(_RA_, Nome)
PORCAO(_ID_, Nome, Preco)
PEDE(_RA_, _ID_, _Data_)
  RA: chave estrangeira -> ALUNO
  ID: chave estrangeira -> PORCAO
CARDAPIO(_Data_, _Refeicao_)
INCLUI(_ID_, _Data_, _Refeicao_)
  ID: chave estrangeira -> PORCAO
  Data, Refeicao: chave estrangeira -> CARDAPIO
INGREDIENTE(_Codigo_, Nome)
COMPÕE(_Composto_, _Componente_)
  Composto: chave estrangeira -> INGREDIENTE
  Componente: chave estrangeira -> INGREDIENTE
LEVA(_ID_, _Codigo_)
  ID: chave estrangeira -> PORCAO
  Codigo: chave estrangeira -> INGREDIENTE
NUTRIENTE(_Nome_, ValorReferencia)
CONTEM(_Codigo_, _Nome_, qtdPresente)
  Codigo: chave estrangeira -> INGREDIENTE
  Nome: chave estrangeira -> NUTRIENTE
~~~