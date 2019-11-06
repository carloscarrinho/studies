# ECMA Script 6

## Definir variável com var x let
O ECMA Script 6 introduziu novas funcionalidades à linguagem como as palavras reservadas ```let``` e ```const``` para declaração de variáveis.

A grande diferença entre definir uma variável com 'var' ou com 'let' é que com **var** ela não possui escopo de bloco, isto é, essa tal variável pode ser acessada em qualquer ponto do código.

Já definindo com **let** ela passa a ter escopo, então se declarmos uma variável dentro de um bloco de código, ela só existirá em tal contexto.

O **const** serve para...

Por exemplo:

```javascript

	for (let i = 0; 0 <= i <= 100; i++) {
		console.log(i)
	}

	console.log(i)

```

Com o **let** o valor de 'i' não será impresso no segundo ```console.log(i)``` apenas no primeiro. Isso porque, neste caso, o escopo de variável (definida com 'let') está apenas dentro da função 'for'.

Outro aspecto de diferenciação é que com let não podemos declarar duas vezes uma variável de mesmo nome:

```javascript

let nome = 'Carlos';
let nome = 'Cadu';

//retornará erro

```
O código acima retornará o seguinte erro:

```javascript

Uncaught TypeError: Identifier 'nome' has already been declared

```

## Trabalhando com Objetos
Antes de iniciar os trabalhos com o Modelo MVC, é válido ter uma boa base em manipulação de Objetos em JavaScript.

Para isso, existe uma página do MDN que faz uma 'Reintrodução ao JavaScript' com um capítulo abordando os principais fundamentos aplicados à manipulação de objetos.

A página pode ser acessada em: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/A_re-introduction_to_JavaScript

## Modelo MVC
Este modelo divide a aplicação em três camadas: **Model**, **View** e **Controller**.

### Model
A camada **Model** consiste nas 'abstrações' de um objeto, isto é, quando temos um determinado objeto associado ao nosso projeto, abstraímos ele em um modelo que apresenta suas características (dados).

Por exemplo: se estamos trabalhando na aplicação de uma rede social, possuímos diversos elementos (objetos) e um deles poderia ser o objeto 'Pessoa'.

Para os fins dessa aplicação, entendemos que alguns dados dessa pessoa precisarão ser manipulados, como: nome, idade e sexo.

Assim, temos a nossa primeira 'abstração', a classe 'Pessoa'.

A partir daí podemos criar vários outras _classes_ que irão permitir a implementação do paradigma de **Orientação a Objetos**, como o **grupos**, as **empresas**, as **coleções** (de fotos, arquivos, etc.) e muito mais.

### View


### Controller


### Organização das Pastas
Normalmente quando vamos trabalhar com o modelo MVC, organizamos os arquivos em uma pasta chamada **app** e a subdividimos nas pastas **models**, **views** e **controllers**, além de outras pastas com arquivos auxiliares, como **routes**, **services**, **Helpers** etc.

Naturalmente, os arquivos .js associados aos modelos ficam na pasta **models** e assim por diante.

## Classes

* **class** - define uma 'classe' que...

	Para criarmos uma classe, usamos a palavra reservada ```class``` seguida do nome da classe. Por convenção, **nomes de classe começam em letra maiúscula**. Curiosamente essa convenção se chama **'pascal case'**.

	Para definirmos _atributos_ de instância de uma classe, precisamos adicionar em sua definição um ```constructor ()```. É através do construtor que adicionamos na variável implícita this as propriedades que desejamos que toda instância da classe tenha.

	* **constructor** - cria uma instância de um determinada operação existente em nosso sistema  
		- pode receber parâmetros;
		- (só pode ser chamada utilizando o operador 'new');

```javascript
	//definindo a classe
	class Negociacao {
		//criando uma instância
		constructor (data, quantidade, valor) {
			this.data = data;
			this.quantidade = quantidade;
			this.valor = valor;
		}
	}

```

Para chamarmos (criarmos uma instância) a classe 'Negociacao' precisamos usar o operador ```new``` mais os parênteses '()' no final, conforme o exemplo abaixo:

```javascript
	//não esqueça do 'new' e dos parênteses
	let negociacao = new Negociacao();

```

Quando usamos a sintaxe ```class```, somos obrigados a usar o operador ```new``` para criarmos instâncias dessa classe. Se omitirmos o operador ```new``` receberemos no console a mensagem:

```javascript

	Uncaught TypeError: Class constructor Negociacao cannot be invoked without 'new'

```

* **Encapsulamento** - quando ocorrer uma situação de 'proibirmos' a modificação dos dados para algo de fora da classe, não conseguimos fazer através do código. Então, por convenção, utilizamo um underline ( _ ) para indicar ao programador que tais dados de uma classe não devem ser modificados fora dela, apenas acessados ('modo leitura').

