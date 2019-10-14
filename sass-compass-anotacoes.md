# Curso de Sass e Compass - Descomplicando o CSS
## Plataforma Alura
### Introdução
As páginas web possuem uma estrutura padrão com a utilização de HTML, CSS e JavaScript.

- O HTML é responsável pela estruturação da página, com a criação dos elementos, botões, formulários, entre outros recursos;

- O CSS é aquele que responde pelo estilo, criando o layout, aplicando as cores, os efeitos _visuais_, o posicionamento dos elementos criados no HTML, efeitos de animação simples, responsividade para varios tamanhos de tela, entre outras coisas;

- O JavaScript é aquele que dá vida à página, criando as relações entre os elementos, os eventos de interação com o usuário, as validações de informações e muitas outras coisas.

Diante desses propósitos, especialmente o CSS e o JavaScript tendem a ser dinâmicos, isto é, podem ter a necessidade de mudar ao longo do tempo, por inserção/remoção de funcionalidades, mudança de layout, etc.

No JavaScript, quando o código foi feito de forma inteligente utilizando boas práticas, não é tão trabalhoso fazer modificações. Porém no CSS, mesmo que o código tenha sido bem estruturado, muitas vezes o código precisa ser alterado em vários pontos, gerando um certo retrabalho e necessidade de extrema atenção por parte do programador que está dando manutenção.

Para isso, foram criados alguns **Frameworks**, que são ferramentas de otimização do trabalho, para facilitar a criação e manutenção de códigos robustos.

O Sass é um pré-processador para trabalhar com o CSS que permite a criação de variáveis e [...] para facilitar e agilizar o trabalho.

### utilizando o Sass
Os arquivos criados em Sass utilizam a extensão .scss e precisam ser **compilados** para gerar o arquivo .css que vai ser aplicado na página.

Assim, a primeira coisa que devemos fazer é pedir para que ele compile o arquivo "estilos.scss" por meio do terminal. O primeiro passo é entrar na pasta do projeto (em que está o arquivo a ser compilado), depois compilamos o arquivo .scss para criar um .css, através do comando:

```console
sass estilos.scss:estilos.css
```
