# NODE JS

## O que é o Node JS


## Primeiros Passos com o Node JS
O primeiro passo para a utilização do Node obviamente é a sua instalação. Após esse passo, ele pode ser utilizado utilizando o comando ```node``` no terminal.

Supondo que temos um arquivo JavaScript chamado **olamundo.js** onde imprimimos no console uma mensagem 'Olá mundo!', podemos adicioná-lo para monitoramento do Node, através de ```node olamundo.js```.

```console
node olamundo.js

Olá mundo node!
```

## Criando o Servidor Web
O primeiro problema que temos que tratar na criação de um servidor é que precisamos de 'alguém' responsável por receber as requisições vindas do navegador, tratá-las e criar uma resposta a ser devolvida para o cliente. Para isso, o **Node** já disponibiliza, por padrão, um módulo que resolve este problema.

Podemos entender um **módulo** como uma biblioteca, um conjunto de funcionalidades que ajudará a resolver determinada tarefa.

No mundo Node, um arquivo qualquer .js _pode_ ser chamado de 'módulo'.

Para importar no código um módulo padrão já disponibilizado pelo Node, fazemos uso da palavra reservada ```require``` acompanhado de uma string informando qual é o módulo a ser importado:

```javascript
require('http');

```
Porém, só importar o módulo não é suficiente, precisamos ainda associar esse módulo à criação propriamente dita do servidor, através do método ```.createServer()``` (disponibilizado pelo módulo http importado). Para isso, no nosso exemplo, criamos uma constante ```const``` chamada **http**, vinculando-a ao módulo importado e depois associamos o método.

Para facilitar, podemos armazenar essa criação do servidor em uma outra constante chamada **servidor**.

Devemos, ainda, informar qual a porta que o servidor deverá 'escutar' as requisições. No mundo Node, normalmente, é utilizada a **porta 3000**. Fazemos isso por meio do método ```.listen(3000)```

```javascript
const http = require('http');

const servidor = http.createServer();

servidor.listen(3000);

```
Tudo lindo até aqui, porém o servidor não fez curso de mãe Diná para saber o que deve fazer sozinho. 

Portanto, devemos passar para o método ```.createServer()``` qual são as ações do ```servidor```. Esse método recebe como parâmetros a **requisição** e a **resposta**.

A **resposta** pode receber o método ```.end``` que indicará ao servidor o que ele deve retornar ao cliente após o recebimento da requisição.

```javascript
const http = require('http');

const servidor = http.createServer((req, resp) => {
    resp.end(
        `
        <html>
            <head>
                <meta charset="utf-8">
                <title>Casa do Código</title>
            </head>
            <body>
                <h1>Casa do Código</h1>
            </body>
        </html>
        `
    )
});

servidor.listen(3000);

```

## Instalando o Express
