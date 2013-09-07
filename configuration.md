# Configuração #

As configurações do Trilado Framework estão concentradas no arquivo `app/config.php`, portanto, os códigos e alterações mencionados abaixo, deverão ser feitos dentro desse arquivo.

## Básicas ##

### Template Padrão ###
Em um controller ou action é possível especificar qual template (ou master) será carregado na apresentação da página. Caso esse template não seja especificado, o Trilado irá carregar o template padrão, portanto, é necessário informar qual será o template padrão.

Para definir qual será esse template, é utilizada a configuração:

	Config::set('default_master', 'template');

Além da definição da configuração, também será necessário criar um arquivo dentro do diretório `app/views/_master` com o nome exatamente igual ao definido como padrão, adicionando a extensão `.php`. O arquivo do exemplo acima ficaria `template.php`.

Veja sobre templates na seção [Master](~/guide/views/master).

### Controller Padrão ###
Está opção define qual o controller padrão que será executado pela aplicação caso nenhum seja específicado pelo usuário. Assim, quando o usuário acessar o diretório raiz da sua aplicação, o Trilado deverá executar o controller que foi definido nesta opção. Para definir o controller padrão, é utilizada a configuração:

	Config::set('default_controller', 'Home');

Neste caso, quando o usuário acessar, por exemplo http://exemplo.com, o controller  `HomeController` será executado. O valor definido na configuração acima não é acompanhando da palavra Controller, pois esse tratamento é realizado pelo Trilado.

### Action Padrão ###
Da mesma forma que é necessário definir um controller padrão, também é necessário definir uma action padrão. Porém, ao contrário do anterior, que era executado somente quando o usuário acessasse a raiz da aplicação, a action padrão será executada toda vez que o usuário acessar uma URL que informa o controller, mas não informa a action.

Para definir a action padrão, é utilizada a configuração:

	Config::set('default_action', 'index');

No caso, quando o usuário acessar http://exemplo.com, a action `HomeController->index()` será executada.

Mas se o usuário acessar http://exemplo.com/post, a action `PostController->index()` será executada. Repare que nessa forma, o controller foi especificado.

### Página de Login ###
Essa configuração só será utilizada se o desenvolvedor utilizar a classe de autenticação do Trilado.

Define para qual URL o usuário será redirecionado caso tente acessar uma página que necessite que ele esteja logado. Normalmente é utilizada para definir a página de login. Veja o exemplo:

	Config::set('default_login', '~/admin');

Pode-se utilizar um endereço completo, começando com `http`, ou `~/` para informar que o endereço começará a partir da raiz da aplicação.

### Charset ###
O charset define a condifição padrão que será adotada pelo Framework:

	Config::set('charset', 'UTF-8');

### Idioma Padrão ###
Com o suporte a internaciolização, será necessário informar qual a linguagem padrão da aplicação, ou seja, em que idioma estão escritos os textos das páginas da aplicação?

Para definir o idioma padrão, é utilizada a configuração:

	Config::set('default_lang', 'pt-br');

Veja mais sobre como criar uma aplicação em vários idiomas na seção de [Internacionalização](~/guide/internationalization).

### Chave de Criptografia ###
Alguns dados são criptografados para aumentar a segurança da aplicação, portanto, é importante definir uma `salt` próprio, assim, caso ocorra coleta dos dados de forma impropria, a criptografia só será desfeita utilizando o valor que você definir, além de outras informações, como o diretório da aplicação.

Para definir o salt, é utilizada a configuração:

	Config::set('salt', 'use qualquer caractere aqui');

## Debug ##

Outra forma de segurança é o funcionamento da configuração de debug, na qual você poderá definir quando as mensagens de erros serão exibidas. Além das mensagens de erro, com o modo debug ativado é possível ver otras informações da aplicação, como por exemplo as consultas SQL executadas.

Para definir o debug, é utilizada a seguinte configuração, informando um `array` como parâmetro:

	Config::set('debug', array(
		'type'	=> 'local',
		'query'	=> false,
		'sql'	=> true,
	));

Veja abaixo a definição de cada chave e valor:

### type ###

O `type` define para quem o debug estará habilitado, pode assumir 3 valores, são eles:

| Valor  | Descrição |
| ------ | --------- |
| off    | Desabilita o debug, os erros são gravados nos logs |
| local  | Habilita somente para conexões localhost |
| all    | Habilita para todos os usuários |

~! Não é recomendado o uso do valor `all`, pois, caso a aplicação dispare um erro, o usuário terá acesso a detalhes do erro. ~!

### query ###

