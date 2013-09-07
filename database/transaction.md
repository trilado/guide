# Transações ##
A classe `Database` também oferece métodos para trabalharmos com transações. Eles servem para garantir que determinadas ações só funcionem em conjunto. Em outras palavras, podemos dizer que caso ocorra algum erro, as demais sejam canceladas. Veja como utilizar:

	$db = Database::factory();
	try
	{
		$db->transaction();
		$db->User->insert(new User());
		$db->commit();
	}
	catch(DatabaseException $e)
	{
		$db->rollback();
	}

Os métodos da transação ficam diretamente na classe `Database`, isso porque a transação será para todas as tabelas, não somente para uma.

## transaction() ##
Método responsável por inicial a transação.

## commit() ##
Esse é o método a ser chamado caso não ocorram exceções durante a execução das instruções. Ele confirma o envio das instruções ao banco de dados.

## rollback() ##
Caso ocorra algum erro em alguma das instruções, você deve chamar o método `rollback()` para cancelar o conjunto de ações, referente ao banco de dados, dentro da transação.
