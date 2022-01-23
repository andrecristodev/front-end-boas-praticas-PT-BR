#Iniciação

<a name="1"></a>

- [1](#1) Crio README.md.

  - Todo projeto hospedado no github deve ter um readme.md.

  - Readme deve conter o nome do projeto.

  - Readme deve conter todas as informações necessárias para implantação (instalação) do projeto e lançamento/teste, certifique-se de testar a implantação em uma nova pasta do zero.

  - В o projeto deve usar um mínimo de bibliotecas globais, todas elas devem estar listadas no Readme (webpack, karma e tudo que pode ser entregue via npm, definitivamente não deve ser global)
  - Se o objetivo do projeto não estiver claro no nome, vale a pena fazer uma breve descrição dele..

  - Se o projeto usar bibliotecas ou abordagens arquitetônicas não padrão, elas também devem ser especificadas. Além disso, é desejável indicar links para seus repositórios para que uma pessoa designada para este projeto, mas que não trabalhou com as tecnologias utilizadas, não precise procurá-los no Google.

  - Se o projeto do repositório já estiver implantado em algum lugar (por exemplo, nas páginas do github), você deve especificar um link para ele.

<a name="2"></a>

- [2](#2) Faça recuos com espaços, no projeto em todos os arquivos html, pug, etc deve haver o mesmo recuo - 4 ou 2 espaços.

<a name="3"></a>

- [3](#3) Pergunte na entrada quais navegadores digitamos (obrigatório).

<a name="4"></a>

- [4](#4) Pergunte se há um adaptável, se não, então sob quais resoluções digitar e o que fazer para outras telas.

<a name="5"></a>

- [5](#5) Lançar site via http://localhost, não através file:///c:\test.html

  Caso contrário, podem ocorrer problemas com elementos inseridos por meio do iframe (por exemplo, likes de FB, VK, etc.), e ao executar scripts que enviam solicitações HTTP, além de problemas inesperados e desconhecidos.

<a name="6"></a>

- [6](#6) Saber de antemão com clareza qual é o resultado fixo do projeto - o ambiente de produção implantado em nosso servidor ou apenas um repositório git, ou mesmo um arquivo zip enviado por correio.

<a name="7"></a>

- [7](#7) Lembre-se sempre: se você pode resolver problemas de alguma forma, isso não significa que realmente valha a pena usar o método.

  Tanto no layout quanto na programação, muitas vezes surgem situações em que você pode escrever um código bastante funcional, mas fazê-lo de maneira não confiável, usando hacks diretos que não são óbvios para outros desenvolvedores ou simplesmente decorando tudo de uma maneira feia. Se você tiver um problema à sua frente, precisará não apenas resolvê-lo, mas também tornar a solução legível, escalável e confiável. Em todos os casos em que houver dúvidas, é melhor perguntar a camaradas mais experientes - isso permitirá que você cresça mais rápido e o projeto obtenha um código melhor.
