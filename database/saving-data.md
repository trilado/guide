# Salvando Dados  #
Utilizando a classe `Database` também é possível fazer a inserção e atualização de registros de uma tabela.

## insert() ##
Com o método `insert()` você adiciona um novo objeto ao banco, neste caso suas propriedades serão transformadas em instruções SQL e inseridas no banco. Esse método recebe como parâmetro uma instância de `Model` referente à entidade que você estiver trabalhando. Por exemplo:

	$user = new User();
	$user->Name	= 'Jhon';
	$user->Level	= 1;
	$user->Status	= 1;
	
	$db = Database::factory();
	$db->User->insert($user);
	
	$db->save();

O método `insert()` não executa a instrução SQL, desta forma os dados apenas serão salvos no banco ao acionar o método `save()`. Observe que o método `insert()` é chamado a partir de uma entidade que representa a tabela no banco de dados. Enquanto que `save()`, foi chamado diretamente a partir da variável `$db`.

## update() ###
Um pouco parecido com o método `insert()`, o `update()` serve para atualizar um registro existente no banco de dados. Você deve informar como parâmetro uma instância do model referente à entidade que estive trabalhando.

	$user = User::get(2);
	$user->Level	= 1;
	$user->Status	= 1;
	
	$db = Database::factory();
	$db->User->update($user);
	
	$db->save();

Observe que utilizamos o método `get()`, isso porque para utilizar o `update()`, devemos informar uma instância recuperada do banco de dados. Se informarmos uma instância nova do model, o framework irá disparar uma exceção.