```javascript

	class Negociacao {
		constructor (data, quantidade, valor) {
			this._data = data;
			this._quantidade = quantidade;
			this._valor = valor;
		}
	}
	//perceba o underline antes de data, quantidade e valor
```
obs: por convenção, uma função JavaScript dentro de uma 'class' chamaremos de **'método'**. Isto é, se criarmos uma ação dentro de uma classe, chamaremos de 'método da class'

* **'métodos acessadores'** - sendo 'proibido' modificar os dados por alguém de fora da classe, então precisamos criar formas de disponibilizar os dados para consulta, utilizamos a função ```get``` para isso.

```javascript

	class Negociacao {
		constructor (data, quantidade, valor) {
			this._data = data;
			this._quantidade = quantidade;
			this._valor = valor;
		}
	}
	//criando um método acessador para disponibilizar a data
	get data () {
		return this._data
	}
	//criando um método acessador para disponibilizar a quantidade
	get quantidade () {
		return this._quantidade
	}
	//criando um método acessador para disponibilizar o valor
	get valor () {
		return this._valor
	}
	//criando um método acessador para disponibilizar o volume, após calculá-lo
	get volume () {
		return this.quantidade * this.valor
	}
```

## Objetos imutáveis
Podemos ainda lançar mão do recurso ```Object.freeze()``` para garantir que determinado objeto não terá seus dados modificados.

```javascript

	class Negociacao {
		constructor (data, quantidade, valor) {
			this._data = data;
			this._quantidade = quantidade;
			this._valor = valor;

			//congelando o objeto para que os dados não sejam modificados
			Object.freeze(this);
		}
	}
	//criando um método acessador para disponibilizar a data
	get data () {
		return this._data
	}
	//criando um método acessador para disponibilizar a quantidade
	get quantidade () {
		return this._quantidade
	}
	//criando um método acessador para disponibilizar o valor
	get valor () {
		return this._valor
	}
	//criando um método acessador para disponibilizar o volume, após calculá-lo
	get volume () {
		return this.quantidade * this.valor
	}
```

## Instanciando eventos do Controller
Uma boa prática comumente utilizada para o desenvolvimento WEB é separar bem as funções de cada linguagem: estrutura da página para HTML, estilos para CSS e dinâmica para JavaScript, cada um no seu quadrado.

Contudo, essa solução nos obriga a manipular o DOM toda vez que quisermos associar um evento com o elemento. Sendo assim, quando criamos **SPA** _(Single Page Applications)_ - páginas que não se recarregam durante seu uso - é muito comum usar a abordagem clássica, que é associar a função do evento diretamente na tag ```<html>``` da nossa página.

Por exemplo, se queremos criar uma negociação em nosso sistema a partir de um botão de submit em nosso formulário, podemos fazer:

1º) criar nosso controller:

```javascript

class NegociacaoController {

   //criando um método que adiciona a negociação
   adiciona (event) {
      //limpando o comportamento padrão do navegador
      event.preventDefault();

      //código que adiciona a negociação
   }
}

```

2º) Instanciamos a classe 'NegociacaoController'

```html
<!-- chamando o arquivo .js que cria a classe 'NegociacaoController' -->
<script src="NegociacaoController.js"></script>

<!-- instanciando a classe -->
<script>
	let negociacaoController = new NegociacaoController();
</script>

```

3º) linkamos o evento no HTML:

```html
<!-- atribuindo o controller a um evento de submit do formulário -->
<form onsubmit="negociacaoController.adiciona(event)">
   <!-- tags que criam o formulário -->
</form>

```
Pode parecer trabalhoso, mas é muito menos do que fazer essas associações de evento (3º passo) no JavaScript.

Dependendo do viés teórico do desenvolvedor, essa solução pode ser considerada uma "heresia". Contudo, frameworks SPA, como **Angular**, adotam estrutura semelhante para associar a ação de um **controller** a um componente da página, dessa forma, removendo o desenvolvedor de ter que realizar essa associação manualmente.

## Spread Operator
O **Spread Operator** indica que um array será desmembrado possibilitando a manipulação dos seus itens como parâmetros. Para utilizá-lo, adicionamos reticências (...) antes do array.

Observe este código:

```javascript

let lista1 = ['banana', 'laranja', 'mamão'];
let lista2 = ['caju', 'tangerina', 'abacaxi'];

lista1.push(...lista2);

```
O método ```push``` de todo array aceita receber os dados que você deseja incluir separados por vírgula, ou seja, a função está preparada para receber **N** elementos. Quando passamos a ```lista2``` para ```lista1.push``` com o uso do **spread operator**, cada item da lista será passado como um parâmetro para ```lista.push```:

```javascript

let lista1 = ['banana', 'laranja', 'mamão'];
let lista2 = ['caju', 'tangerina', 'abacaxi'];

lista1.push(...lista2);

console.log(lista1);
// ["banana", "laranja", "mamão", "caju", "tangerina", "abacaxi"]

```

## Outros recursos

* **.map** - percorre os itens de um array. Podemos passar como parâmetros qual o item e qual o índice que estamos buscando: ```.map(item, indice)```;

