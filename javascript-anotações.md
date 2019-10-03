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

- Podem começar com '$' ou _
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

### Operadores

O JavaScript possui várias famílias de operadores, as mais comuns são:

- Aritméticos;
- Atribuição;
- Incremento;
- Relacionais;
- Lógicos;
- Ternários.

Obs: observe que quando tivermos um código com a presença de vários tipos de operadores, a precedência ocorre com base na sequência que estão sendo apresentados esses conceitos, isto é: Aritméticos --> Atribuição --> Relacionais --> Lógicos --> Ternários.

#### Operadores Aritméticos

São aqueles associados às operações matemáticas básicas: soma, subtração, divisão, etc.

O mais relevante de ser dito neste ponto é o uso dos operadores:

- 5 % 2 = 1 (o operador '%' retorna o valor do resto de uma divisão, isto é, 5 divido por 2 dá 2 com resto 1)
- 5 ** 2 = 25 (o operador ** representa uma potência)

No uso dos operadores é muito importante atentar para a precedência matemática entre eles.

#### Operadores de Atribuição

O operador de atribuição é o '=' e lê-se 'recebe'.

```javascript
var n = 3 // n recebe 3, essa é a chamada 'atribuição simples'

n = n + 5 // agora, o n que valia três, foi somado com cinco, passando a valer 8. Essa é a chamada 'auto-atribuição'
n += 5 // essa expressão signigica o mesmo da de cima, podemos utilizá-la quanto temos uma variável realizando uma operação com ela mesma.
```

#### Operadores de Incremento

É muito comum na programação que precisemos fazer, por exemplo:

```javascript
var x = 5

x = x + 1
```

Quando isso acontece, podemos utilizar a sintaxe x++, isso quer dizer a mesma coisa do anterior, porém de uma forma mais resumida. Ficamos então com:

```javascript
var x = 5 // x recebe 5

x++ // x igual a x mais 1

// da mesma forma para subtração

x-- // x igual a x menos 1
```

#### Operadores Relacionais

'<' menor
'>' maior
'>=' maior ou igual
'<=' menor ou igual
'==' igual
'!=' desigual ou diferente
'===' idêntico

#### Operadores Lógicos

'!' negação
'&&' conjunção (e)
'||' disjunção (ou)

```javascript
idade >= 15 && idade <= 17 // A idade está entre 15 e 17 anos?
estado == 'RJ' || estado == 'SP' // O estado é RJ ou é SP?
salario == 1500 && sexo != 'M' // É uma mulher que ganha mais de 1500?
```

#### Operadores Ternários

'?' teste de uma condição
':' separador das respostas do teste

Daí funciona assim: 'teste?true:false'

```console
> var media = 5.5
undefined
> media > 7?'APROVADO':'REPROVADO'
> 'REPROVADO'
```

### Entendendo o Document Object Model (DOM)

#### Introdução ao DOM
DOM é um conjunto de objetos dentro do navegador que vai dar acesso aos componentes internos do website.

A 'Árvore DOM' representa a árvore hierárquica dos elementos constantes no documento html. Nesta árvore, o 'window' é o elemento pai (parent) principal, isto é, todos os demais elementos (child) estão dentro dele.

Por padrão, é possível selecionar os elementos no DOM por meio de:
- TagName: .getElementByTag() ou .getElementsByTag()[] - perceba neste caso que quando tem mais de um elemento deve-se indicar qual deles se deseja buscar entre colchetes;
- Id - .getElementById();
- Name - .getElementByName();
- Class - .getElementByClass();

Porém, o mais recomendado (e comum) é utilizar seletores CSS para buscar o elemento, através dos comandos '.querySelector()' e '.querySelectorAll()'. O único problema é que este recurso é mais recente, então em navegadores antigos pode quebrar.

#### Eventos DOM
Eventos são tipos de interações possíveis do usuário com o conteúdo da página.

Há uma lista super extensa de eventos possíveis, é valido acessar a página de referência do MDN: https://developer.mozilla.org/en-US/docs/Web/Events

