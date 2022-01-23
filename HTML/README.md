# HTML
 
1. [Semântica](#1)
2. [Tags](#2)
3. [Incluir arquivos](#3)
 
<a name="1"></a>
 
## Semântica
 
<a name="1.1"></a>
 
- [1.1](#1.1) Combine blocos não por sua localização visual, mas por seu significado.
 
  Mesclar blocos como este:  
  ![bom exemplo](http://image.prntscr.com/image/665a3fda6b3847e687c4ed5fdbbaec22.png)
 
  Não assim:  
  ![mau exemplo](http://image.prntscr.com/image/ ea6179004eb9493e90a4ceae4dad2a7c.png).  
  No mínimo, isso facilitará muito a adição de um novo elemento posteriormente, quando for necessário, a pedido do cliente, fazer uma folha de 4 elementos, e não três, como aqui. Além disso, a segunda abordagem é muito inconveniente se o conteúdo for gerado dinamicamente. Então, se você criar um layout que os clientes irão anexar ao back-end, e você fizer tal layout, as maldições de seus programadores e danos a todo o nosso carma são garantidos.
 
<a name="1.2"></a>
 
- [1.2](#1.2) Se houver algo como uma lista, verifique como ficará com mais elementos.
 
  ![Lista](https://rizzoma.com/r/files/a87a0a28b84d6326d4f3909e8801dab7-97a135d68ad6e2e449e9c9f2dbf9766c-0-0.6276249218551724)
 
  Se não estiver claro o que acontecerá com os 4 elementos, neste caso, não deixe de perguntar decidir por conta própria
 
<a name="1.3"></a>
 
- [1.3](#1.3) Todos os elementos com texto, cujo conteúdo é gerado dinamicamente, são verificados para que não quebrem com mais texto do que no layout.
 
  Nos nomes substituímos o famoso [Constantino de Constantinopla] (https://tema.livejournal.com/1322108.html).  
  O ideal é que os momentos difíceis de dimensionar com o texto possam ser encontrados na fase de conhecer o layout e fazer perguntas ao designer.
 
<a name="1.4"></a>
 
- [1.4](#1.4) Verifique se há erros nas páginas com o [validador W3C](https://validator.w3.org/#validate_by_uri). Se você quiser executar as páginas localmente, use a [extensão do navegador](https://chrispederick.com/work/web-developer/). Os avisos podem ser resolvidos conforme necessário com base nas condições do projeto.
 
  Erros comuns:
 
  <a name="1.4.1"></a>
 
  - [1.4.1](#1.4.1) Insere elementos de bloco dentro de elementos inline.
 
    Não `<span><div></div></span>`.
 
  <a name="1.4.2"></a>
 
  - [1.4.2](#1.4.2) Não se destina a ser expandido por outros arquivos por meio de algum mecanismo de modelo, arquivos de página .html não começam com `<!DOCTYPE html >`, que é contra o padrão HTML5.
 
  <a name="1.4.3"></a>
 
  - [1.4.3](#1.4.3) As tags de fechamento automático são usadas se suportarem outro modo.
 
    É proibido:
 
    ```html
    <div />
    <intervalo />
    ```
 
    Você pode:
 
    ```html
    <link />
    <img />
    <input />
    ```
 
  <a name="1.4.4"></a>
 
  - [1.4.4](#1.4.4) Nem todas as imagens `<img>` contêm o `alt` atributo.
 
  <a name="1.4.5"></a>
 
  - [1.4.5](#1.4.5) Existemaninhados formulários `<form>`.
 
  A lista completa de possíveis erros é descrita [aqui](https://validator.w3.org/docs/errors.html).
 
<a name="1.5"></a>
 
- [1.5](#1.5) Use h1..h6 apenas para títulos, e h1 deve aparecer apenas uma vez em uma página.
 
<a name="1.6"></a>
 
- [1.6](#1.6) Use `<table>` apenaspara tabelas reais.
 
  Se houver uma descrição de texto antes da tabela, faça-a dentro da tag `<table>` via `<caption>`.  
  Se a tabela tiver a primeira linha como cabeçalho, use `<thead>` e aninhado `<th>` para isso, e use "scope" para essas células.
 
  Exemplo:
 
  ```html
  <table>
    <caption>
      Primeiros dois presidentes dos EUA
    </caption>
    <thead>
      <tr>
        <th scope="col">Nome</th>
        <th scope="col">Tomou posse</th>
        <th scope="col">Festa</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>George Washington</td>
        <td>30 de abril de 1789</td>
        <td>n/ a</td>
      </tr>
      <tr>
        <td>John Adams</td>
        <td>4 de março de 1797</td>
        <td>Federalista</td>
      </tr>
    </tbody>
  </mesa>
  ```
 
<a name="1.7"></a>
 
- [1.7](#1.7) Não use `<br>` em nenhum lugar, exceto quando todos os requisitos forem atendidos:
 
  - Novas linhas são semanticamente significativas.
  - O recuo não é semanticamente significativo (caso contrário, você deve usar um `<pre>`).
  - Não existe nenhuma outra tag semanticamente apropriada, como uma tag de parágrafo ou de cabeçalho.
 
<a name="1.8"></a>
 
- [1.8](#1.8) Use tags semânticas.
 
  Você pode descobrir por que eles devem ser usados ​​[aqui](https://www.youtube.com/watch?v=bDYEnNzprzE) e [aqui](https://developer.mozilla.org/en/docs/Learn/ %D0 %94%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%BD%D0%BE%D1%81%D1%82%D1%8C/HTML).  
  [Fluxograma](http://html5doctor.com/downloads/h5d-sectioning-flowchart.pdf) para selecionar tags semânticas.
 
<a name="2"></a>
 
## Tags
 
<a name="2.1"></a>
 
- [2.1](#2.1) Todas as tags devem funcionar mesmo sem CSS e JS.
 
  Todos os textos que são visíveis inicialmente ao abrir a página também devem estar disponíveis, formulários devem ser enviados, links devem ser navegados (e links que não devem ser navegados e para os quais é costume definir `href="#"`, não deve ser usado, isso seguirá).
 
<a name="2.2"></a>
 
- [2.2](#2.2) A estrutura das tags deve vir principalmente do conteúdo, não do design
 
  ![exemplo](http://image.prntscr.com/image /a89c1aed00f14864851989caceacd59d .png) - por exemplo, esse elemento pode ser organizado como quatro elementos consecutivos: um ícone de mensagem, um crachá com o número 10, um ícone de avatar e um nome de usuário. Mas aqui é necessário combinar explicitamenteusando `<div>` dois blocospara que sejam semanticamente separados - um bloco com informações sobre a mensagem e um bloco sobre o usuário. Para css, você pode ter que escrever estilos extras, mas o layout será mais significativo e não será vinculado novamente ao design.
 
<a name="2.3"></a>
 
- [2.3](#2.3) Nãoantes de `<!DOCTYPE html>` deve haver caracteres, incluindo espaços e quebras de linha.
 
<a name="2.4"></a>
 
- [2.4](#2.4) Dentro de `<head>`, a primeira tag deve ser `<meta charset="utf-8">`.
 
<a name="2.5"></a>
 
- [2.5](#2.5) Cada página deve ter `title` tagse meta tags `keywords`, `description` (peça conteúdo ao gerente de conteúdo).
 
<a name="2.6"></a>
 
- [2.6](#2.6) Em `head` adicione `<meta name="viewport" content="initial-scale=1.0, width=device-width">` - on os navegadores móveis podem evitar a rolagem horizontal e dimensionar o conteúdo para a largura da tela inteira.
 
<a name = "2.7"> </
 
Todos os atributos devem estar entre aspas duplas
 
  não podem ser:
 
  ```html
  <img largura=200 />
  <div classe=bloco>
    <a href = '/ algum/url'
  
  ```
 
  Você pode:
 
  ```html
  <img largura="200" />
  <div classe="bloco">
    <a href = "/ algum / url"
  
  ```
 
  Além disso, se não houver outras convenções no projeto, os atributos devem ser nomeados com hífen em minúsculas (nomes apenas em letras minúsculas e hifenizados) e, se o valor for uma string e mostrar algum nome, então deve também ser hifenizado em minúsculas . Tente iniciar atributos personalizados com data- (essa é a prática padrão recomendada para HTML5).
 
  Exemplo: `<a href="/" data-index="33" data-page-name="main-page">Home</a>`
 
<a name="2.8"></a>
 
- [2.8](#2.8) Não use id a menos que seja semanticamente necessário.
 
  Quando sua exclusividade é garantida, por exemplo, no nível do banco de dados e quando você precisa:
 
  - fazer uma navegação funcional dentro de uma página (por exemplo, como na Wikipedia ou neste site de coleção [melhores práticas](https://isobar -idev.github .io/code-standards/#javascript_javascript)
  - vincular `<label>` e `<input />`, que estão em ramos completamente diferentes da árvore DOM (em geral, é sempre melhor apenas `< input />` dentro de `<label > `set,e então nenhum aydishniki não é necessário).
 
<a name="2.9"></a>
 
- [2.9](#2.9) Todas as tags vêm apenas com classes - semvazio `<div>`, `<section>` etc. uma compreensão clara do porquê. Isso impede muito que novas pessoas entrem no projeto e depois de um tempo você descobre seu próprio layout.
 
<a name="2.10"></a>
 
- [2.10](#2.10) Evite estilos inline e manipuladores de eventos em `html` o máximo possível (ou seja, não `<div onclick="func()">`).
 
<a name="2.11"></a>
 
- [2.11](#2.11) Não use links com umvazio ou inválido `href` (sem `<a href="#">`) - então é melhor usar um link stub para um URL inexistente que diz claramente que o link não está definido.
 
  Se você estiver configurando um projeto que possui páginas que não estão no design (por exemplo, elas serão criadas dinamicamente posteriormente ao integrar com o servidor), então é melhor colocar um endereço que diga claramente que este é um link de stub . Além disso, todos os links de stub devem ter o mesmo endereço dentro do projeto, por exemplo `<a href="/mock-address/change-me"></a>`.  
  Para SPA, às vezes você precisa gerar dinamicamente esses links com js (pelo menos em angular, existe até um atributo ng-href separado para isso), que daria suporte à geração dinâmica com base no roteamento puro do lado do cliente.  
  Não há necessidade de `<a href="#">` ou `<a href="javascript:someFunc(1)">`. Além disso, você não precisa salvar urls aqui antes dos métodos da API no servidor, esperando poder processar o clique com JS, enviar uma solicitação ajax para o servidor usando essa url e processar a resposta você mesmo. Isso não acontecerá se o usuário abrir o link em uma nova aba através do menu de contexto ou clicando com a roda do mouse, por exemplo. Todos os URLs especificados em `href`devem abrir conteúdo legível por humanos, que é totalmente dependente do servidor. [Último parágrafo original](https://isobar-idev.github.io/code-standards/#html_anchors_amp_links).
 
<a name="2.12"></a>
 
- [2.12](#2.12) Links para outros sites devem conter o atributo `target="_blank"`para abrir em uma nova janela.
 
<a name="2.13"></a>
 
- [2.13](#2.13) Todos os links com `target="_blank"` também devem conter o atributo `rel="noopener noreferrer"`.
 
  Isso se deve a [vulnerabilidade](https://mathiasbynens.github.io/rel-noopener/), segundo a qual o site que você abriu acessará o site de onde você veio através do `window.opener`, e isso até funciona domínio cruzado.
 
<a name="2.14"></a>
 
- [2.14](#2.14) Todas as entradas, seleções e outros elementos de formulário interativos devem estar dentro da tag `<form>`.
 
  ```html
  <form>
    <label>
      Nome:
      <input tipo="texto" nome="nome" value="João" />
    </label>
    <label>
      Sobrenome:
      <input tipo="texto" nome="sobrenome" value="Doe" />
    </label>
    <botão type="enviar"Enviar</botão>>
  </form>
  ```
 
<a name="2.15"></a>
 
- [2.15](#2.15) Todos os elementos interativos para os quais o designer pretendia uma ordem de campo não trivial devem ter o atributo `tabindex`envio, mais o botão deem tabindex deve sempre ser o último (respectivamente, se houver campos visuais sob o botão, eles devem ter tabindex e devem ser menores que o botão).
 
<a name="2.16"></a>
 
- [2.16](#2.16) Pergunte aos designers quais elementos focar automaticamente em qual página.
 
<a name="2.17"></a>
 
- [2.17](#2.17) Se o campo tiver um propósito claro, use o tipo apropriado (e-mail, número, cor etc.).
 
<a name="2.18"></a>
 
- [2.18](#2.18) Cada tag que pode conter texto deve ser verificada quanto a um grande número de caracteres.
 
  Todos os títulos e todas as tags com descrições de texto.  
  Verifique todas as entradas para que ao preencher o texto não seja pressionado perto da borda direita:  
  ![imagem](https://user-images.githubusercontent.com/12808495/55307777-c0e18e80-5482-11e9-927f-9c195d81555e.png)
 
<um name="2.19"></a>
 
- [2.19](#2.19) As tags inline clássicas devem ser apenas inline ou inline-block e não devem conter nada além de texto simples e outras tags inline.
 
  Exceções: `<a>` - às vezes você precisa fazer do link um elemento de bloco, mas é melhor usar inline-block.
 
<a name="2.20"></a>
 
- [2.20](#2.20) Para números de telefone, endereços de e-mail e apelidos do skype, use `<a>` com o endereço correspondente.
 
  ```html
  <a href="tel: +74951234567">+7 (495) 123-45-67</a>
  <a href="mailto: example@mail.ru">example@mail.ru</a>
  <a href="skype: someskype?call">someskype</a>
  ```
 
<a name="2.21"></a>
 
- [2.21](#2.21) Exibe exemplos de código por meio da tag `<code>`.
 
  Às vezes, em alguns projetos, você precisa mostrar exemplos de código para usuários diretamente no site (por exemplo, [aqui no tutorial do React](https://reactjs.org/) um monte de exemplos de código) - esses exemplos devem ser escrito em fontes monoespaçadas e diferir do texto normal - por padrão, é suficiente envolver o código em uma tag `<code>`.
 
<a name="3"></a>
 
## Incluir arquivos
 
<a name="3.1"></a>
 
- [3.1](#3.1) Todas as imagens, fontes, etc. devem ter um nome exclusivo dentro do projeto e não conter caracteres cirílicos. Se não houver convenções individuais no projeto, elas devem ser nomeadas no estilo hifenizado em minúsculas.
 
<a name="3.2"></a>
 
- [3.2](#3.2) O projeto deve ter um favicon.ico incluído em todas as páginas.
 
  Como fazer isso usando o webpack está muito bem escrito em [este artigo](https://medium.com/tech-angels-publications/bundle-your-favicons-with-webpack-b69d834b2f53).
 
<a name="3.3"></a>
 
- [3.3](#3.3) O Safari tem sua própria versão do favicon, ele também deve ser configurado.
 
  Ou seja, precisamos de svg para o contorno do ícone e precisamos de uma cor para o ícone ao passar o mouse. [Artigo](https://yoast.com/dev-blog/safari-pinned-tab-icon-mask-icon/).
 
<a name="3.4"></a>
 
- [3.4](#3.4) Execute imagens por meio de [kraken.io](https://kraken.io/) ou use seus utilitários CLI para fazer isso.
 
<a name="3.5"></a>
 
- [3.5](#3.5) Todas as fotos e imagens onde não houver transparência devem ser feitas em jpg.
 
<a name="3.6"></a>
 
- [3.6](#3.6) Ao cortar imagens do Photoshop, defina o DPI para 72dpi e salve a imagem em "Salvar para a Web".
 
<a name="3.7"></a>
 
- [3.7](#3.7) A largura máxima da imagem é 1920 pixels. Se for maior em layouts, reduza-o proporcionalmente.
 
  Na verdade, essa regra é discutível (pelo menos para telas de retina, não tenho certeza), mas siga-a até que o designer diga o contrário.
