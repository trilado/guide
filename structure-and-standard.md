# Estrutura #
O Trilado apresenta uma estrutura que tem como objetivo organizar os códigos da aplicação. Assim, os desenvolvedores que utilizam o Trilado não terão dificuldades em entender o objetivo de determinado arquivo, isso por localização. Por padrão a framework utiliza o padrão MVC, que separa o código em três camadas (Model, View e Controller), no entanto é possível realizar alterações neste formato, como será apresentado a posteriori.

Após fazer o download do Trilado Framework e extrair o arquivo compactado, será obtida a seguinte estrutura de diretórios:

	trilado/
	├── app/
	│   ├── controllers/
	│   ├── helpers/
	│   ├── locale/
	│   ├── models/
	│   ├── tmp/
	│   │   ├── cache/
	│   │   └── logs/
	│   ├── vendors/
	│   ├── views/
	│   │   ├── _error/
	│   │   ├── _master/
	│   │   └── _snippet/
	│   └── wwwroot/
	└── core/
	    ├── error/
	    └── libs/
	        ├── cachesource/
	        ├── datasource/
	        └── exceptions/

Os dois diretórios principais `core` e `app`. O primeiro é onde ficam os códigos que fazem parte do framework, são essenciais para o funcionamento do Trilado. O segundo é onde ficará a aplicação.

## app/ ##
Dentro do `app` ainda exitem outros diretórios, cada uma destas pastas possuí um objetivo específico que será apresentado a seguir.

| Diretório   | Descrição                 |
| ----------  | ------------------------- |
| controllers | Diretório em que estão as classes que herdam de `Controller` |
| helpers     | Diretório para classes que auxiliam o programador e desenvolver a interface |
| locale      | Diretório para os arquivos de idiomas (internacionalização) |
| models      | Diretório para as classes que heram de `Model` ou com lógica de negócio  |
| tmp         | Diretório para arquivos temporários, como logs e cache |
| vendors     | Diretório para arquivos de terceiros, ou seja, que você baixou |
| view        | Diretório para views |
| wwwroot     | Diretório público, para arquivos estáticos. Quando o usuário acessar `seusite.com/logo.png`, por exemplo, ele estará acessando esse diretório |

Além desses diretórios, o programador pode criar outros diretórios, tanto para arquivos estáticos, dentro do `wwwroot`, como para PHP, como por exemplo, para classes de excções próprias. Mais informações sobre a divisão de arquivos padrão da aplicação pode, ser encontradas na seção [Sistema de Arquivos da Aplicação]().

~? Os diretórios criados pelo programador para armazenar classes devem ser registrados no arquivo de configuração. Veja a seção Configuração ~?

## core/ ##
Dentro do diretório `core`, ou núcleo, tém mais dois diretórios, o `error` e `libs`. O primeiro armazena páginas HTML de erro padrão da aplicação. O segundo armazena as classes que formam o framework.

### libs/ ###
Dentro do diretório `libs`, são apresentados mais três diretórios, que são:

| Diretório   | Descrição                 |
| ----------  | ------------------------- |
| cachesource | Diretório em que ficam as classes que fazem conexão com as ferramentas de cache |
| datasource  | Diretório em que ficam as classes que fazem conexão com os bancos de dados |
| exceptions  | Diretório com as classes de exceções do Trilado |


# Padrões #
A padronização, dentro do desenvolvimento de software, é muito importante, pois facilita a compreensão dos códigos escritos por terceiros. Nós, da equipe de desenvolvimento do Trilado, definimos alguns padrões, ou convenções, para que possa facilitar a  compreensão de classes e bibliotecas compartilhadas para o framework. Esses padrões não são obrigatórios, são apenas recomendandos.

## Formatos de Arquivo ##
No Trilado, os arquivos devem conter o mesmo nome classe, assim, o framework consegue carregá=los automaticamente quando necessitados. 

| Tipo       | Nome da Classe   | Caminho do Arquivo               |
| ---------- | ---------------  | -------------------------------- |
| Controller | PostController   | controllers/PostController.php   |
| Model      | Post             | models/Post.php                  |
| Helper     | MyForm           | helpers/MyForm.php               |




## Fechar Tag PHP ##
O PHP não obriga que os arquivos fechem a tag `?>`, porém, se for fechado, quando espaço em branco ou quebra de linha pode gerar uma saída inesperada. Portanto, adotamos o padrão de fechar a tag em arquivos de classes PHP.

	//Incorreto
	<?php
	class Test {}
	?>

	
	//Correto
	<?php
	class Test {}

## Nome de Classe ##
Os nomes de classes devem seguir o padrão `UpperCamelCase`, onde cada palavra é iniciada com Maiúsculas e unidas sem espaços.

	//Incorreto
	class postController {}
	class postcontroller {}
	class post_controller {}

	//Correto
	class PostControler {}

## Identação ##
Por questão de organização, adotamos o padrão de identação do Trilado Framework com uma quebra nas chaves que compoem as classes, métodos, condicionais e laços de repetição.

### Classes ###
As chaves das classes, quando estão vazias, podem estar na mesma linha.

	//Incorreto
	class PostControler {
	}
	class PostControler 
	{
	}
	class PostControler {
		public function index() {}
	}

	//Correto
	class PostControler {}
	class PostControler 
	{
		public function index() {}
	}

### Métodos e Funções ###
As chaves dos métodos e funções, quando estão vazias, podem estar na mesma linha.

	//Incorreto
	function index() {
	}
	function index() 
	{
	}
	function index() {
		echo 'hello';
	}

	//Correto
	function index() {}
	function index() 
	{
		echo 'hello';
	}

### Condicionais ####
Nos condicionais, quando houver apenas uma linha, não é necessário utilizar as chaves, porém, quando houver duas linhas ou mais, será necessário que as chaves estejam em nova linha.

	//Incorreto
	if($a > 1) {
	}
	if($a > 1) {
	} else {
	}
	if($a > 1) {
	} 
	else {
	}
	switch($a) {
		case 1: {
		}
	}

	//Correto
	if($a > 1) 
	{
	}
	if($a > 1) 
	{
	}
	else
	{
	}
	if($a > 1)
		echo 'a';
	else
		echo 'b';
	switch($a) 
	{
		case 1: 
		{
		}
	}

### Laços de Repetição ###
Nos laços de repetição, quando houver apenas uma linha, não é necessário utilizar as chaves, porém, quando houver duas linhas ou mais, será necessário que as chaves estejam em nova linha.

	//Incorreto
	for($i = 0; $i < 10; $i++) {
	}
	while($i < 10) {
	}
	do {
	} while($i < 10);

	//Correto
	for($i = 0; $i < 10; $i++) 
	{
	}
	for($i = 0; $i < 10; $i++) 
		echo $i;
	while($i < 10) 
	{
	}
	do 
	{
	} while($i < 10);