Para utilizar os eventos na prática, é necessário que aliar um evento a uma função, isto é, a ação que deve ser executada a partir do disparo do evento, como por exemplo um clique em um botão, ou um input de dados em um formulário ou ainda a movimentação do cursor do mouse sobre algum elemento.

É possível adicionar o evento a partir do HTML:

```html
<body>
	<!-- utilizando o evento de clique por meio do html, mas também é possível (e recomendado) fazer pelo JavaScript -->
	<div id="area" onclick="clicar()" onmouseenter="entrar()" onmouseout="sair()">
		Interaja...
	</div>

	<script>
		//buscando elementos utilizando a estrutura da árvore DOM: window --> document --> elemento
		var area = window.document.getElementById('area');

		//definindo quais ações deseja executar dentro de funções
		function clicar() {
			a.innerText = 'Clicou';
			a.style.backgroud = 'red';
		}
		function entrar() {
			a.innerText = 'Entrou';
		}
		function sair() {
			a.innerText = 'Saiu';
		}
	</script>
</body>
```

Mas também é possível chegar ao mesmo resultado utilizando o comando 'addEventListener' (escutadores) por meio do JavaScript.

```html
<body>
	<div>
		Interaja...
	</div>

	<script>
		var area = window.document.getElementById('area');

		//adicionando interação apenas por meio do JavaScript
		a.addEventListener('click', clicar);
		a.addEventListener('onmouseenter', entrar);
		a.addEventListener('onmouseout', sair);
	</script>
</body>
```

### Condições

#### Condição simples
Possui apenas um bloco condicional, comumente com o valor ```true```. Se a condição retornar ```false``` nada acontece.

```javascript
if (numero > x) {
	//script que deve ser executado se a condição for verdadeira
}
```

#### Condição Composta
Possui dois blocos condicionais, um ```if``` e ```else```. Temos dois scripts diferentes para quando a condição retorna ```true``` ou ```false```.

```javascript
var velocidade = 45;

if (velocidade > 60) {
	//script caso a condição retorne 'true'
	console.log('Você ultrapassou o limite máximo de velocidade, MULTADO!');
}else {
	//script caso a condição retorne 'false'
	console.log('Dirija sempre com o cinto de segurança!');
}
```

#### Condições Aninhadas
Quando é necessário fazermos mais de duas condições, podemos utilizar o ```else if``` para aninhar as condições. É possível criar quantos ```else if``` quanto forem necessários para satisfazer o conjunto de Condições.

```javascript
var idade = 15

if (idade < 16) {
	console.log('Não vota');
} else if (idade < 18 || idade > 65) {
	console.log('Voto opcional');
} else {
	//neste 'else' também poderíamos colocar 'else if'
	console.log('Voto obrigatório');
}
```

#### Condições Múltiplas
Em situações específicas podemos utilizar uma outra estrutura para estabelecer condições que é o ```switch```, para isso precisamos utilizar uma expressão como base, o ```case``` para cada uma das condições e o ```break``` para fechar o case e, por fim, o ```default``` para estabelecer qual a condição padrão.

É obrigatório o uso do ```break``` para fechamento dos ```case```, porém é uma boa prática utilizá-lo também para a condição ```default```.

```javascript
switch (expression) {
	case expression:

		break;
	default:
}
```
Um recurso bastante útil no trabalho com condicionais é o ```new Date()```. Ele busca a data atual do sistema, seja o navegador do usuário (em ambiente de produção), ou o servidor do desenvolvedor (em ambiente de desenvolvimento).

```javascript
var data = new Date();
//a título de curiosidade para pegar a hora do sistema usamos '.getHour'
var hora = data.getHour();
var diaSemana = data.getDay();
//o '.getDay' retorna o dia da semana (domingo, segunda, terça, etc.)
//os dias da semana funcionam como um array onde o domingo é a posição zero [dom, seg, ter, etc.]

//lemos assim: 'de acordo com o dia da semana...'
switch (diaSemana) {
	//'se e o valor for zero, escreva no console: Domingo'
	case 0:
		console.log('Domingo');
		break;
	//'se o valor for 1, escreva no console: Segunda'
	case 1:
		console.log('Segunda');
		break;
	case 2:
		console.log('Terça');
		break;
	//'se não satisfazer nenhum dos casos anteriores, escreva: [ERRO] Dia inválido'
	default:
		console.log('[ERRO] Dia inválido');
}
```
Não é recomendado utilizar o ```switch``` para testar intervalos (como no exemplo da obrigatoriedade de voto, mais acima). Nestes casos é melhor utilizar a estrutura ```if```.

