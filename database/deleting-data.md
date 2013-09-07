# Deletando Dados  #
Utilizando a classe `Database` também é possível remover registros de uma tabela.


## delete() ##
Com o método `delete()` você remove um registro do banco de dados. Esse método recebe como parâmetro uma instância de `Model` referente à entidade que você estiver trabalhando. Por exemplo:

	$user = User::get(2);

	$db = Database::factory();
	$db->User->delete($user);
	
	$db->save();

Observe que utilizamos o método `get()`, isso porque para usarmos o `update()`, devemos informar uma instância recuperada do banco de dados. Se informarmos uma instância nova de model, o framework irá disparar uma exceção.

## deleteAll() ##
A diferença entre os métodos `delete()` e `deleteAll()` é que o primeiro remove um único registro, utilizando a chave primária como condicional. Já o segundo utiliza o condicional que você informar. Existem duas formas de informar o condicional, veja:

	$db = Database::factory();
	$db->User->where('UserId = ?', 3)->deleteAll();
	
	$db->save();

Veja que utilizando o método `where()`, que foi apresentado anteriormente. As demais formas também podem ser utilizadas. A segunda forma é mais compacta, na qual passamos o condicional como parâmetro do método `deleteAll()`, assim como mostramos anteriormente no `all()` e no `single()`.

	$db = Database::factory();
	$db->User->deleteAll('UserId = ?', 3);
	
	$db->save();