Em alguns casos, é necessário verificar o debug, porém, não tem acesso direto ao servidor para acessar a aplicação localhost, portanto, você pode definir um valor para a querystring `debug` que, ao ser acessada, habilita o debug. O valor padrão da query é `false`, nesse caso, a querystring não irá funcionar.

	'query' => 'hab-meu-debug'

No exemplo acima, ao acessar uma URL com a querystring `?debug=hab-meu-debug`, o debug será habilitado, mas somente para página que você está acessando e no momento em que você está acessando.

~! Se for habilitar essa opção, é importante que defina um valor que só você saberá, para que outra pessoa não tenha acesso as informações. ~!

### sql ###
O `sql` define se serão exibidas as instruções SQL geradas pelo ORM. Por exemplo, ao executar o código abaixo, irá aparecer a instrução SQL correspondente no final da página.

	Post::all()

O comando anterior gera o seguinte SQL.

	SELECT post.* FROM post

~? Se defindo como `true`, só funciona se o debug estiver habilitado. ~?

## Banco de Dados ##
O Trilado permite que sua aplicação conecte em vários bancos de dados diferentes, e ao mesmo tempo. Você deve configurar as conexões, e dentro da sua aplicação chamar a que necessitar.

Para definir as conexões, é utilizada a seguinte configuração, informando uma matriz (`array` bidimensional) como parâmetro: 

	Config::set('database', array(
		'default' => array(
			'type' => 'mysql',
			'host' => 'localhost',
			'name' => 'trilado2',
			'user' => 'root',
			'pass' => '1234',
			'validate' => true
		)
	));

O primeiro array deve ter como chave o nome da configuração. No exemplo acima foi utilizada a chave `default`, que é chamada quando o nome da conexão não é informado no `Database::factory()` (veja mais na seção [Database](~/guide/database)).

Os valores do segundo array são:

| Valor  | Tipo   | Descrição |
| ------ | ------ | --------- |
| type   | string | Define qual driver (chamado de datasource) o framework irá utilizar. É necessário que exista uma classe que implemente os métodos do datasource dentro diretório `core/libs/datasource/NomeDatasource.php` |
| host   | string | Endereço do servidor do banco de dados |
| name   | string | Nome do banco de dados |
| user   | string | Usuário do banco de dados |
| pass   | string | Senha do usuário do banco de dados |
| validate | boolean | Se `true`, define que o framework irá validar a instância do `Model` de acordo com as [Anotações](~/guide/model/annotation) |

O Trilado vem com dois datasource implementados, o `MysqlDatasource` (type = mysql) e `SqlsrvDatasource` (type = sqlsrv, do SQL Server) com a biblioteca PDO de ambos. Você pode baixar outros datasources em nosso fórum e criar o seu, basta extender a classe `Datasource` e implementar os métodos.

A seguir um exemplo de configuração utilizando duas conexões.

	Config::set('database', array(
		'default' => array(
			'type' => 'mysql',
			'host' => 'localhost',
			'name' => 'trilado2',
			'user' => 'root',
			'pass' => '1234',
			'validate' => true
		),
		'outher' => array(
			'type' => 'sqlsrv',
			'host' => '.\\SQLEXPRESS',
			'name' => 'trilado2',
			'user' => 'sa',
			'pass' => '1234',
			'validate' => true
		)
	));

## Cache ##
Alguns dados do Trilado são armazenados automaticamente em cache, isso para aumentar o desempenho do framework, e consequentemente da aplicação. A forma de armazenamento de cache padrão é em arquivos no disco, que é mais rápido do que o Trilado ter que processar os dados todas vezes, no entanto existem outras formas de armazenamento em cache mais eficientes. Portanto, é possível configurar qual ferramenta será utilizada para armazenamento.

Para definir o cache, é utilizada a seguinte configuração, informando um `array` como parâmetro:

	Config::set('cache', array(
		'enabled'	=> false,
		'type'		=> 'file',
		'host'		=> 'localhost',
		'port'		=> 0,
		'page'		=> false,
		'time'		=> 10
	));


| Valor  | Tipo    | Descrição |
| ------ | ------- | --------- |
| enabled| boolean | Define o cache está habilitado ou não |
| type   | string  | Define qual driver (chamanos de cachesource) o framework irá utilizar. É necessário que exista o cachesource dentro diretório `core/libs/cachesource/NomeCachesource.php` |
| host   | string  | Endereço do servidor de cache |
| port   | int     | Porta da conexão com o servidor |
| page   | boolean | Define se o HTML das páginas serão armazenadas automáticamente em cache. Se definido como `true`, o tempo de armazenamento é do parâmetro `time` |
| time   | int     | Tempo padrão que os dados permanecerão no cache |

