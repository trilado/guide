# Database #
A classe `Database` é responsável pela conexão e comunicação entre a aplicação e o banco de dados. É por meio dela que são realizadas as buscas, inserções, atualizações e exclusões de registros de uma entidade. A forma de manipulação da classe `Model` que apresentamos na seção [Active Record](~/guide/model/active-record), implementa, de forma transparente, a instanciação da classe `Database`.

## Conexão ##

A classe `Database` implementa o padrão Factory, que cria uma instância da classe `Datasource` de acordo com as configurações de banco de dados. Porém, é necessário que exista um datasource conforme a configuração.

Veja um exemplo de configuração:

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

Agora veja um exemplo de como criar uma instância de `Database`:


	$db = Database::factory();

No exemplo, a variável `$db` está recebendo uma instância do datasource, de acordo com a configuração. Como não foi especificado qual configuração de datasource, o método irá utilizar a configuração `default`. Como na configurção está específicado que o `type`, ou o driver, será o `mysql`, é necessário ter uma classe de datasource chamada `MysqlDatasource` que herde da classe abstrada `Datasource`.

Um outro exemplo é especificar qual configuração a instância irá utilizar:

	$db = Database::factory('outher');

Nesse exemplo, a classe `Database` irá conectar ao banco de dados usando a configuração `outher`. Como na configurção está específicado que o `type`, ou o driver, será o `sqlsrv`, é necessário ter um datasource `SqlsrvDatasource` que herde da classe abstrada `Datasource`.

~? O padrão Factory foi implementando junto ao padrão Singleton. No caso, por exemplo, toda vez que chamar o método `factory()`, em uma única requisição, informando o parâmetro `outher`, não será criada uma nova conexão, o Trilado irá usar a existente, pois as configurações são as mesmas. ~?

## Entidades ##
Após criar uma instância de `Database`, pode-se utilizar os models pertencentes à conexão especificada. Se, por exemplo, usarmos a driver `mysql`, irá retorna uma instância de `MysqlDatasource`:

	$db->User;

No exemplo acima estamos chamando o model `User`. Nesse caso será necessário existir uma classe `User` que herde de `Model`.