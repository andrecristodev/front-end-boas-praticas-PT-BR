#js

1. [Boas Práticas](#1)
2. [Nomeação da variável](#2)
3. [Nomeação da Função](#3)
4. [Bibliotecas](#4)
5. [JQuery](#5)
6. [React](#6)
7. [Desempenho](#7)
8. [Arquitetura](#8)
9. [Segurança](#9)

<a name="1"></a>

## Boas práticas

<a name="1.1"></a>

- [1.1](#1.1) A legibilidade é fundamental

  Qualquer solução deve, antes de tudo, ser compreensível e dividida em partes lógicas para que outros membros da equipe possam entender não apenas o propósito do código, mas também as soluções aplicadas sem reservas adicionais.

<a name="1.2"></a>

- [1.2](#1.2) Tudo o que pode ser escrito em puro html + css dentro do framework das propriedades que os navegadores declarados fornecem - deve ser escrito sem usar JS.

  > _Esta regra não deve contradizer o parágrafo anterior_

  Esta é uma regra muito importante porque:

  - Muitas vezes, o uso excessivo de scripts engana outros desenvolvedores, principalmente quando, no meio do trabalho, o script altera repentinamente algumas propriedades do elemento.

  - Reduz o desempenho da aplicação web.

  - Via de regra, o código escrito em html + css é muito mais fácil de mudar.

  Se a implementação da funcionalidade em html + css for possível apenas com o uso de vários hacks, já vale a pena mudar para JS para que a manutenibilidade do projeto não caia

<a name="1.3"></a>

- [1.3](#1.3) Evite dependências críticas implícitas.

  Às vezes, as tarefas podem surgir em um projeto, resolvendo o que você torna o sistema vulnerável a uma queda, em vez de um hack. Um exemplo da vida real é o cálculo do valor de um pedido em um cliente. Como nenhum cálculo no cliente pode ser confiável (afinal, qualquer pessoa pode enviar um preço diferente com uma simples solicitação HTTP), você precisa fazer um código separado no servidor e rejeitar o pedido se os valores não corresponderem. Idealmente, isso deve ser evitado ao máximo, mas se ainda for necessário deixá-lo no projeto, é necessário tornar a solução o mais segura possível (prever todos os casos de quedas, corrigi-los e notificar o administradores se algo deu errado) e generosamente regue com comentários e testes.

  O segundo exemplo seria quando você confia em algo de um banco de dados em seu código. Se não houver tais valores no banco de dados e seu sistema travou - 99% é culpa sua, mesmo que o preenchimento desse tipo específico de dados fosse o dever sagrado dos administradores que erraram.

<a name="1.4"></a>

- [1.4](#1.4) Conheça e use o guia de estilo do AirBnB.

  Ele está localizado [aqui](https://github.com/airbnb/javascript).

  Existem traduções para ele, inclusive em russo, mas você precisa ler o original, pois os recursos do ES6 são descritos lá. Tudo o que está listado no guia é aceito para execução, se não estiver bloqueado pelas nossas regras abaixo.

<a name="1.5"></a>

- [1.5](#1.5) Use `eslint` ou similar.

<a name="1.6"></a>

- [1.6](#1.6) Métodos.

  **Nome**:

  O nome do método deve ser `autodescritivo`. A partir do nome, deve ficar claro para que serve o método e o que ele faz. Não deve haver razão para pensar em sua implementação interna.

  **Parâmetros**:

  Se você precisar passar muitos parâmetros para um método, combine-os em um objeto. Por exemplo, você tem um método que desenha um retângulo, com as coordenadas do ponto, largura, altura, cor, espessura da borda e outros parâmetros. Neste caso, será mais fácil passar um único objeto 'options'. Isso removerá a obrigação de ter em mente todos os parâmetros, bem como sua ordem, e nos permitirá criar convenientemente muitas propriedades com valores padrão.

  No caso em que os parâmetros são passados ​​por um objeto, é preferível obter seus valores usando a desestruturação.

  Se o parâmetro for opcional, ele deve receber um valor padrão.

  **Corpo**:

  Respeite o princípio da Responsabilidade Única. O método deve realizar apenas uma tarefa (por exemplo, o método `createReport`, que cria um relatório e o envia ao servidor, deve ser dividido em dois: `createReport` e `sendReport`).

  O método deve ser compacto. Normalmente, o comprimento do método varia entre 10-40 linhas. Isso não significa que seu método precisa estar dentro desse escopo, mas se seu método tiver 200 linhas, vale a pena considerar se ele pode ser dividido em vários métodos separados. Você pode ler sobre a compactação dos métodos em S. McConnell “Código Perfeito” e R. Martin “Código Limpo”. Também [aqui](https://softwareengineering.stackexchange.com/questions/133404/what-is-the-ideal-length-of-a-method-for-you) Boa discussão sobre tamanhos de métodos.

<a name="1.7"></a>

- [1.7](#1.7) Mantenha os tempos de vida das variáveis ​​o mais curtos possível.

  A declaração da variável deve estar perto de onde é usada. Isso lhe dá uma compreensão mais rápida do que está acontecendo em seu código, além de menos chance de a variável ser mal utilizada ou sobrescrita.

  Mais detalhes sobre o tempo de vida de uma variável podem ser encontrados em "Código Perfeito" de S. McConnell.

botão.

  Esta é uma regra de UX muito importante que muitas vezes é ignorada pelos iniciantes. Mais uma vez: não pendure o processamento de preenchimento do formulário no evento `click` do botão, mas pendure-o no evento `submit` do formulário. No mínimo, o `submit` de um formulário pode ser chamado de maneiras adicionais - por exemplo, pressionando enter em qualquer `input` e cometendo um erro, você viola seriamente o UX de todo o site.

<a name="1.9"></a>

- [1.9](#1.9) Todas as verificações contendo mais de uma condição devem ser aprovadas.
  Retire para uma unidade arquitetônica separada - uma variável ou uma função.

  Seriamente:

  ```javascript
    if ((this.allowUpdate) && ((user.isAdmin) || (user.role === item.owner)) {
      this.update(item.dados);
    }
  ```

  Boa:

  ```javascript
    function isUpdateAllowedForUser(usuário, item) {
      return (this.allowUpdate) && ((user.isAdmin) || (user.role === item.owner);
    }
    //.. no lugar certo
    if (this.isUpdateAllowedForUser(usuário, item)) {
      this.update(item.dados);
    }
  ```

  Também é bom (um exemplo de código de ramificação com várias condições, onde tudo é nomeado e disperso e, portanto, compreensível)

  ```javascript
    const isTodayRequested = dia === 'hoje';
    const isTomorrowRequested = dia === 'amanhã';
    const isDepartTomorrow = partida.dia() !== agora.dia() && unix(partida) unix(agora);
    const isDepartToday = partida.dia() === agora.dia();
    const isRequestedDayIncorrect = (isDepartToday && !isTodayRequested) || (isDepartTomorrow && !isTomorrowRequested);
    const resultado = isRequestedDayIncorrect ? getAnteriorDia(dia): dia;
  ```

  A remoção de condições e sua disseminação por diferentes funções/variáveis ​​permite que cada condição receba um nome humano e então seus colegas podem ler convenientemente todas as relações lógicas não em uma cifra, mas de uma forma conveniente, quase como um texto literário.

<a name="1.10"></a>

- [1.10](#1.10) Sempre evite a conversão implícita em JS.

  Em nossa linguagem favorita, você pode adicionar arrays com strings, objetos com números e assim por diante. Mas, claro, você não precisa fazer isso. Sempre converta explicitamente as variáveis ​​para o mesmo tipo ao adicioná-las, subtraí-las, dividi-las e multiplicá-las.

  Seriamente:

  ```javascript
    const lifes = [true, false, false, true, true];
    aliveTotal = 0;
    for (let i = 0; i < lifes.length; i++) {
      aliveTotal += lifes[i]; // aqui adicionamos um elemento de array ao número, que é booleano.
    }
  ```

  O pior é que esse código funcionará, mas tudo é muito vulnerável nele e para mantê-lo, você deve ter em mente constantemente que existem bolas com números somados.

<a name="1.11"></a>

- [1.11](#1.11) Não altere os protótipos de construtores padrão (por exemplo, `String.prototype` ou `Function.prototype`) até que o assunto tenha sido cuidadosamente examinado e o truque acordado com um desenvolvedor sênior.

<a name="1.12"></a>

- [1.12](#1.12) O construtor da classe deve ser o mais leve possível.

  Por exemplo, se você quiser pesquisar na árvore DOM para definir valores para campos de classe, precisará mover essa funcionalidade para um método separado. Além disso, se você precisar definir manipuladores de eventos - em um método separado.

<a name="1.13"></a>

- [1.13](#1.13) Mova manipuladores de eventos para funções separadas.

  Você não deve criar funções anônimas exatamente no mesmo local onde o evento está vinculado.

  Seriamente:

  ```javascript
  elem.addEventListener("clique", function() {
    alert("Obrigado!");
  });
  ```

  Boa:

  ```javascript
    class Component {
      bindEventListeners() {
      topButton.addEventListener("click", this.handleStopButtonClick);
    }

    handleStopButtonClick() {
     // ...
    }
   }
  ```

<a name="1.14"></a>

- [1.14](#1.14) Nos handlers, não trabalhe com o contexto (this), mas com o argumento do objeto de evento, que foi passado de cima.

  Não confie nisso ao trabalhar com objetos de evento, mas use o primeiro parâmetro do retorno de chamada do evento.
  Trabalhe apenas com o que vem do evento. JS permite adicionar dados adicionais ao evento.
  Ou seja, não use "this.value". Em vez disso, receba dados por meio do objeto de evento "e.currentTarget.value".
  Seriamente:

  ```javascript
  handleButtonClick() {
   const buttonWidth = $(this).width();
   // ...
  }
  ```

  Boa:

  ```javascript
  handleButtonClick(evento) {
   const buttonWidth = $(event.currentTarget).width();
   // ...
  }
  ```

<a name="1.15"></a>

- [1.15](#1.15) Tente evitar loops o máximo possível e use métodos de array integrados.

  `.map`, `.filter` e assim por diante são geralmente muito mais fáceis de ler, além da função de processar um elemento que pode ser retirado e reutilizado em diferentes lugares.

<a name="1.16"></a>

- [1.16](#1.16) Não use literais da lógica de negócios diretamente - você precisa criar um objeto com constantes.

  Se houver algum parâmetro na lógica de negócios, você precisará criar uma variável em algum lugar, de preferência em um local especial para a configuração, colocar todos os valores fixos lá e usá-los apenas pelo nome no código .

  Lata:

  ```javascript
   if (status === ordersModule.ACTIVE_STATUS) {...}
  ```

  É proibido:

  ```javascript
    if (status === 'active') {...}
  ```

<a name="1.17"></a>

- [1.17](#1.17) Formatando o posicionamento das importações.

  As importações são combinadas em seções, as seções são separadas por uma quebra de linha.
  Três seções são alocadas para a frente (nesta ordem de colocação):

  - Importações absolutas de node_modules;
  - Importações absolutas de src;
  - Importações relativas, classificadas em ordem decrescente de saltos na árvore de caminhos (via ../).

    Por exemplo:

  ```javascript
    import * as React from "react";
    import block from "bem-cn";
    import { connect, Dispatch } from "react-redux";
    import { bindActionCreators } from "redux";
    import { arrayPush } from "redux-form";

    import { Modal } from "shared/view/elements";
    import { IPreset } from "shared/types/models";
    import { IAppReduxState } from "shared/types/app";
    import { actions as notificationActions } from "services/notification";
    import { selectors as configSelectors } from "services/config";

    import { actions, selectors } from "../../../redux";
    import { managePresetsFormEntry } from "../../../redux/reduxFormEntries";
    import { Presets } from "../../components/ManagePresets";
    import "./ManagePresets.scss";
  ```

  Além disso, para qualquer subárvore de um elemento de caminho, não deve haver uma subárvore cujas importações sejam compartilhadas por outra subárvore de mesma profundidade.
  Por exemplo:
  As importações da subárvore `shared` (profundidade 1) são compartilhadas pelas importações da subárvore de serviços.

  ```javascript
    import { IModel } from "shared/types/models";
    import { i18nConnect } from "services/i18n";
    import { Component } from "shared/view/components";
  ```

  Estará correto assim:

  ```javascript
    import { IModel } from "shared/types/models";
    import { Component } from "shared/view/components";
    import { i18nConnect } from "services/i18n";
  ```

  Ou em:

  ```javascript
    import { IAppReduxState } from "shared/types/app";
    import { Component } from "shared/view/components";
    import { IModel } from "shared/types/models";
    import { i18nConnect } from "services/i18n";
  ```

  As importações de subárvore `shared/types` (profundidade 2) são separadas por importações de subárvore `shared/view`. Estará correto assim:

  ```javascript
    import { IAppReduxState } from "shared/types/app";
    import { IModel } from "shared/types/models";
    import { Component } from "shared/view/components";
    import { i18nConnect } from "services/i18n";
  ```

<a name="1.18"></a>

- [1.18](#1.18) Mantenha as exportações no final do arquivo.

  Seriamente:

  ```javascript
    export class Foo {
      // ...
    }
    export class Bar {
     // ...
    }
  // a comédia acaba
  ```

  Boa:

  ```javascript
    class Foo {
      // ...
    }
    class Bar {
      // ...
    }
    export { Foo, Bar };
  ```

<a name="1.19"></a>

- [1.19](#1.19) Em caso de dúvida se um navegador suporta um recurso, verifique se o recurso está definido diretamente, em vez de comparar `user-agent` com os nomes e versões dos navegadores que o suportam de acordo com a documentação. E para o bem, geralmente use [Modernizr](https://modernizr.com/).

<a name="1.20"></a>

- [1.20](#1.20) Evite variáveis ​​globais.

  Em quase qualquer idioma, as variáveis ​​globais são a fonte do mal. Em JavaScript, essa regra não é exceção.

  Variáveis ​​globais tornam o programa imprevisível e dificultam o aprendizado da lógica do código, além de causar tontura e gritos de raiva em desenvolvedores experientes quando aparecem.

  Na maioria das vezes, você pode usar variáveis ​​globais apenas porque as bibliotecas antigas exigem, por exemplo, o Google Maps, que cria um objeto global do google e os mapas só podem ser personalizados por meio dele e solicita um retorno de chamada para criar uma função global em seu início, que o Google Maps então se chamará .

  Você pode usar uma (e apenas uma) variável global nos primeiros estágios de projetos muito simples, onde existem algumas animações em jquery, para salvar módulos nela e poder acessar funções de outros arquivos js (o próprio js não suporta isso por padrão).

<a name="1.21"></a>

- [1.21](#1.21) Acesse as variáveis ​​globais apenas como propriedades da janela.

  E criar objetos apenas como propriedades de janela, pois a declaração sem var não é óbvia - as variáveis ​​também são redefinidas a partir do fechamento e é difícil distinguir esses pontos.

  ```javascript
  // aqui a regra é violada, uma variável global é criada sem janela, e o acesso a ela também é sem janela:
  function test() {
    foo = "olá mundo"; // note que a variável foi criada sem var, então ela é global
  }
  test();
  console.log(foo); // saída 'olá mundo', chama também sem janela
  ```

  ```javascript
  // isso é seguido pela variável global declarada, como deveria:
  function test() {
    window.foo = "olá mundo";
  }
  test();
  console.log(window.foo); // saída 'olá mundo', acessada como uma >propriedade do objeto window
  ```

<a name="1.22"></a>

- [1.22](#1.22) Use wrappers personalizados para log, não `console.log` bruto.

  Geralmente logado. ou seja, é uma arte por si só, boas regras foram descritas em [esta apresentação](https://www.slideshare.net/nzakas/enterprise-javascript-error-handling-presentation/2-Whos_this_g_uy_P).

  Cada log deve ter um prefixo que diga de qual módulo o log foi chamado e em que momento foi chamado (timestamp);

  Separe o log em pelo menos dois níveis - `debug` e `production`, para que os logs dos desenvolvedores não sejam exibidos no assembly de produção;

  Todos os logs que seu sistema produz devem ser armazenados em uma única variável para que em caso de erros você possa enviar tudo imediatamente para o servidor.

  <a name="1.23"></a>

- [1.23](#1.23) O código antigo deve ser removido, não comentado. Se você precisar dele no futuro, você sempre pode olhar no histórico de commits.

  Isto destina-se principalmente aos seus colegas - grandes pedaços de código redundante são confusos, interferem na pesquisa através de `ctrl+F`, às vezes fazem com que você se distraia estudando o código. Portanto, é melhor escondê-lo no histórico de alterações.

<a name="1.24"></a>

- [1.24](#1.24) Todas as mudanças de estilo que podem ser feitas alternando classes em um elemento devem ser feitas adicionando/removendo classes, não estilizando elementos DOM. Assim, por exemplo, você pode alternar a visibilidade de um elemento. No entanto, para alterar continuamente os valores numéricos, isso não funcionará mais, como, por exemplo, ao alterar a propriedade `top` ao rolar a página, então aqui você ainda precisa colocar o valor diretamente no elemento na propriedade css.\ *\*;

  Isso não apenas aumentará o desempenho (porque você aplicará todos os estilos da nova classe de uma só vez), mas também ajudará você a reescrever os estilos do css de maneira normal, porque senão os estilos serão embutidos e não poderão ser redefinidos de css, exceto por meio de `! importante`.

<a name="1.25"></a>

- [1.25](#1.25) É muito útil entender como os ciclos de redesenho do navegador funcionam e como você pode verificar e melhorar o desempenho do DOM - aqui no artigo [fontes úteis] estão listadas (https://isobar-us.github.io/code-standards/#javascript_javascript_performance).

<a name="1.26"></a>

- [1.26](#1.26) O código deve estar livre de erros de ortografia. Nomes de variáveis, funções, comentários devem ser escritos corretamente.

  Normalmente, para evitar a maioria dos erros, são usadas extensões para `IDE`, para `vscode` por exemplo existe uma boa extensão [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code- corretor ortográfico).

<a name="1.27"></a>

- [1.27](#1.27) Todo o trabalho com serviços do navegador (`navigator services`, `cookie`, `localStorage`) deve ser encapsulado em try/catch, porque estes são serviços externos ao nosso código, dos quais não está claro o que esperar. Você não deve confiar em especificações aqui, porque. há também novos motores que têm, entre outras coisas, bugs em seus tipos.

  No safari, se o modo de navegação anônima estiver ativado, ou se o navegador tiver um bloco de `cookie`, o navegador gerará um erro. Portanto, se você não pegá-lo, o aplicativo desmoronará :)

<a name="1.28"></a>

- [1.28](#1.28) Não estenda classes padrão como Array, Error, Map e outras porque aqui está [por que](https://github.com/Microsoft/TypeScript/wiki/Breaking-Changes#extending- built- ins-like-error-array-and-map-may-no-mais-work)

<a name="2"></a>

## Nomenclatura de variáveis

<a name="2.1"></a>

- [2.1](#2.1) Nomeie as variáveis ​​de acordo com o significado.

  O nome da variável deve descrever completa e precisamente a entidade e sua finalidade.

  Significa não usar data, resultado, array como nomes. Por exemplo, para a data atual, é melhor usar a variável hoje, não a data, para uma lista de alunos, os alunos é melhor que o array.

<a name="2.2"></a>

- [2.2](#2.2) Tente não dar nomes muito longos às variáveis.

  Como regra, cerca de três palavras (10-15 caracteres) são suficientes para revelar o significado de uma variável. Variáveis ​​são sempre usadas em algum contexto, do qual alguns detalhes podem ser omitidos. Por exemplo, um objeto de classe de controle deslizante pode conter um campo de intervalo que contém o intervalo do controle deslizante. Não há necessidade de nomear este campo como `sliderRange`, pois é óbvio que isso se refere ao controle deslizante. Nomes longos tornam o código mais difícil de ler e só devem ser usados ​​quando um nome mais curto for ambíguo e contiver muito pouca informação (dado o contexto discutido acima) para fazer sentido.

<a name="2.3"></a>

- [2.3](#2.3) Use `camelCase` ao nomear variáveis, pois é aceito pela comunidade JavaScript.

  Se os dados que vêm "de fora" (por exemplo, do backend) não estão no formato `camelCase` (`snake_case` ou qualquer outro), faz sentido normalizar as chaves para consistência.
<a name="2.4"></a>

- [2.4](#2.4) Dê nomes de variáveis ​​​​booleanas que assumem valores `true` ou `false`.

  Os prefixos usados ​​no início das variáveis ​​são: `is/is`, `has`, `with`. Algumas vezes o nome de uma variável `boolean` pode ser formulado como uma declaração: `selectedColsWereChanged`, o que tornará o código mais legível e compreensível.

  `` Javascript
  if (SelectedColswerchanged) {// Something ...}
  ``

  Por outro lado, ninguém limita você a uma coleção de outras construções em inglês: `Will, Should, etc.`. que querem expressar em código. Também existe um caso assim: alguns nomes não precisam de informações adicionais que mostrem que é `booleano` (seja de acordo com o idioma afetado, ou historicamente): `pened, hidden, disabled, etc.`. Em geral, aprenda inglês para expressar corretamente seus pensamentos e códigos :) Assim você não precisará se lembrar de todas essas coisas e ficará claro por que de uma forma ou de outra

<a name="2.5"> </a>

- [2.5] (# 2.5) Use a forma aplicada de construções booleanas.

  Nomes baseados em rejeição (como notFound` `, ` ` e notdone` notSuccessful`) tornam-se menos óbvios ao tomar a decisão,

  por exemplo: ``` javascript
  if (not notFound) {..}
  `` `

  nomes expostos devem ser substituído em `found`, `done` e `processingComplete`, fazendo negação de variável no caso de nadis. Então você usou `found` em vez de `not not Found` para verificar o valor necessário.

<a name="2.6"></a>

- [2.6](#2.6) contém variáveis ​​explicativas.

  Ruim:

  ```javascript
  const address = "Um loop infinito, Cupertino 95014";
  const cidadeZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
  saveCityZipCode(
    address.match(cityZipCodeRegex)[1],
    address.match(cityZipCodeRegex)[2]
  );
  ```

  Bom:

  ``` javascript
  const address = "Um loop infinito, Cupertino 95014";
  const cidadeZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
  const [_, cidade, CEP] = address.match(cityZipCodeRegex) ?? [];
  saveCityZipCode(cidade, CEP);
  `` `

<a name="2.7"> </a>

- [2.7] (# 2.7) o nome de uma constante deve caracterizar uma entidade abstrata que implica uma constante, não um valor concreto.

  Por exemplo, quantidade, você precisa de uma constante representando dias úteis:

  bad: `Five`  
   good:` work_days.`

<a name="3"> </a>

## Nomeação de funções

<a name ="3.1"> </a> a>

- [3.1] (# 3.1) Todos os nomes de funções, com raras exceções (por exemplo, investigação de um acordo já estabelecido dentro de alguém) devem iniciar a biblioteca com verbos.

<a name="3.2"> </a>

- [3.2] (# 3.2) Funções de ordem superior que retornam funções make devem ser nomeadas após o padrão + \ + substantivo verbal, onde \* -. conjunto opcional e sintaticamente correto de palavras que esclarecem as funções de cura.

  Exemplo: `makeButtonClickHandler`.

<a name="3.3"></a>

- [3.3](#3.3) Manipuladores de eventos.

  Os eventos são entendidos não apenas como o evento DOM do vestido, mas também alguns eventos abstratos que são processados ​​usando callbacks, como a janela modal onClose` `` onLogin` ou o formulário de login):

  - Componentes Props-React relacionados ao tratamento de eventos devem ser nomeados de acordo com o padrão `onEventName`, onde `EventName` é o nome do evento tratado.

  - Manipuladores de eventos para elementos BEM, bem como para componentes aninhados em elementos BEM, são nomeados após `handleElementNameEventName`, onde `ElementName` é o nome do elemento BEM.

    Exemplos:

    ```JSX
    <button className="block__cancel-button" onClick={this.handleCancelButtonClick} />
    <div className="block__first-name-input">
      <Input onChange={this.handleFirstNameInputChange} />
    </div >
    ``

    Se o componente não estiver aninhado em um elemento BEM, então 'ElementName', se usado, deve ser escolhido de acordo com o significado, com base no contexto \ * \ * (além disso, já que os elementos BEM são nomeados para um propósito semelhante , então o elemento BEM nomeado da mesma forma):

    ```JSX
    <div className="block">
      <Button onClick={this.handleCancelButtonClick} />
      <Input onChange={this.handleFirstNameInputdivChange} />
    </>
    ` `

    ` Justificativa: nomeando o retorno de chamada por esse modelo, não perderemos tempo inventando um nome.

    ** ** Nota: nos casos em que o manipulador é usado em outro lugar, você deve usá-lo em uma função separada: por exemplo, o manipulador `handleButtonClick` que exibe uma lista de elementos só pode ser passado na prop onClick` do elemento BEM "botão" ; se você precisar de uma lista de itens em alguns outros casos, então você deve fazer uma sugestão:

    `` `` Jsx
    HandlebuttonClick () {
      Showitems ();
    }

    showItems() {
      // ...
    }
    ```

<a name="4"></a>

## Bibliotecas

<a name="4.1"></a>

- [4.1](#4.1) Nenhuma em nenhum caso qualquer arquivo pode ser uma biblioteca.

  Se houver uma pequena biblioteca útil que não tenha uma pequena edição, você precisará bifurcar e especificar separadamente o caminho para seunas dependências

<a name="4.2"> </a>

- [4.2] (# 4.2)Aprenda melhor práticas para grandes bibliotecas que você inclui no projeto.

  Existe um [guia] para Angular (https://github.com/mgechev/angularjs-style-guide/blob/master/README-ru-ru.md).  
   Para React, há [guide](https://github.com/airbnb/javascript/tree/master/react) ou [this](https://medium.com/lexical-labs-engineering/redux-best-práticas-64d59775802e).

<a name="4.3"></a>

- [4.3](#4.3) Os módulos devem ser registrados na República do Uzbequistão a partir de node_modules.

  Se módulos adicionais forem usados, o package.json deverá conter os caminhos para as portas que você instalou.

<a name="4.4"></a>

- [4.4](#4.4) Escolha.

  Quando uma pesquisa pode ser usada para uma determinada tarefa, nunca escolha a primeira que aparecer em um mecanismo de pesquisa. Primeiro você precisa avaliar pelo menos 3 Soluções Mais Populares e para cada uma:

  - Você tem um repositório público separado e onde está localizado.
  - Possui documentação e utiliza nossa biblioteca instalada;
  - se não houver docas ou não houver descrição normal, você precisa estudar cuidadosamente o código da biblioteca e entender a API, que resolverá o problema;
  - `ver questões em aberto` (pelo menos folheie a primeira página da biblioteca) e entenda o que pode ser incluído no trabalho dentro do nosso framework;
  - tomar a decisão de coletar apenas bibliotecas mistas com outros valores de acordo com o status de desenvolvedores front-end antigos ou próprios da equipe;
  - elimine a atenção adicionada à biblioteca, ou seja abandonada. Existem pull requests e há discussões neles. Os pull requests são aceitos?
  - destruir a atenção, protestar contra a biblioteca. Se uma biblioteca for testada, vale a pena prestar atenção nos testes que foram escritos para ela: quais casos de uso serão verificados nos testes e se esses problemas foram resolvidos, os casos de uso para os quais você a usa. Também vale a pena prestar atenção à qualidade dos próprios testes, se são frágeis para serem alterados. Se não houver testes para a biblioteca em questão, você pode procurar outra biblioteca.

<a name="5"></a>

## JQuery

> _ou todas as bibliotecas com API semelhante, onde buscamos elementos por seletores e os manipulamos como com variáveis ​​js, por exemplo: _
>
> ```javascript
> const $ newMessage = $('<li class="js-message" />');
> const $messageList = $body.find("ul.js-messages");
> $messageList.append($newMessage);
> ```

<a name="5.1"></a>

- [5.1](#5.1) Todas as classes que usamos para pesquisar o DOM devem começar com o prefixo `js-`.

  Por exemplo, existe um botão que abre um popup ao clicar - precisamos duplicar sua classe e adicionar este prefixo lá:

  ```html
  <div class="open-popup-button js-open-popup-button">< /div>
  `` `

  Como resultado, em arquivos js usamos apenas a segunda classe:

  ```javascript
  $('.js-open-popup-button').click(...);
  ```

  Isso ajudará a evitar quebras inesperadas de scripts ao alterar o layout e vice-versa.

<a name="5.2"></a>tratados

- [5.2](#5.2) Concatenar seletores se os elementos foremda mesma forma.

  ```javascript
  $("form p").addClass("valid");
  $("form li").addClass("válido");
  $("form span").addClass("válido");
  // - é melhor substituir por isso:
  $("form p, form li, form span").addClass("valid");
  ```

<a name="5.3"></a>

- [5.3](#5.3) Todas as variáveis ​​que suportam a API jQuery devem começar com um sinal.

  Por exemplo:

  ```javascript
  const $body = $("body");
  const $listas = $body.find("ul");
  ```

  Isso não é mais uma API jQuery e as variáveis ​​não devem começar com \$

  ```javascript
  // este é um método nativo que também retorna um elemento DOM nativo
  const chatBox = document.getElementById("chat-box") ;

  // recuperação por índice retorna um elemento DOM nativo
  const firstList = $lists[0];
  ```

<a name="5.4"></a>

- [5.4](#5.4) Sempre nomeie os manipuladores de eventos.

  ```javascript
  // Não faça apenas
  $(window).scroll(...);
  // mas
  $(window).on('scroll.myComponent', function (event) {...});
  ```

  Isso facilitará a desconexão de manipuladores quando eles não forem mais necessários.

<a name="5.5"></a>

- [5.5](#5.5) Suporta modularidade.
  Como a ideologia jquery não carrega nenhum conhecimento sobre como organizar aplicações mais ou menos complexas (quando há mais de 3 elementos na página), você tem que inventar tudo sozinho. Os principais princípios a serem seguidos para que o código seja limpo e a arquitetura seja previsível e compreensível para outros membros da equipe:

  <a name="5.5.1"></a>

  1. [5.5.1](#5.5.1) dividir aplicação em blocos semânticos. Tudo o que parece um elemento independente separado deve ser colocado em um bloco separado. Todo o código js para ele deve estar em um arquivo separado e estritamente separado do resto do aplicativo. Este código deve ter uma interface clara e compreensível que permita que o mundo exterior se comunique com o bloco.

  <a name="5.5.2"></a>

  1. [5.5.2](#5.5.2) certifique-se de que dois blocos idênticos na mesma página sejam independentes um do outro. Ou seja, se houver dois controles deslizantes na página, no nível de arquitetura, tome cuidado com antecedência para que nenhum evento do primeiro controle afete o segundo.

  <a name="5.5.3"></a>

  1. [5.5.3](#5.5.3) A condição anterior (independência de blocos homogêneos) pode ser alcançada se o código js de cada bloco for enquadrado em um class e, em seguida, para criar cada bloco html de contador no layout de acordo com a instância da classe. Em uma instância de classe, você pode salvar o próprio elemento DOM e somente através dele procurar todos os elementos aninhados e apenas pendurar manipuladores neles.

  <a name="5.5.4"></a>tivessem

  1. [5.5.4](#5.5.4) O requisito acima era que todos os manipuladores nãonome. Aqui fica ainda mais estrito - os nomes dos manipuladores para diferentes instâncias da mesma classe devem ser únicos, de modo que \$(block).off(...) desabilite eventos apenas para a instância atual do bloco, não para todas instâncias, caso contrário, inesperadamente para o desenvolvedor, os manipuladores de eventos para todos os controles deslizantes na página serão desativados imediatamente.

  <a name="5.5.5"></a>

  1. [5.5.5](#5.5.5) Além disso, as classes permitem que você torne a estrutura de todos os blocos igual e previsível - sabendo como o bloco deslizante funciona , você já pode prever como os blocos de calendário e dropdown são organizados. Todos eles terão métodos para inicializar e procurar por elementos DOM aninhados, todos terão código que trava eventos, todos terão uma interface para excluir uma instância e assim por diante. Portanto, é melhor cuidar imediatamente da mesma estrutura e padronizar tudo o máximo possível.

<a name="6"></a>

## React

> _Leia e aplique somente se você já estiver familiarizado com o React, caso contrário, ignore por

enquanto_ <a name="6.1"></a>

- [6.1] (# 6.1) Todos os componentes devem ser funcionais por padrão, ou seja, sem estado ([o que é?](https://reactjs.org/docs/components-and-props.html#stateless-functions)) e somente quando necessário tornar-se componente `baseado em classe`.

<a name="6.2"></a>

- [6.2](#6.2) O método `render()` deve ser limpo ([ler documentos](https://reactjs.org/docs/react-component.html#render)).

<a name="6.3"></a>

- [6.3](#6.3) Evite criar métodos de renderização em componentes de classe (não se trata do método de renderização, mas de métodos que você pode escrever além dele e que também retornar JSX).

  Como esses métodos retornam fragmentos JSX que não são objetos completos de unidade de reação, você pode ter problemas para manter esses componentes posteriormente. E então - com jsx renderizado incorretamente, não é possível trabalhar como com uma unidade de reação completa, problemas com refs e rastreabilidade no DOM.

  Se você quiser remover o JSX - remova-o em um componente sem estado.  
   Por exemplo:

  ```javascript
  export class OrderStatus extends Component {
    renderStatusView(status) {
      // esta renderização deve ser renderizada em um componente separado
      if (status === "succeed") {
        return <span>Pronto!</span> ;
      }
      return <span>Ativo...</span>;
    }

    render() {
      return (
        <div>
          Status do pedido: {this.renderStatusView(this.props.status)}// O
          componente deve ser usado aqui, não o método
        </div>
      );
    }
  }
  ```

<a name="6.4"></a>

- [6.4](#6.4) O método `render()` e todos os métodos que retornam pedaços DOM devem ser colocados no final do componente, o O próprio método `render` é o mais recente público.

<a name="6.5"></a>

- [6.5](#6.5) Como trabalhar com `criadores de ação (redux)`.

  - Você deve evitar chamadas desnecessárias de `getState` para `action creator`, exceto em casos específicos (por exemplo, quando a visualização não pode obter dados suficientes de forma alguma). Os dados devem ser enviados ao `criador da ação` explicitamente como argumentos para indicar explicitamente com quais dados a função está trabalhando e o que ela precisa para funcionar corretamente.

  - A decomposição de uma ação complexa (composta por várias ações estruturais e algorítmicas) deve ser realizada na presença de um desenvolvedor sênior. ou seja, se vários `dispatch` em um `action creatore` forem sugeridos, este ponto deve ser discutido com o desenvolvedor sênior, porque há casos em que isso pode ser evitado, e há casos em que não pode

  - os criadores de ação devem ser chamados apenas em contêineres, em resposta a ações de componentes estúpidos de nível inferior: por exemplo, `registerUser action` deve ser chamado em resposta a o evento `OnSubmit` do componente do formulário de registro .

<a name="7"></a>

## Desempenho

<a name="7.1"></a>

- [7.1](#7.1) Em projetos jquery ou qualquer coisa que procure elementos DOM por seletores - você precisa para armazenar em cache todos os elementos encontrados.

  ```javascript
  $foodItem = $("#lista de compras li");

  $foodItem.click(function() {
    // faça algo...
  });
  ```

<a name="7.2"></a>

- [7.2](#7.2) Todas as operações DOM são melhor executadas primeiro em elementos virtuais e, em seguida, inseridas imediatamente no documento da página.

  aqui, em um loop no DOM, cada elemento do array é embutido um por um, como resultado, temos vários loops de redesenho:

  ```javascript
  for (let i=0; i < items.length; i++ ) {
      const item = document.createElement("li" );
      item.appendChild(document.createTextNode("Option " + i);
      list.appendChild(item);
  }
  ```

  Aqui nós fazemos um loop adicionando um elemento a um elemento virtual, e então incorporamos tudo de uma vez no DOM real e obtemos um loop de redesenho:

  ```javascript
  const fragment = document.createDocumentFragment();
  for (let i=0; i < items.length; i++) {
      const item = document.createElement('li');
      item.appendChild(document . createTextNode('Option ' + i);
      fragment.appendChild(item);
  }
  list.appendChild(fragment);
  ```

<a name="7.3"></a>

- [7.3](#7.3) Evite complexos seletores .

  dependendo do tipo e complexidade do seletor dependente de CSS, desempenho de renderização da animação e exemplo de uso do site no seletor `transition` por atributo (por exemplo, entrada [type = "text"50%) `} teoricamente poderia retardar a animação em si.As mesmas regras são extrapoladas para toda a página.Os seletores css mais complexos (muitos seletores aninhados e não triviais com a necessidade de calcular prioridades com frequência e muito) , mais difícil será para o navegador renderizar a página, porque você precisa aplicar estilos consistentemente entre si e analisar a árvore DOM, o que, é claro, não é a tarefa mais fácil em termos de desempenho em si.

<a name="7.4"></a>

- [7.4](#7.4) Incluímos todos os js-ki na parte inferior da página antes da tag de fechamento `<body>`.

<a name="7.5"></a>

- [7.5](#7.5) Materiais úteis:

  - [Perf.Rocks](https://perf.rocks/)
  - [calendar](https://calendar. perfplanet.com/2014/)
  - [Regras do PageSpeed ​​Insights](https://developers.google.com/speed/docs/insights/rules)
  - [avascriptrocks](http://javascriptrocks.com/)

<a name= "8"></a>

## Arquitetura

<a name="8.1"></a>

- [8.1](#8.1) Modularidade é tudo!

  Certifique-se de dividir o aplicativo em diferentes módulos, mesmo que o site seja apenas conteúdo estático com vários manipuladores de eventos que são suspensos via jquery.

  Para importar módulos entre si, use o webpack, se o projeto for muito simples, você pode criar um (!) objeto Global e salvar diferentes módulos com suas propriedades.

  Há apenas um arquivo para cada módulo. Sem usar o webpack e outros bundlers, tome cuidado para não poluir o escopo global (agrupe todo o conteúdo de cada arquivo em uma função de chamada automática).

  Dentro da estrutura de um módulo, descreva apenas funcionalidades semelhantes que são unidas pelo significado. Isso se chama [conectividade](https://ru.wikipedia.org/wiki/%D0%A1%D0%B2%D1%8F%D0%B7%D0%BD%D0%BE%D1%81%D1%82%D1%8C_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)). O outro lado da moeda - [engajamento](https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D1%86%D0%B5%D0%BF%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)), quando os módulos dependem muito um do outro - isso Deveria ser evitado. Ou seja, o princípio geral é que os módulos devem ser divididos para que dentro de cada módulo haja a máxima semelhança da área de trabalho, e entre os módulos haja a máxima diferença. Por exemplo, em estatística, a segmentação é realizada de acordo com os mesmos princípios, todos os grupos devem consistir nos elementos mais semelhantes e, ao mesmo tempo, diferir entre si o máximo possível :).

<a name="8.2"></a>

- [8.2](#8.2) Dentro do módulo, divida claramente em camadas e não interfira na lógica de trabalhar com o DOM e trabalhar com dados (por exemplo, solicitações ajax ).

  Em geral, todo o trabalho com os dados em si deve ser separado o máximo possível do trabalho com o DOM e do processamento de eventos do usuário (cliques, envios, etc.).

  É desejável que cada aplicação formalize mais ou menos a estrutura do módulo, é impossível descrevê-lo de uma forma específica para todos os projetos, pois algo está escrito em `React`, algo em `React + Redux`, e algo em `jquery` simples. Para este último, este ponto é o mais importante, mas também o mais incerto.

<a name="8.3"></a>

- [8.3](#8.3) Evite mutações de uma variável em várias funções ao mesmo tempo.

  Exemplo de código incorreto:

  ```javascript
  const box = {};

  function addBall(box) {
    box.ball = { radius: 2 };
  }

  function addFood(box) { box.food
    = { cenoura: 4 };
  }

  function addShoes(box) {
    box.shoes = { tênis: 2 };
  }

  addBall(box);
  addFood(box);
  addShoes(box);
  ```

  Por causa de tais ações, o escopo da variável se torna muito grande e fica difícil entender qual função e quando mudou a variável. Quando ocorrer um erro na 10ª função, não ficará claro por que a caixa contém 5 pares de tênis e 15 cenouras.

  Use funções puras, recrie objetos em vez de alterá-los, ou melhor ainda, formalize todas as possibilidades de alterar seu objeto, como o `Redux` faz para a variável de estado da aplicação.

<a name="8.4"></a>

- [8.4](#8.4) Não há propriedades públicas ou privadas em js, portanto, métodos privados são fáceis de fazer com prefixos `"_"` (sublinhado).

  ```javascript
  class Person {
    constructor(name) {
      this.name = name;
    }

    public() {
      console.log("Chame-me dos módulos externos");
    }

    _private() {log(
      console.
        "Chame-me apenas dos métodos da classe Person, por exemplo de public"
      );
    }
  }
  ```

<a name="8.5"></a>

- [8.5](#8.5) Ao escrever uma classe, declare todos os métodos públicos primeiro, e o construtor deve vir primeiro, agrupe todos os métodos privados por significado em a parte inferior da classe

< a name="9"></a>

## Security

- [Browser Security Handbook from Google](https://code.google.com/archive/p/browsersec/wikis/Main.wiki).
- [Folha de dicas de segurança HTML5](https://html5sec.org/#javascript).
- [Noções básicas de segurança da Web](https://github.com/vasanthk/web-security-basics).
