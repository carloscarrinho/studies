# Curso de jQuery
## Plataforma Alura

### Introdução

#### O que é?
O jQuery é uma biblioteca que permite uma maior produtividade em projetos com o uso de JavaScript. Ele também auxilia na compatibilidade entre navegadores.

#### Versões
No site do jQuery podemos baixar três tipos de versões:

- 'Production': versão comprimida para uso no servidor de produção;
- 'Development': versão completa para o uso do desenvolvedor;
- 'Slim': versão mais leve que não contem suporte para AJAX e animações;

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