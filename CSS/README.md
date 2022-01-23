# CSS
 
1. [Requisitos gerais](#1)
2. [Regras](#2)
3. [Fontes](#3)
4. [BEM](#4)
5. [Possíveis erros](#5)
 
<uma name="1"></a>
 
## Requisitos gerais
 
<a name="1.1"></a>
 
- [1.1](#1.1) Importante! Use [pixel-perfect](https://chrome.google.com/webstore/detail/perfectpixel-by-welldonec/dkaagdgjmgdmbnecmcefdhjekcoceebi?hl=en) se o cliente fornecer um layout.
 
<a name="1.2"></a>
 
- [1.2](#1.2) Não inclua estilos de fontes remotas - apenas de nossos servidores.
 
<a name="1.3"></a>
 
- [1.3](#1.3) CSS é uma força perigosa.
 
  Todos os estilos conectados à página são globais e, se isso for abusado, você poderá facilmente levar o projeto a um estado de introdução extremamente dolorosa de qualquer novo elemento ou alteração do antigo. Isso acontece com mais frequência quando classes "gerais" são criadas e anexadas a diferentes elementos da página (um exemplo banal é um cabeçalho que possui um formulário de pesquisa dentro, que está em todas as páginas com as mesmas classes) e, como resultado, quando, de acordo com o design, em páginas diferentes aparecem pequenas diferenças no cabeçalho, as classes que reescrevem as propriedades se multiplicam. E assim para quase todos os elementos de cada página. Como resultado, alterando o link mais à direita na barra lateral da página de notícias, você pode quebrar o layout de toda a barra lateral em alguma outra página, por exemplo, na página da conta pessoal.
 
  Para evitar que isso aconteça, existem diferentes metodologias, por exemplo, `BEM` (leia sobre isso pelo menos em termos gerais) ou, por exemplo, [rscss](https://rscss.io/index.html). Para começar, você pode estudar [uma pequena abordagem](https://isobar-us.github.io/code-standards/) que os caras do `Isobar` usam - está descrito dentro do padrão deles e consiste em 7 pequenos parágrafos.
 
<a name="1.4"></a>
 
- [1.4](#1.4) Recuo com espaços, um nível — 2 espaços.
 
<a name="1.5"></a>
 
- [1.5](#1.5) Use aspas simples.
 
<a name="1.6"></a>
 
- [1.6](#1.6) Antes de começar, certifique-se de conhecer claramente todas as prioridades do seletor e todos os 4 tipos de relacionamentos possíveis.
 
  As relações entre os elementos podem ser:
 
  - `div p` - elementos p que são filhos de div
  - `div > p` - apenas filhos imediatos
  - `div ~ p` - vizinhos à direita: todos p no mesmo nível de aninhamento que vêm depois de `div
  - div + p` -primeiro vizinho direito: p no mesmo nível de aninhamento, que vem imediatamente após div (se presente)
 
  quanto às prioridades podem ser lidas[aqui](https://habrahabr.ru/post/137588/ )e em muitos outros lugares.
 
<a name="1.7"></a>
 
- [1.7](#1.7) Não use `@import` dentro de arquivos.
 
  Isso significa que ofinal `css` arquivoque o cliente recebe não deve conter essas construções. Mas se `WebPack` e `css-loader` forem configurados, que trata apenas deste caso, ou análogos compilados são usados ​​que podem substituir o conteúdo direto de arquivos em vez de importações, então as importações são possíveis, já que o navegador não as verá de qualquer maneira e nunca os receberá em trabalho real.
 
  Existem algumas razões pelas quais você não deve usar `@import`:
 
  - Alguns navegadores mais antigos não suportam o uso da regra `@import`, e os estilos que carregamos através desta regra serão perdidos
  - `@import` blocoscarregamento paralelo de estilos, e isso significa que o navegador aguardará a conclusão do download do arquivo importado antes de processar o restante do conteúdo.
  - Mais detalhes podem ser encontrados [aqui](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/).
 
<a name="1.8"></a>
 
- [1.8](#1.8) Todas as regras devem ser divididas em arquivos diferentes por páginas e blocos, cada arquivo não deve ter mais de 1000 linhas.
 
<a name="1.9"></a>
 
- [1.9](#1.9) Cada regra CSS deve estar em sua própria linha.
 
  Isso ajudará muito, pelo menos ao visualizar diferenças no sistema de controle de versão. Além disso, evitará a rolagem horizontal.
 
<a name="1.10"></a>
 
- [1.10](#1.10) Para todos os elementos interativos (links, botões, dropdowns, inputs, selects), o designer pode desenhar estados separados e ocultá-los na camada mais próxima - sempre verifique para cada elemento, se há um estado renderizado.
 
<a name="1.11"></a>
 
- [1.11](#1.11) Designers podem cometer erros - às vezes você precisa fazer solicitações para alterar o layout se eles desenharam algo muito complicado.
 
  Por exemplo, um layout pode ter uma faixa centralizada verticalmente em relação ao texto:
 
  | ![Exemplo](https://user-images.githubusercontent.com/12808495/55335190-df687980-54c4-11e9-8623-13ecdb996ebc.png)  |
  | :------------------------------------------------- -------------------------------------------------- ----------: |
  |                       _essa foto é apenas um exemplo, não o fato de que existe apenas um erro_                    |
 
  O designer pode apenas colocar visualmente essa faixa no nível médio das letras inferiores do texto, no entanto, como designers de layout, basta aplicar vertical-align: middle e você verá que a faixa está acima/abaixo do nível que o design mostrou, e Pixel Perfect destaca isso claramente. Na maioria das vezes, você não precisa codificar algum recuo não óbvio, apenas para combinar perfeitamente com o layout - é melhor dizer ao designer que a tira é colocada automaticamente em um local diferente e é melhor deixá-la lá. Um designer para aprender tipografia.
 
<a name="1.12"></a>
 
- [1.12](#1.12) Tente tornar o site o mais fluido possível (defina a largura como uma porcentagem e defina max-width, min-width) - use um elemento fixo largura somente se o layout não tiver como fugir disso.
 
  Se você precisar de um site de largura fixa, verifique o lado direito de cada página em telas pequenas. Um erro muito comum iniciantes não fazem todos os elementos com min-width, e a rolagem horizontal é obtida assim:
  
   ![image](https://rizzoma.com/r/files/a87a0a28b84d6326d4f3909e8801dab7-60dd9b15a5f2c5e495726e74545edcae-0-0.7016728184648524)
 
- [1.13](#1.13) Ao construir um projeto na ausência de design (em estruturas CSS, por exemplo), evite "esculpir".
 
  Se você estiver desenvolvendo um projeto que não tem design (usando frameworks CSS, por exemplo), tente evitar a escultura.
 
  As regras são as mesmas que ao escrever módulos de programa: tente dar espaço entre os componentes, limite-os visualmente um do outro (o acoplamento fraco é realizado), mas, ao mesmo tempo, os próprios componentes devem parecer auto-suficientes, ou seja, tem todas as funcionalidades necessárias, mas sem redundância, para que possa ser chamado de componente completo (é realizada uma forte conectividade).
 
  O BEM é um bom detector aqui: tente recuar entre os blocos pelo menos duas vezes mais do que dentro do bloco entre os elementos.
 
<a name="1.14"></a>
 
- [1.14](#1.14) Todos os estilos de um bloco devem estar no mesmo lugar e classificados por ordem na página.
 
  Ou seja, se houver um cabeçalho e dentro dele houver um formulário de pesquisa, em arquivos .css você não poderá definir primeiro os estilos de cabeçalho, depois vários estilos de corpo de página e, em seguida, os estilos de formulário de pesquisa de cabeçalho. Os estilos do próprio cabeçalho devem ir, e logo abaixo dele, os estilos do formulário.
 
  Ao mesmo tempo, estilos de barra lateral não podem preceder estilos de cabeçalho e estilos de rodapé não podem preceder estilos de barra lateral. É melhor espalhar esses estilos em arquivos diferentes.
 
<a name="1.15"></a>
 
- [1.15](#1.15) O rodapé da página deve sempre ser pressionado na parte inferior da página, mesmo que haja pouco conteúdo na página ([5 maneiras de fazer isso](http://dimox.name/press_footer_bottom_with_css/)).
 
<a name="1.16"></a>
 
- [1.16](#1.16) Nomes.
 
  Use `minúsculas com hifenização` (ou seja, não`mySuperAwesomeElement` não `my_super_awesome_element`) Os
 
  nomes devem refletir o significado, ao invés da descrição dos estilos(`"carregando"`,não` "big-yellow-spinny-)
 
<a name="2"></a>
 
## Regras
 
<a name="2.1"></a>
 
- [2.1](#2.1) Não use `!important`.
 
  Em 99% dos casos, o problema pode ser resolvido usando `BEM`módulos CSS` ou `com sabedoria. Em casos raros difíceis, é melhor aumentar a prioridade dos seletores (por exemplo, quando você precisa redefinir estilos de biblioteca).
 
<a name="2.2"></a>
 
- [2.2](#2.2) Não use `position: absolute` para estilizar onde poderia ser substituído por outras abordagens.
 
<a name="2.3"></a>
 
- [2.3](#2.3) Não mova o elemento com `top`, `left`, `right` ou `bottom` quando `position: relative`, onde pode ser substituído por outras abordagens.
 
  Você pode usar o próprio `position: relative` (sem as propriedades `top`, `left`, `right` ou `bottom`) para o `z-index` e para dar um ponto de referência aos descendentes do elemento.
 
<a name="2.4"></a>
 
- [2.4](#2.4) Não use margens negativas.
 
  De fato,negativas `margin`s são regras válidas, elas são suportadas pela especificação `CSS`, e são usadas até mesmo por gigantes como Bootstrap (veja os estilos para `.row`).
 
  Mas essas são regras muito não óbvias, difíceis de detectar e quase sempre podem ser substituídas por propriedades mais fáceis e previsíveis.
 
<a name="2.5"></a>
 
- [2.5](#2.5) Evite fixar a altura.
 
  Quase sempre, usar uma fixa em pixels, porcentagens e outras unidades 'altura' é um sinal de código ruim. Isso torna o comportamento de elementos que seguem uma altura fixa muito obscuro, e o conteúdo pode ser recortado ou sobreposto em elementos subsequentes.
 
  Quando ainda pode ser necessário:
 
  - As alças do elemento devem ser ajustadas à altura dos descendentes que foram "retirados" do fluxo geral. Você pode "remover" do stream por meio de `position: absolute`, por exemplo. Este pode ser um slider, cujos descendentes giram apenas pelo posicionamento em vez de offset `margin`th
 
  - Por design, é necessário ajustar todos os elementos de uma certa altura e o conteúdo sai da borda, apara.
 
<a name="2.6"></a>
 
- [2.6](#2.6) Evite alinhamentos fixos.
 
  Se o bloco precisar ser centralizado (horizontal ou verticalmente), centralize-o dinamicamente em vez de um `margin-top` fixo.
 
  Por exemplo:
 
  ![Exemplo](https://user-images.githubusercontent.com/12808495/55335190-df687980-54c4-11e9-8623-13ecdb996ebc.png)
 
  Aqui a imagem, o texto e a faixa devem ser centralizados usando `vertical-align`e não `top: 55px` para a faixa.
 
  Muitas vezes, casos de centralização mais complexos aparecerão - quase todo mundo tem seu próprio método, você precisa estudá-los separadamente.
 
  [Artigo sobre alinhamento vertical](http://web-standards.ru/articles/vertical-align/)
 
  O que precisa ser feito para centralizar a altura de _element1_ dentro de _element2_:
 
  - Ambos os elementos devem ser quaisquer elementos embutidos
 
  - _element2_ deve têm o tamanho da fonte ou a altura da linha especificados. _Element2_ será centralizado apenas com base no tamanho da fonte ou na altura da linha e não se importará com a altura.
 
<a name="2.7"></a>
 
- [2.7](#2.7) Defina a cor de fundo padrão, cor da fonte, `font-size`font- efamily para `html`.
 
  A partir de agora, o tamanho da fonte será a referência para todos os elementos que usam rem para suas unidades de tamanho.
 
<a name="2.8"></a>
 
- [2.8](#2.8)se de observar a cor doao testar Certifique-`:visited` link.
 
  O navegador padrão torna esses links roxos, o que geralmente é inaceitável no design.
 
<a name="2.9"></a>
 
- [2.9](#2.9) Adicione um elemento `cursor: pointer`se for clicável e não for compatível por padrão.
 
<a name="2.10"></a>
 
- [2.10](#2.10) Remova todas as regras não utilizadas e regras que não afetem a exibição de forma alguma (por exemplo, propriedades padrão duplicadas ou null `margin`já, se não forem definido ) - eles podem posteriormente apresentar um comportamento não óbvio ao editar e, por causa deles, é difícil entender o projeto.
 
<a name="2.11"></a>
 
- [2.11](#2.11) Palavras totalmente maiúsculas devem ser preferencialmente feitas usando o estilo `text-transform: uppercase` em vez de digitar letras maiúsculas.
 
<a name="2.12"></a>
 
- [2.12](#2.12) Ao definir um elemento para `outline: none`, certifique-se de definir estilos para `:focus` nesse elemento.
 
  `outline` é muito útil quando o usuário preenche um formulário usando a tecla `tab` para alternar entre entradas e botões. Se `outline` for removido, ficará menos perceptível (ou até invisível para botões) qual elemento está selecionado no momento.
 
<a name="2.13"></a>
 
- [2.13](#2.13) Todos os usos de `@media` devem vir imediatamente após as regras principais do elemento, para que você possa ver todas as regras e todos os estados possíveis do elemento elemento em uma tela sem rolagem.
 
<a name="2.14"></a>
 
- [2.14](#2.14) Os prefixos do fornecedor devem vir antes do estilo genérico.
 
  A regra padrão deve estar sempre sob as regras específicas para cada motor.
 
  Exemplo:
 
  ``` css
  .thing {
    -webkit-transition: all 100ms;
    -moz-transition: all 100ms;
    -o-transition: all 100ms;
    transition: all 100ms;
  }
  ```
 
<a name="3"></a>
 
## Fontes
 
<a name="3.1"></a>
 
- [3.1](#3.1) Se o cliente forneceu layouts com fontes personalizadas, verifique se estão disponíveis e, caso não estejam, solicite os arquivos de fontes adquiridos.
 
<a name="3.2"></a>
 
- [3.2](#3.2) A menos que seja necessário suporte para navegadores mais antigos, as fontes devem estar nos formatos `.woff2`, `.woff`. Primeiro inclua `.woff2` fontes, depois `.woff` (exemplo abaixo).
 
<a name="3.3"></a>
 
- [3.3](#3.3) Se o projeto deve suportar caracteres não latinos (por exemplo, russo), verifique se o arquivo de fonte contém esses caracteres.
 
<a name="3.4"></a>
 
- [3.4](#3.4) Conecte diferentes estilos da mesma fonte com o mesmo nome, mas para diferentes pesos da`font-weight` e `font-style`.
 
  ``` css
  @font-face {
   font-family: "Lato";
   src: url("../fonts/lato-regular.woff2"), url("../fonts/lato-regular.woff");
   font-weight: 400;
   font-style: normal;
  }
  @font-face {
   font-family: "Lato";
   src: url("../fonts/lato-italic.woff2"), url("../fonts/lato-italic.woff");
   font-weight: 400;
   font-style: italic;
  }
  @font-face {
   font-family: "Lato";
   src: url("../fonts/lato-light.woff2"), url("../fonts/lato-light.woff");
   font-weight: 300;
   font-style: normal;
  }
  @font-face {
    font-family: "Lato";
    src: url("../fonts/lato-lightitalic.woff2"),
    url("../fonts/lato-lightitalic.woff");
    font-weight: 300;
    font-style: italic;
  }
  ```
 
<a name="3.5"></a>
 
- [3.5](#3.5) Sempre use pelo menos uma fonte de fallback e uma família de fallback.
 
  Eles são separados por vírgulas em `font-family`, então cada uso de `font-family` deve seguir o padrão:
 
  ``` css
  block {
   font-family: Helvetica, Arial, sans-serif;
  }
  ```
 
  Aqui `Helvetica` é uma fonte de plugin não padrão.
 
  `Arial` é a fonte padrão usada por quase todos os clientes, ela será usada senão incluir `Helvetica`.
 
  `sans-serif` é a família de todas as fontes sem serifa (que são `Helvetica`e `Arial`). Mesmo se não houver 'Arial-a' no computador, alguma fonte sans-serif padrão do sistema será instalada. A escolha aqui deve ser feita de `"serif,"` `"sans-serif,"` ou `"monospace"`. Para fontes sem serifa, use o padrão `Arial`, para fontes com serifa, `Georgia` (não `Times New Roman`fontes), e paramonoespaçadas, `"Courier New"`
 
<a name="3.6"></a>
 
- [3.6](#3.6) Nomes de fontes contendo espaços, números ou pontuação que não sejam hífens devem ser colocados entre aspas.
 
  Exemplo:
 
  ``` css
   block {
    font-family: 'Times New Roman', serif;
  }
  ```
 
<a nome="4"></a>
 
## BEM
 
<a name="4.1"></a>
 
- [4.1](#4.1) A nomenclatura das entidades BEM deve seguir as seguintes restrições:
 
  Bloco, elemento - sempre um substantivo (substantivo)
 
  Modificador - deve satisfazer as propriedades de [modificador do inglês](https://en.wikipedia.org/wiki/Gramatical_modifier). Sempre `adjetivo` ou `frase adjetiva`.
 
  Assim, frases em inglês `"$BLOCK_NAME [é] $MODIFIER_NAME"`, `"$ELEMENT_NAME [é] $MODIFIER_NAME"` ou `"$MODIFIER_NAME $BLOCK_NAME"`, `"$MODIFIER_NAME $ELEMENT_NAME"`, ` "$ ELEMENT_NAME WITH $MODIFIER_NAME $MODIFIER_KEY"` devem ser frases sintaticamente corretas.
 
  Exemplos de _nomes corretos_:
 
  - `input_selected` - ` entrada selecionada` - entrada selecionada ou `entrada selecionada`entrada selecionada -
  - `header_size_large` - `header with large size` - cabeçalho com tamanho grande.
 
  Exemplos de _**NÃO**nomes válidos_:
 
  - `form__`**_save_**`_small`, para o elemento save (que, por exemplo, é pendurado em um botão) - `small save` - save small, ` economize pequeno` - economize pouco. Seria correto usar um substantivo em vez de `verbo` e renomear o elemento para **_`save-button;`_** `pequeno` botão salvar- um botão salvar pequeno
 
  - `entrada_`**_focus_** - `entrada` foco de-foco ou entrada de`entrada é foco` - entrada é foco. É correto usar `adjetivo` em vez de `substantivo/verbo` e renomear o modificador para `focado; input_`**_focused_** - `focada` entrada- entrada focada
 
  - `row_`**_error_** - `linha`linha erro de- erro deou `linha é erro` - linha é um erro. É correto usar `frase adjetiva` em vez de `substantivo` e renomear o modificador para `com-erro`. `row_`**_with_**`-error` - `row with error` - linha com erro.
 
  Justificativa: sempre seremos capazes de interpretar a essência do elemento de layout e as propriedades que lhe são impostas de forma inequívoca e sem custos de energia desnecessários.
 
<a name="4.2"></a>
 
- [4.2](#4.2) Sempre fazemos o layout de acordo com o BEM, a arquitetura do layout deve ser baseada em componentes.
 
  Cada bloco deve estar em sua própria pasta.
 
  As pastas de bloco não podem ser aninhadas.
 
<a name="4.3"></a>
 
- [4.3](#4.3) Cada componente é um bloco separado da metodologia BEM.
 
<a name="4.4"></a>
 
- [4.4](#4.4) Cada componente deve ter apenas dependências explícitas, ser autocontido.
 
  Faça todas as dependências explicitamente importando no início do componente e inserindo-o no lugar certo no layout.
 
  Auto-suficiência significa que cada componente deve conter tudo o que é necessário dentro de si - todo o layout, todos os estilos e todos os scripts js.
 
  Não deve haver nada extra no componente:
 
  - Não deve haver definições de outros blocos dentro deste bloco
  - Não deve haver estilos que afetem outros blocos de alguma forma
  - Não deve haver estilos globais (por exemplo, em todos ostags ` span`)
  - O componente não deve afetar o `DOM` de outro componente (alterações de layout são estritamente proibidas)
 
<a name="4.5"></a>
 
- [4.5](#4.5) Personalize componentes apenas por meio de modificadores, sem mixins.
 
  Em quase qualquer projeto, há a necessidade de customizar os blocos. Por exemplo, há um layout de 20 páginas. Quinze dessas páginas têm cabeçalho, sendo que 10 delas têm cabeçalho azul, três delas cinza e duas transparentes. Isso significa que o componente de cabeçalho deve ser personalizável, e esse tipo de personalização é feito adicionando modificadores ao bloco, e não passando classes separadas com estilos.
 
  Vamos supor que a página promocional tenha um vídeo em segundo plano e, por design, precisamos fazer um cabeçalho transparente com uma fonte clara (escuro por padrão).
 
  Seriamente:
 
  ```pug
  .promo-page
    +header({ classname: 'promo-page__header' })
  ```
 
  Bom:
 
  ```pug
  .promo-page
    +header({ theme: 'transparent', font: 'light' })
  ```
 
  Com a abordagem correta, é claro, você precisará aprender como aceitar esses dois parâmetros, adicionar modificadores às classes necessárias e escrever regras para esses modificadores no CSS do componente.
 
  Esta regra foi introduzida após uma dolorosa experiência de manutenção de um projeto de média complexidade, e aqui estão os solavancos que são recheados com o uso de mixins:

  - O encapsulamento está quebrado - o uso de estilos externos dentro do componente leva a problemas de manutenção no futuro. O fato é que os estilos do componente são parte integrante dele e não devem afetar o que o cerca. O oposto também é verdadeiro - estilos externos não devem afetar o componente. Em outras palavras, o componente deve ser autossuficiente. Ao recorrer ao uso de estilos externos, criamos uma dependência entre dois estilos - externo e interno. Cada estilo precisa saber do que o outro é composto para que o estilo global não quebre o estilo do componente.   Esta é uma violação de encapsulamento.

  - Se um componente for usado em 20 páginas diferentes, depois de alterar uma propriedade no próprio componente, você terá que percorrer todas as 20 páginas manualmente e verificar se nada está quebrado, pois não se sabe quais estilos podem ser pendurados nos lugares de uso por meio de classes personalizadas, e você precisa verificar todas as combinações

  - Um aditivo geralmente é pendurado apenas no nível superior do componente, mas às vezes você precisa personalizar algo interno, então acontece que você precisa enviar e receber dois aditivos no componente, um aditivo para as propriedades do bloco inteiro , o segundo - para algum elemento, e quando você precisar de outro elemento para personalizar, terá que adicionar uma terceira impureza :)

  - Não será possível compilar claramente uma lista de todos os estados possíveis do componente, e ao abordar com modificadores, vemos claramente todos os parâmetros possíveis na entrada, e quando seu número sair da escala, podemos chutar o designer que ele está muito fantasiado e seria hora de passar para um único guia de estilo

<a name="4.6"></a>
 
- [4.6](#4.6) Você também não precisa usar mixes para posicionar o bloco no container pai - este problema é resolvido adicionando containers especiais.
 
  Digamos que haja um bloco pai, ele contém um bloco filho, que precisamos posicionar. Para posicionar o bloco interno, criamos um elemento wrapper no elemento pai e simplesmente configuramos as propriedades (_margin, padding, position_ etc) para este container. Assim, o posicionamento do bloco fica no arquivo do bloco pai e não afeta os estilos do próprio bloco.
 
  Este método permite que você posicione o bloco filho sem usar mixagens.
 
  Por exemplo, no cabeçalho temos um botão azul normal, mas aqui mesmo, no cabeçalho, ele deve estar recuado do lado esquerdo, para isso adicionaremos `div.header__button`:
 
  ```pug
   div.header
     div.header__button
       +button({ color:blue })
  ```
 
  E nos estilos de cabeçalho, basta adicionar:
 
  ``` css
  .header__button {
    margin-left: 3rem;
  }
  ```
 
<a name="5"></a>
 
## Possíveis erros
 
> Existem algumas regras muito não óbvias em CSS, é melhor estudá-las na teoria com antecedência do que quebrar a cabeça por horas por que o layout vai
 
<a name="5.1"></a>
 
- [5.1](#5.1) A margem superior do primeiro elemento empurra todos os pais para baixo.
 
  Digamos que a visualização desejada seja assim:
 
  ![image](https://user-images.githubusercontent.com/12808495/55340918-d92bca80-54cf-11e9-9701-eed499af7a05.png)
 
  Para que o título seja recuado da borda superior, adicionamos margem a ela: 20px 0 0; no entanto, temos este comportamento:
 
  [imagem](https://user-images.githubusercontent.com/12808495/55340961-f52f6c00-54cf-11e9-8506-09894ce1988e.png)
 
  !      seus pais também se mudaram:
 
  ![imagem] (https://user-images.githubusercontent.com/12808495/55341005-0a0bff80-54d0-11e9-8ac2-1ca16dbc40a3.png)
 
<a name="5.2"></a>
 
- [5.2](#5.2) Os pais ignoram todos os filhos que têm `float: left` ou `float: right`
 
<a name="5.3"></a>
 
- [5.3](#5.3) A propriedade `z-index` só funciona em elementos que têm um valor de posição de `absolute`, `fixed` ou `relative`.
 
<a name="5.4"></a>
 
- [5.4](#5.4) E z-index` Você também pode afetar ` sobre isso [aqui](https://habrahabr.ru/post/166435/).
 
<a name="5.5"></a>
 
- [5.5](#5.5) `height` como porcentagem não funciona se a altura do pai for derivada do conteúdo.
 
  Em `learn.javascript.ru` existe até um [artigo](https://learn.javascript.ru/height-percent) .
 
<a name="5.6"></a>
 
- [5.6](#5.6) Verifique cuidadosamente todos `:hover` em dispositivos móveis em uma ordem separada se o projeto for compatível com telas móveis.
 
  Em diferentes navegadores, os hovers se comportam de maneira diferente e isso deve ser acordado com os designers separadamente - às vezes, para que funcione, você precisa, por exemplo, fazer um toque separado no elemento. Assim, para que o clique funcione, você precisa tocá-lo duas vezes, o que também será muito estranho para alguns elementos.
 
<a name="5.7"></a>
 
- [5.7](#5.7) Pseudo-elements (`::after/before`) [não funciona](https://stackoverflow.com/questions/14585070/css-after-pseudo-element-not-showing-up-on-img/14586588#14586588) com `tags de fechamento automático` (`<img />`, `<input />`, etc.).
 
<a name="5.8"></a>
 
- [5.8](#5.8) Não use um simples :hover para exibir novos elementos que não são fáceis de alcançar com o mouse.
 
  Menus suspensos implementados através da `:hover`, não apenas este menu é praticamente inoperável em um dispositivo móvel, mas também causa muitas dores de cabeça para usuários de desktop. A solução neste caso é usar JavaScript.
 
  ![imagem](https://habrastorage.org/files/45f/aa7/1eb/45faa71eb7e74d3b8c39773cd181f298.gif)
 
<a name="5.9"></a>
 
- [5.9](#5.9) Em alguns navegadores (Chrome, Opera, Edge, Firefox 62-, Safari 10-), tags de formulário como `button`, `fieldset` e ` legend`não pode se tornar contêiner flexível.
 
  possível solução é usar um elemento wrapper dentro da tag (por exemplo, `span class="button__text"` dentro de um botão), e já definir a `display: flex`:
 
  ```html
  <button class="botão">
    <intervalo class="button_text">...</span>
  </button>
  ```
 
  ``` css
  .button_text {
    display: flex;
    ...;
  }
  ```
 
  Você pode ler mais sobre este e outros bugs que ocorrem ao trabalhar com flex em [Flexbugs](https://github.com/philipwalton/flexbugs).
 
  Para resolver problemas com flex, você pode usar um bom [postcss-plugin] (https://github.com/luisrudge/postcss-flexbugs-fixes), que corrige automaticamente alguns bugs na escrita de estilos para flex.
