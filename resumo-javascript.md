# JavaScript
O JavaScript (JS) é uma linguagem de programação _multiparadigma_ originalmente criada para desenvolvimento no client side. É uma linguagem de alto nível e interpretada pelos navegadores, permitindo adicionar dinamicidade às páginas. 

Atualmente também é possível programar o **server side** com o auxílio do framework **Node Js**.

Para projetos mais complexos, atualmente os dois principais frameworks mais usados são o **React** e o **Angular**.

## Criando Comentários
Os comentários em JavaScript podem ser realizados de duas formas:

* com duas barras para comentar um trecho com apenas uma linha;
* com barra asterisco asterisco barra para comentar um trecho com mais de uma linha.

```javascript

// em uma linha

/*
comentários em
mais de
uma linha
*/

```

## Variáveis

As **variáveis são uma forma que temos de guardar dados**. Elas podem ser de vários tipos, os mais comuns são 'string', 'number' e 'boolean'.

Para definir uma variável deve-se colocar ```var```, ```let``` ou ```const```, o nome que você deseja dar para tal variável, o sinal de igual '=' (que em programação deve-se ler como 'recebe') e o **seu valor inicial**.

### var x let x const
O ECMA Script 6 introduziu novas funcionalidades à linguagem como as palavras reservadas ```let``` e ```const``` para declaração de variáveis.

* **var**: definindo uma variável com ```var```, tal variável **não possuirá escopo de bloco**, isto é, essa tal variável pode ser acessada em qualquer ponto do código.

```javascript
var nome = 'Carlos' //definimos uma variável chamada 'nome' que recebeu um valor do tipo 'string'

var n1 = 54 // definimos uma variável chamada 'n1' que recebeu um valor do tipo 'number'
```

* **let**: definindo com ```let``` ela passa a ter escopo, então se declarmos uma variável dentro de um bloco de código, ela só existirá em tal contexto. 

```javascript

for (let i = 0; 0 <= i <= 100; i++) {
    console.log(i)
}
    
console.log(i)

```
Como utilizamos o ```let``` para definir a variável 'i', seu valor não será impresso no segundo ```console.log(i)```, apenas no primeiro. Isso porque, neste caso, o escopo de variável está apenas dentro da função 'for'.

Outro aspecto de diferenciação é que com let não podemos declarar duas vezes uma variável de mesmo nome:

```javascript

let nome = 'Carlos';
let nome = 'Cadu';

//retornará erro

```

* **const**: cria uma variável cujo **o valor é fixo**, ou seja, uma constante somente leitura. Isso não significa que o valor é imutável, apenas que a variável constante não pode ser alterada ou retribuída. (explorar mais em: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/const)

### Pontos de Atenção

#### Identificadores

Existem algumas regras para a definição do nome de uma variável, são elas:

* Podem começar com '$' ou _
* Não podem começar com números
* É possível usar letras com números
* É possível usar acentos e símbolos
* Não podem conter espaços
* Não podem usar palavras reservadas da linguagem (verificar lista de palavras reservadas em: https://www.w3schools.com/js/js_reserved.asp)


#### Definição de um bom nome de variável

1. Letras maiúsculas e minúsculas fazem diferença - a variável 'a' é diferente da variável 'A';
2. Tente escolher nomes coerentes para as variáveis - deve-se evitar usar n1, n2, n3 ou x, y, z, etc. Se a variável guarda o nome de alguem, defina como 'nome', se é o telefone, defina 'telefone', se é o endereço, por que não definir como 'endereco'? Enfim, use identificadores coerentes;


## Tipos Primitivos

### Tipos de Dados
Como dito anteriormente, as variáveis podem receber vários tipos de dados e o entendimento do tipo é importante, pois eles interferem na forma como a linguagem interpreta os comandos.

Os tipos são:

* **number**: 1, 7, 45, -15, 7.7, .9 (Esse tipo possui ainda dois 'tipos internos' o 'Infinity' e ou 'NaN' (que significa Not a Number));
* **string**: 'Carlos', 'Emili', 'Digite seu texto aqui'
* **Boolean**: ```true``` ou ```false```
* **null**;
* **undefined**;
* **object** (dentro desse tipo tem a famosa **Array**, que consiste grossamente em uma lista de dados)
* **function**;

Para saber o tipo de uma determinada variável, pode-se usar o comando 'typeof' no console:

```console
var nome = 'Emili'
> typeof nome
> 'string'
```

### Manipulando Números
Para formatar números contidos em variáveis, podemos utilizar algumas funcionalidades. 

* **to.Fixed:** Adiciona um número fixo de casas decimais;
* **replace:** permite trocar, por exemplo, o ponto (.) utilizado pelo formato americano para a vírgula (,) em números decimais;
* **toLocaleString:** permite apresentar também o tipo de moeda.

### Conversão de Tipos
Diante dos tipos existentes, em muitos casos será necessário fazer a sua conversão em determinado ponto do código.

#### de 'String' para 'Number'
Os dois recursos mais comuns usados na manipulação de strings para números são o ```parseInt``` e o ```parseFloat```.

* **parseInt:** Analisa uma **string** e a converte apresentando-a como um tipo **number** com valor **inteiro**.

    * Pode ser especificada uma base (um valor inteiro entre 2 e 36), porém, quando esse parâmetro não é especificado, o valor assumido fica em 10 (entenda melhor este ponto em: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/parseInt).

* **parseFloat:** Tem um comportamento similar ao ```parseInt```, porém o ```parseFloat``` apresenta o valor como um número decimal.

    * É válido ressaltar que se o ```parseFloat``` encontrar um caractere diferente de um sinal (+ ou -), numeral (0-9), um ponto decimal, ou um expoente, ele retorna o valor até esse ponto e ignora esse caractere e todos os caracteres seguintes;

    ```javascript
    parseFloat("3.14");
    parseFloat("314e-2");
    parseFloat("0.0314E+2");
    parseFloat("3.14more non-digit characters");
    // o retorno será 3.14 para todos os casos
    ```

    * Se o primeiro caractere não puder ser convertido para **number**, o ```parseFloat``` retorna ```NaN```;

    ```javascript
    parseFloat("FF2");
    ```

#### de 'Number' para 'String'
É comum em muitos pontos do código termos que converter um número para uma string, para isso utilizamos basicamente o recurso ```toString``` ou envolvemos uma variável no ```String(variavel)```

```javascript
var idade = 28;

idade = idade.toString;
//ou
idade = String(idade);
```

### Manipulando Strings
Além da conversão dos tipos, também precisamos manipular as strings que temos no código e cada contexto necessita de um recurso diferente (concatenação, formatação dos caracteres, contagem dos caracteres, etc.)

#### Concatenção e Template Strings
Outro aspecto comum no dia a dia do código, é a necessidade de concatenação de strings. Até o ES6 o pessoal utilizava a concatenação propriamente dita. Contudo, depois desse marco (ES6), foi introduzido o recurso **template strings**, que facilita muito essa implementação.

Vamos supor que temos as seguintes variáveis definidas:

```javascript
var nome = 'Cadu' // dado do tipo string
var idade = 28 // dado do tipo number
var nota = 9.5 // outro dado do tipo number

// se eu quiser imprimir na tela um texto que apresenta o nome, idade e nota, após definidas tais variáveis

document.write('A nota de ' + nome ', que possui ' + idade ' anos' + ', é de ' + nota) // utilizando o simbolo '+' para concatenação
document.write(`A nota de ${nome}, que possui ${idade} anos, é de ${nota}`) // utilizando o recurso 'template string' --> `${}`

// É impotante atentar para o uso do símbolo de crase (`) no caso de template strings.
```

#### Outros recursos úteis

* **string.length:** conta quantos caracteres uma determinada string possui;
* **string.toUpperCase:** transforma todas as letras do texto de uma string em **maiúsculas**;
* **string.toLowerCase:** transforma todas as letras do texto de uma string em **minúsculas**.

## Operadores

### Operadores Aritméticos

### Operadores de Atribuição

### Operadores de Incremento

### Operadores Relacionais

### Operadores Lógicos

### Operadores Ternários



## Arrays
As **variáveis simples** são aquelas que só conseguem armazenar um valor por vez. Desse modo, as **variáveis compostas** são aquelas capazes de armazenar vários valores em uma mesma estrutura. Este tipo de variável faz uso do chamado **Array (ou Vetor, em portuquês)**.

```javascript
var automoveis = [opala, escort, monza, celta, fiesta, corsa, siena, punto];
//se eu quisesse armazenar os carros que minha familia e eu já tivemos todos em uma única variável
```
Os arrays são representados pelos colchetes '[]', armazenando os elementos em **keys (ou índices, em portuquês)**, que podem ser utilizados para acessar o valor de cada elemento posteriormente. Esses índices são contados a partir do zero, ou seja, na variável composta criada no exemplo acima, o opala está no índice 0, o escort no índice 1, e assim sucessivamente.

```javascript
let automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];

for (carro = 0; carro < automoveis.length; carro++){
	console.log(`O ${carro + 1}º veículo que minha família teve foi o ${automoveis[carro]}`);
	if (carro == automoveis.length) {
		console.log(`O ${carro + 1}º nosso carro atual é o ${automoveis[carro]}`);
	}
}
```

### Manipulando Arrays

#### Inserindo elementos no Array
É possível inserir um novo elemento dentro de um array previamente definido, para isso pode-se fazer de três formas:

1ª) indicar a variável, o índice do elemento que se deseja colocar no array entre colchetes e depois o elemento propriamente dito:

```javascript
let automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];

// variavel[índice do elemento] = valor do elemento;
automoveis[6] = 'uno vivace';

//retorna o elemento 'uno vivace' na posição '6'.
// automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'uno vivace', 'siena', 'punto'];
```

2ª) **push:** Adiciona um ou mais elementos ao final do array:

```javascript
let automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];

// variavel[índice do elemento] = valor do elemento;
automoveis.push('uno vivace');

//retorna o elemento 'uno vivace' no final do array, neste caso, na posição '8'
// automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto', 'uno vivace'];
```

3ª) **unshift:** adiciona um ou mais elementos no início de um array:

```javascript
let automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];

// variavel[índice do elemento] = valor do elemento;
automoveis.unshift('uno vivace');

//retorna o elemento 'uno vivace' no INÍCIO do array
// automoveis = ['uno vivace', 'opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];
```

#### Removendo elementos do Array

* **pop:** Remove um ou mais elementos do final da array
* **shift:**
* **splice:**

### Arrays Bidimensionais


### Arrais Tridimensionais

* reduce



## Document Object Model (DOM)

## Selecionar Elementos

### Get Elements
* getElementsById
* getElementsByTagName
* getElementsByClass
* getElementsByName

### Query Selector
* querySelector

## Adicionar Eventos

### Event Listener
* addEventListener

### Eventos de Mouse

### Eventos de Teclado


## Condições

### Condição Simples

#### Condição Ternária

### Condição Composta

### Condições Aninhadas

### Condição Múltipla



## Laços (Estruturas de Repetição)

### While

### Do While

### For

### For Each



## Funções

### Função 'Normal'

### Função Anônima

### Arrow Function

### Imediately Invoked Function Expression (IIFE)



## Objetos



## Classes

### Contructor

### Getters e Setters

### Métodos Estáticos (static)

### Herança




## Recursos Avançados

### Spread Operator