O Trilado vem com alguns CacheSources implementados, o `FileCachesource`, `ApcCachesource`, `MemcacheCachesource` e `MemcachedCachesource`. Você pode baixar outros cachesources em nosso fórum e criar o seu, basta extender a classe `Cachesource` e implementar os métodos. Mais informações sobre o armazenamento de arquivos em Cache na seção [Cache](~/guide/cache).

## AJAX ##
O Trilado fornece uma série de facilidades para o desenvolvedor utilizar AJAX em sua aplicação, veja como configurar:

### Resposta AJAX Automaticamente ###
Um dos recursos do Trilado é a detecção automática de requisições via AJAX, você pode configurar o Trilado para responder a requisição em formado AJAX também:

	Config::set('auto_ajax', true);

Para que essa configuração funcione, é necessário informado ao framework qual conteúdo será retornado na action. Veja a seção [Controller > Retornos](/guide/controller/return).

### Resposta JSON Automaticamente ###
Outro recurso interessante, baseado na API do Twitter, é informar qual o tipo resposta da aplicação por meio da URL. Se essa configuração for definida como `true`, ao acessar uma action terminando com .json, o Trilado irá retorna automaticamente dos dados no formato JSON.

	Config::set('auto_dotjson', true);

Para que essa configuração funcione, é necessário informar ao framework qual conteúdo será retornado na action. Veja a seção [Controller > Retornos](/guide/controller/return).

### Resposta XML Automaticamente ###
Semelhante a opção anterior, porém para requisições com .xml. Neste caso as requisições retornarão dados no formato XML.

	Config::set('auto_dotxml', true);

Para que essa configuração funcione, é necessário informar ao framework qual conteúdo será retornado na action. Veja a seção [Controller > Retornos](/guide/controller/return).

## Dispositivo Móvel ##
Quando um usuário acessar sua aplicação via dipositivo móvel (celular ou tablet) é possível apresentar uma versão da interface de acordo com o aparelho do usuário.

### Versão Móvel Automaticamente ###
Se a requisição partir de um dispositivo móvel a configuração estiver definida com `true`, o Trilado irá procurar as views com nome `nome_da_view.mobile.php`, dessa forma, você pode definir uma interface mais leve para celulares.

	Config::set('auto_mobile', true);

Caso não exista a view na versão móvel, o Trilado irá carregar a versão normal, mesmo se configuração for `true`.

### Versão Tablet Automaticamente ###
Semelhante ao anterior, porém, a detecção é para tablets. Se definido como `true`, o Trilado irá procurar as view com o nome `nome_da_view.tablet.php`.

	Config::set('auto_tablet', true);

Em geral a maior parte dos tablets possuem resoluções maiores que os celulares, o que motivou a separação destas interfaces. Na verdade, muitas vezes é desnecessária a criação de uma interface para tablet, uma vez que as resoluções são semelhantes ao computador.

## Registrar Diretório ##
O Trilado vem com uma estrutura padrão de diretórios, na qual seu núcleo está programado para importar automaticamente os arquivos que ele necessita. Porém, em alguns casos pode ser necessário que você informe algum diretório a mais para carregar os arquivos. 

Você pode utilizar o método `Import::register()`, informando qual diretório deseja inserir, assim, o Trilado irá importar os arquivos desse diretório quando forem solicitados:

	Config::set('directories', array(
		'controller'	=> App::$root . 'app/controllers',
		'model'			=> App::$root . 'app/models',
		'helper'		=> App::$root . 'app/helpers',
		'vendor'		=> App::$root . 'app/vendors',
	));

Quando uma classe for instanciada, ou executado algum método estático, por exemplo `$var = new Hello()` ou `Hello::world()`, o Trilado irá procurar automaticamente dentro dos diretórios registrados. Neste caso, serão procurados primeiramente nos diretórios inicialmente definidos no framework, e posteiormente os definidos pelo desenvolvedor. Mais informações sobre o sistema de arquivos do Trilado na seção [Sistema de Arquivos](~/guide/filesystem).

~! O arquivo importado deve possuir o mesmo nome da classe. As classes com _ para representar o namespace também são aceitas, por exemplo, se registrarmos o `app/meudir` e chamarmos a classe `new Hello_World()` ela deverá estar em `app/meudir/hello/World.php` ~!

Ao encontrar o diretório da classe chamada, o Trilado guarda o endereço em cache, assim, na próxima chama a importação será executada mais rapidamente. O tempo de cache vai de acordo com a configuração, previamente apresentada.