* **.split** - separa strings por meio de algum separador. Passamos dentro de parênteses o separador que utilizaremos para 'quebrar' a string: ```.split('-')```. Neste caso foi um traço ( - );

* **arrow function** - cria uma função de uma forma mais limpa (menos verbosa). Não precisamos dar um nome para a função (similar à 'função anônima') e, quando a função tem apenas uma instrução (uma linha) não precisamos usar o bloco com as chaves '{}', bastando indicar com um '=>' (seta) mais a instrução:

```javascript

let data = new Date(...
	this._inputData.value
		 .split('-')
		 .map((item, indice) => item - indice % 2)

		 //arrow function que percorre o array e executa a instrução
)

```

* **.concat** - concatena dois ou mais arrays e itens em uma array única.

```javascript

let listaDeNomes1 = ['Flávio', 'Rogers', 'Júlia'];
let listaDeNomes2 = ['Vieira', 'Fernanda', 'Gerson'];
exibeNoConsole([].concat(listaDeNomes1, listaDeNomes2, 'Rômulo'));

```


## Helpers (Ajudantes)
Embora o modelo seja 'apenas' MVC (Model, View, Controller), como explanado mais acima quanto a organização de pastas, podemos criar outras classes que irão auxiliar nessa divisão de responsabilidades, facilitando a organização e reutilização de código.

## Métodos Estáticos (static)



## Pincelada em Expressões Regulares (RegEsp)
Temos os seguintes comandos que definem uma função que sabe validar um determinado **código**:

```javascript

let codigo = 'GWZ-JJ-12';

function validaCodigo(codigo) {

    if(/\D{3}-\D{2}-\d{2}/.test(codigo)) {
          alert('Código válido!');
      } else {
          alert('Código inválido');
      }

}

validaCodigo('GWZ-JJ-12'); // válido
validaCodigo('1X1-JJ-12'); // inválido

```
Muita coisa acontecendo? Vamos desmembrar o código para facilitar a leitura:

```javascript

function validaCodigo(codigo) {

    // Duas barras criam a expressão regular. Mas também poderíamos ter usado
    // a sintaxe new RegExp(/\D{3}-\D{2}-\d{2}/)
    // \D é qualquer coisa não dígito
    // \D{3} é qualquer coisa não dígito que forme um grupo de 3 caracteres
    // \d é qualquer dígito.
    let expressao = /\D{3}-\D{2}-\d{2}/;

    // toda expressão regular possui o método test
    // que recebe o alvo do teste, retornando true
    // se passou, e false se falhou
    if(expressao.test(codigo)) {
          alert('Código válido!');
      } else {
          alert('Código inválido');
      }

}

validaCodigo('GWZ-JJ-12'); // válido
validaCodigo('1X1-JJ-12'); // inválido

```
O exemplo de solução acima é **procedural**, toda vez que criarmos um código precisaremos buscar em algum lugar do nosso sistema alguém que o valide. Temos uma separação entre dado e comportamento.

Podemos aplicar a **programação orientada a objetos** nesse contexto criando uma ```class``` que representa um código e encapsular a regra de que o código deve ter determinado formato:

```javascript

class Codigo {

    constructor(texto) {

        if(!this._valida(texto)) throw new Error(`O texto ${texto} não é um código válido`);
        this._texto = texto;        
    }

    _valida(texto) {

        return /\D{3}-\D{2}-\d{2}/.test(texto);
    }

    get texto() {

        return this._texto;
    }
}

let codigo1 = new Codigo('GWZ-JJ-12'); // válido
console.log(codigo1.texto);
let codigo2 = new Codigo('1X1-JJ-12'); // inválido
console.log(codigo2.texto);

```

Onde quer que tenhamos um código, dado e comportamento caminham juntos, mesmo que esse comportamento/regra esteja no construtor. Aliás, o ```_valida``` está prefixado desta forma porque esse método só deve ser chamado pela própria classe.

## Imediately Invoked Function Expression (IIFE)
Quando colocamos uma função toda dentro de um parênteses e a chamamos com outros parênteses:

```javascript

(function () {
	let total = 0;
	model.negociacoes.forEach(n => total += 	n.volume);
})();
//perceba que a função está dentro dos parênteses e com outros parênteses

```
detalhar melhor essa seção

## Reduce
A função ```reduce()``` reduz o array a um único valor. Ela executa a função passada como parâmetro para cada item do array, acumulando o valor de retorno da função em um 'total'.

É importante observar que o ```reduce ()``` não executa a função para um array que não possui valores.

```html

<button onclick="myFunction()">Try it</button>

<p>Sum of numbers in array: <span id="demo"></span></p>

<script>
var numbers = [15.5, 2.3, 1.1, 4.7];

function getSum(total, num) {
  return total + Math.round(num);
}

function myFunction(item) {
  document.getElementById("demo").innerHTML = numbers.reduce(getSum, 0);
}
</script>

```

## Resumo com exemplo do Cadu

buscar aquivo .txt na pasta
