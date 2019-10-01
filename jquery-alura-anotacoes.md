# Curso de jQuery
## Plataforma Alura

### Introdução

#### O que é?
O jQuery é uma biblioteca, feita em JavaScript, que tem como objetivo facilitar a vida do desenvolvedor Web. O grande propósito dela é facilitar o uso do JavaScript nos websites, abstraindo da cabeça do desenvolvedor os problemas de compatibilidade entre os navegadores. Ele também possui funções enxutas, que reduzem drasticamente a quantidade de código que o desenvolvedor tem que escrever, possuindo módulos que facilitam coisas como o AJAX , que é algo nativamente complexo de se fazer com JavaScript puro.

#### Versões
No site do jQuery podemos baixar três tipos de versões:

- 'Production': versão comprimida (mais leve) para uso no servidor de produção;
- 'Development': versão completa para o uso do desenvolvedor;
- 'Slim': versão mais leve que não contem suporte para AJAX e animações;

Obs: a versão Slim é útil para desenvolvedores que querem utilizar o jQuery apenas para a manipulação do DOM, escutar eventos, adicionar ou remover classes ou criar elementos, permitindo estes desenvolvedores terem acesso a uma versão mais simples do framework, pois muitas vezes queremos fazer animações utilizando algum recurso do CSS3 ou utilizar alguma outra biblioteca específica para requisições AJAX.

### Como inserir no projeto?
O arquivo de jQuery deve ser importado da mesma forma que um arquivo JavaScript, entre as tags script do HTML.
É importante que tal aquivo jQuery seja importado na página antes do aquivo JavaScript que deseja fazer uso de suas funcionalidades. Assim, se temos um aquivo 'main.js' e um arquivo 'jquery.js', nossa tag script ficará da seguinte forma:

```html
<!-- importando o arquivo jQuery -->
<script src="jquery.js"></script>
<!-- importando o arquivo JavaScript que faz uso do arquivo jQuery -->
<script src="main.js"></script>
```

### Primeiros passos com jQuery

- jQuery ou $: para buscar um determinado elemento no documento HTML.

```javascript
var nome = jQuery('.nome').text() // define a variável nome como o valor do elemento que possui a class 'nome'

var idade = $('#idade').text() // define a variável 'idade' como o valor do elemento que possui o id 'idade'
```

- .text(): serve para buscar o texto de um elemento no documento quando o parênteses for vazio, ou para modificar o texto de um elemento quando é passado algum parâmetro dentro do parênteses. É muito importante não esquecer do parênteses ao final do comando;

- .val(): busca um texto digitado dentro de um formulário;

- .on(): recebe como parâmetro dois argumentos, o primeiro sendo uma string com o nome do evento que ela vai passar a escutar e o segundo uma função, com a ação que ela deve executar quando o evento acontecer. O nome do evento são os nomes do eventos comuns do Javascript, como de 'click', 'input', 'focus', 'dblclick' entre outros.

```javascript
// exemplo aplicação das funcionalidades

// a class 'campo-digitacao' poderia, por exemplo, estar indicada em um formulário no documento HTML

var campoDigitacao = $('.campo-digitacao');

campoDigitacao.on('input', function(){
  console.log(campoDigitacao.val);
})
```