### Alguns recursos úteis

- .setAttribute: Insere atributos dentro de elementos no DOM ;

- .innerHTML: Modifica o texto que está dentro de uma tag no HTML;

- .createElement combinado com .appendChild: Permite criar um elemento dentro do HTML, como se fossemos lá e criássemos manualmente. É útil quando queremos criar estruras ou inserir coisas na página conforme a interação do usuário.

### Estruturas de Repetição (Laços)
Laços são blocos de código que se repetem enquanto uma determinada condição for atendida. Para utilizar esse tipo de estrutura podemos utilizar as funções:

- while(condição){} - que é uma estrutura de repetição com teste lógico no início;

```javascript
var contador = 1;
while (contador <= 6) {
	console.log(`Passo ${contador}`);
	contador++
}
```

- do {} while(condição) - que é uma estrutura de repetição com teste lógico no final.

```javascript
//com esta estrutura chegamos ao mesmo resultado do exemplo anterior
var contador = 1;
do {
	console.log(`Passo ${contador}`);
	contador++
} while (contador <= 6) {
}

```
- for (inicio; teste; incremento){} - que é uma estrutura de repetição com variável de controle. E comumente a mais utilizada pelor programadores em situações onde se conhece o limite das execuções (quantas vezes o bloco de código tem de ser executado).

```javascript
for (var contador = 1; contador <= 6; contador++){
	console.log(`Passo ${contador}`);
}
```


### Variáveis Compostas
As *variáveis simples* são aquelas que só conseguem armazenar um valor por vez. Desse modo, as *variáveis compostas* são aquelas capazes de armazenar vários valores em uma mesma estrutura. Este tipo de variável faz uso do chamado *Array* (ou Vetor, em portuquês).

```javascript
var automoveis = [opala, escort, monza, celta, fiesta, corsa, siena, punto];
//se eu quisesse armazenar os carros que minha familia e eu já tivemos todos em uma única variável
```

Os arrays são representados pelos colchetes '[]', armazenando os elementos em *keys* (ou índices, em portuquês), que podem ser utilizados para acessar o *valor* de cada elemento posteriormente. Esses índices são contados a partir do zero, ou seja, na variável composta criada no exemplo acima, o opala está no índice 0, o escort no índice 1, e assim sucessivamente.

```javascript
let automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];

for (carro = 0; carro < automoveis.length; carro++){
	console.log(`O ${carro + 1}º veículo que minha família teve foi o ${automoveis[carro]}`);
	if (carro == automoveis.length) {
		console.log(`O ${carro + 1}º nosso carro atual é o ${automoveis[carro]}`);
	}
}
```

É possível inserir um novo elemento dentro de um array previamente definido, para isso pode-se fazer de duas formas:

1ª) indicar a variável, o índice do elemento que se deseja colocar no array entre colchetes e depois o elemento propriamente dito:

```javascript
let automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];

// variavel[índice do elemento] = valor do elemento;
automoveis[8] = 'uno vivace';
```

2ª) Utilizar o comando .push(valor do elemento). Neste caso, o novo elemento será inserido ao final da lista.

```javascript
let automoveis = ['opala', 'escort', 'monza', 'celta', 'fiesta', 'corsa', 'siena', 'punto'];

// variavel[índice do elemento] = valor do elemento;
automoveis.push('uno vivace');
```

Caso tenhamos um array formado por números como:

```javascript
let num = [5, 8, 7, 3, 9, 2];
```

Podemos utilizar o .sort() para organizá-los em ordem crescente dentro da lista:

```javascript
let num = [5, 8, 7, 3, 9, 2];

num.sort();
//o resultado seria: [2, 3, 5, 7, 8, 9]

```
