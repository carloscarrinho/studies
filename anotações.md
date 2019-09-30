# Anotações sobre JavaScript
## Curso em Vídeo - Gustavo Guanabara
---

### comentários

Os comentários em JavaScript podem ser realizados de duas formas:

- com duas barras para comentar um trecho com apenas uma linha;
- com barra asterisco asterisco barra para comentar um trecho com mais de uma linha.


```javascript
	// em uma linha

	/*
	comentários em 
	mais de 
	uma linha
	*/
```



### Variáveis e Tipos Primitivos


#### definição de variaveis

As variáveis são uma forma que temos de guardar dados, elas podem ser de vários tipos, os mais comuns são 'string', 'number' e 'boolean'.

Para definir uma variável deve-se colocar 'var' (ou 'let' ou 'const'), o sinal de igual '=' (que em programação deve-se ler como 'recebe') e o nome que você deseja dar para tal variável.

```javascript
	var nome = 'Carlos' //definimos uma variável chamada 'nome' que recebeu um valor do tipo 'string'

	var n1 = 54 // definimos uma variável chamada 'n1' que recebeu um valor do tipo 'number' 

```

Elas podem ser definidas diretamente, como no exemplo acima, mas também podem ser capturadas a partir de uma interação como o usuário da página / aplicação.

```javascript
var nome = window.prompt("Coloque seu nome aqui");
```

As variáveis são extremamente importantes para o desenvolvimento de qualquer sistema.

##### identificadores

Existem algumas regras para a definição do nome de uma variável, são elas:

- Podem começar com '$' ou '_'
- Não podem começar com números 
- É possível usar letras com números
- É possível usar acentos e símbolos
- Não podem conter espaços
- Não podem usar palavras reservadas da linguagem verificar lista de palavras reservadas em: []

Alguns pontos de atenção e dicas para definição de um bom nome de variável:

1. Letras maiúsculas e minúsculas fazem diferença - a variável 'a' é diferente da variável 'A';

2. Tente escolher nomes coerentes para as variáveis - deve-se evitar usar n1, n2, n3 ou x, y, z, etc. Se a variável guarda o nome de alguem, defina como 'nome', se é o telefone, defina 'telefone', se é o endereço, por que não definir como 'endereco'? Enfim, use identificadores coerentes;

##### tipos de dados

Como dito anteriormente, as variáveis podem receber vários tipos de dados e o entendimento do tipo é importante, pois eles interferem na forma como a linguagem interpreta os comandos.

Os tipos são:

- number: 1, 7, 45, -15, 7.7, .9 (Esse tipo possui ainda dois 'tipos internos' o 'Infinity' e ou 'NaN' (que significa Not a Number));
- string: 'Carlos', 'Emili', 'Digite seu texto aqui'
- Boolean:
- null;
- undefined;
- object (dentro desse tipo tem a famosa Array, que consiste grossamente em uma lista de dados)
- function;

Para saber o tipo de uma determinada variável, pode-se usar o comando 'typeof' no console:

```console 
	> var nome = 'Emili'
	> typeof nome
	> 'string'
```

##### conversão de tipos

Diante dos tipos existentes, em muitos casos será necessário fazer a sua conversão em determinado ponto do código.

de String para Number

```javascript
var idade = Number.parseInt(window.prompt('Qual a sua idade?')) // código para capturar um número inteiro

var altura = Number.parseFloat(window.prompt('Qual a sua altura?')) // código para capturar um número quebrado

var nota = Number(window.prompt('Qual a sua nota em matemática?')) // recurso recente do JavaScript onde a própria linguagem interpreta o nº

```


de Number para String

```javascript

var idade = 28

idade = String(idade) 

// ou

idade = idade.toString 

```

##### manipulando strings

Formas de utilizar variáveis strings:

```javascript
//vamos supor que temos as seguintes variáveis definidas

var nome = 'Cadu' // dado do tipo string
var idade = 28 // dado do tipo number
var nota = 9.5 // outro dado do tipo number

// se eu quiser imprimir na tela um texto que apresenta o nome, idade e nota, após definidas tais variáveis

document.write('A nota de ' + nome ', que possui ' + idade ' anos' + ', é de ' + nota) // utilizando o simbolo '+' para concatenação

document.write(`A nota de ${nome}, que possui ${idade} anos, é de ${nota}`) // utilizando o recurso 'template string' --> `${}`

// É impotante atentar para o uso do símbolo de crase (`) no caso de template strings.

```

##### outros comandos comuns no uso de strings

- string.length -- conta quantos caracteres uma determinada string possui
- string.toUpperCase -- transforma todas as letras do texto de uma string em maiúsculas
- string.toLowerCase -- transforma todas as letras do texto de uma string em minúsculas

```javascript

//exemplo de uso do comando .length com strings

var nome = window.prompt('Qual o seu nome?')
document.write('Seu nome tem ${nome.length} letras.')
document.writeln('Seu nome em maiúsculas é ${nome.toUpperCase}.') // o comando 'document.writeln' imprime o texto na linha seguinte
document.writeln('Seu nome em minúsculas é ${nome.toLowerCase}.') 

```

##### manipulando números

Para formatar números contidos em variáveis, podemos utilizar as funcionalidades

- to.Fixed(): define uma quantidade de casas decimais
- .replace: permite trocar, por exemplo, o ponto (.) utilizado pelo formato americano para a vírgula (,) em números decimais
- .toLocaleString: permite apresentar também o tipo de moeda 

```javascript
var n1 = 1547.8745

// se eu quiser imprimir na tela definindo que o valor dessa variável deverá ter, no máximo, duas casas decimais

document.write(n1.toFixed(2)) // estabeleço a quantidade de casas decimais dentro do parenteses do .toFixed().

// e se eu quiser trocar do padrão americano para o brasileiro?

document.write(n1.toFixed(2).replace('.',','))

// e se de repente esta variável n1 representa um valor monetário em reais (R$)?

document.write(n1.toLocaleString('pt-BR', {style: 'currency', currency: 'BRL'}))
```
