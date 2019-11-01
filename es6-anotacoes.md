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

### Model


### View


### Controller


### Organização das Pastas
Normalmente quando vamos trabalhar com o modelo MVC, organizamos os arquivos em uma pasta chamada **app** e a subdividimos nas pastas **models**, **views** e **controllers**, além de outras pastas com arquivos auxiliares, como **routes**, **services**, etc.

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

Quando usamos a sintaxe class, somos obrigados a usar o operador new para criarmos instâncias dessa classe. Se omitirmos o operador new receberemos no console a mensagem:

```console

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
Uma boa prática comumente utilizada para o desenvolvimento WEB é separar bem as funções de cada linguagem: estrutura da página para HTML, estilos para CSS e dinâmica para JavaScript.

Entretanto, para criarmos os eventos que iniciam os Controllers, para diminuir a quantidade de código no mundo JavaScript, podemos fazer as chamadas dentro do HTML.

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

2º) linkamos o evento no HTML:

```html
<!-- atribuindo o controller a um evento de submit do formulário -->
<form onsubmit="negociacaoController.adiciona(event)">
   <!-- tags que criam o formulário -->
</form>

```

## Evitando percorrer o DOM
