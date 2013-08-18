# Consultas  #

## all() ##
Executa a instrução e retorna um `array` com os resultados. Caso não encontre resultados, retorna um `array` vazio. Por exemplo:

	$db->User->all();

Como no exemplo estamos usando o model `User`, o resultado será um `array` de objetos `User`.

## single() ##
Executa a instrução e retorna um objeto. Caso não encontre resultados, retorna `null`. Se encontrar mais de um resultado, somente o primeiro será retornado. Por exemplo:

	$db->User->single();

Como no exemplo estamos usando o model `User`, o resultado será um objeto `User`.

## where() ##
No método `where` especificamos um condicional para nossa consulta. Esse método retorna uma instância da própria classe, ou seja, uma instância de `Datasource`. Nesse método é necessário informar, no mínimo, dois parâmetros. O primeiro deve conter o condicional, o segundo deve conter os valores dos condicionais.

	$db->User->where('Level = ?', 1)->all();

Veja um exemplo que utiliza mais de um condicional:

	$db->User->where('Level = ? AND Status = ?', 1, true)->all();

Os métodos `all()` e `single()` podem receber o condicional como parâmetro, funcionando exatamente igual ao método `where`. É uma forma de abreviar. Veja os exemplos:

	$db->User->all('Level = ?', 1);
	$db->User->single('Id = ?', 1);

## orderBy() ##
Cria uma cláusula de ordenação. Pode receber dois parâmetros, sendo somente o primeiro obrigatório. No primeiro você deve informar o nome da coluna que deseja ordenar, já no segundo você informa qual tipo de ordenação, `ASC` ou `DESC`. Se não for informado, o segundo parâmetro tem como valor padrão o `ASC`. Veja os exemplos:

	$db->User->orderBy('Name')->all();
	$db->User->orderBy('Name', 'DESC')->all();

## orderByDesc() ##
Esse recebe somente um parâmetro, o nome da coluna, pois como o nome do método já diz, irá ordenar em forma decrescente, ou seja, `DESC`. Por exemplo:

	$db->User->orderByDesc('Name')->all();

## offset() ##
Define o ponteiro de onde os resultados devem começar. Por exemplo, se a quantidade de resultados fosse 25 items, você poderia definir para começar no elemento 5, ou seja, retornaria apenas os 20 últimos. Veja um código de código:

	$db->User->offset(5)->all();

## limit() ##
Define um limite máximo de resultados. Por exemplo, se a quantidade de resultados fosse 25 items, você poderia definir o limite em 7 elementos, isto retornaria apenas os 7 primeiros resultados. Veja no código:

	$db->User->limit(7)->all();

Ainda pode ser informado outro parâmetro que define o `offset()`. Por exemplo, se a quantidade de resultados fosse 25 items, você poderia definir o limite em 7 elementos e iniciar no elemento 3, ou seja, retornaria apenas os 7 primeiros resultados depois do terceiro. Veja no código:

	$db->User->limit(7, 3)->all();

## groupBy() ##
Para agrupar os resultados pode-se utilizar o método `groupBy()`.

## avg() ##
O método `avg()` serve para calcular a média dos valores de uma coluna específica (essa coluna deve ser numérica). Deve ser informado como parâmetro o nome da coluna, o método retorna um número com a média. Por exemplo:

	$db->ViewUser->avg('Age');

No exemplo acima, utilizamos uma view que contém a coluna `Age`, com as idades dos usuários. O método irá somar as idades e dividir pela quantidade de resultados.

## count() ##
Para contar a quantidade de resultados que será retornado, pode-se utilizar o método `count`. O método retorna um inteiro. Veja o código:

	$db->User->count();

## sum() ##
O método `sum()` é para somar os valores de uma coluna (essa coluna deve ser numérica). Deve ser informado como parâmetro o nome da coluna, o método retorna o resultado da soma. Por exemplo:

		$db->ViewUser->sum('Age');

No exemplo acima, utilizamos uma view que contém a coluna `Age`, com as idades dos usuários. O método irá somar as idades e retornar o valor.

## max() ##
Retorna o maior valor de uma coluna (essa coluna deve ser numérica). Deve ser informado como parâmetro o nome da coluna. Por exemplo:

			$db->ViewUser->max('Age');

No exemplo acima, utilizamos uma view que contém a coluna `Age`, com as idades dos usuários. O método irá retorna a idade da pessoa mais velha.

## min() ##
Retorna o menor valor de uma coluna (essa coluna deve ser numérica). Deve ser informado como parâmetro o nome da coluna. Por exemplo:

			$db->User->min('Id');

No exemplo acima, é utilizada uma tabela que contém a coluna `Id`, com ID's dos usuários. O método irá retorna a menor idade.

## distinct() ##


## from() ##
Por padrão, a tabela a ser seleciona é a que o model faz referência, porém, caso queria alterar, basta chamar o método `from` informando o nome do novo model.

	$db->User->from('Profile')->all();

## lastInsertId() ###
Retorna o último ID inserido **recentemente**.

	$db->User->lastInsertId();

~! Caso se passe muito tempo sem novas inserções a função não irá retornar o valor. ~!

## paginate() ##
Esse método é composto pela mistura de vários outros para retornar o resultado paginado. Veja como seria a implementação de uma paginação sem a utilização deste método:

	$data = $db->User->offset(0)->limit(10)->all();
	$count = $db->User->offset(0)->limit(10)->count();

Agora veja a mesma consulta utilizando o método `paginate()`:

	$db->User->paginate(1, 10);

O método recebe dois parâmetros, sendo o número da página (começa com 1) e a quantidade de itens por página. O resultado será um objeto contendo duas propriedades: `Data`, que contem um `array` com os resultados; e `Count`, que retorna a quantidade total de resultados.

## query() ##
Por meio do método `query()` é possível executar uma instrução SQL livremente.

	$db->query('SELECT * FROM user');

## whereArray() ##
Uma forma de deixar os condicionais um pouco mais flexíveis, é utilizar o método `whereArray`, no qual o usuário pode informar um `array` com os valores dos condicionais.

	$db->User->whereArray('Level = ? AND Status = ?', array(1, true))->all();

## whereSQL() ##
Outra forma de deixar os condicionais um pouco mais flexíveis, é a utilização do método `whereSQL`, neste método o desenvolvedor pode informar um SQL sem definir os valores dos condicionais.

	$db->User->whereSQL('Level = 1 AND Status = 1')->all();

### Manipulação dos Dados ###
Utilizando a classe `Database` também é possível fazer a manipulação dos dados, ou seja, cadastrar, editar e remover registros de uma tabela.

## insert() ##
Com o método `insert()` você insere um objeto cuja as propriedades serão transformadas em instruções SQL e inseridas no banco. Esse método recebe como parâmetro uma instância de `Model` referente à entidade que você estiver trabalhando. Por exemplo:

	$user = new User();
	$user->Name	= 'Jhon';
	$user->Level = 1;
	$user->Status = 1;
	
	$db = Database::factory();
	$db->User->insert($user);
	
	$db->save();

O método `insert()` não executa a instrução, somente o método `save()`. Observe que o método `insert()` é utilizado a partir de uma chamada da entidade. Já o `save()`, veio direito da variável `$db`.

## update() ###
Um pouco parecido com o método `insert()`, o `update()` serve para atualizar um registro existente no banco de dados. Você deve informar como parâmetro uma instância do model referente à entidade que estive trabalhando.

	$user = User::get(2);
	$user->Level	= 1;
	$user->Status	= 1;
	
	$db = Database::factory();
	$db->User->update($user);
	
	$db->save();

Observe que utilizamos o método `get()`, isso porque para usarmos o `update()`, devemos informar uma instância recuperada do banco de dados. Se informarmos uma instância nova do model, o framework irá disparar uma exceção.

## delete() ##
Funciona semelhante aos anteriores, porém sua finalidade é remover um registro do banco de dados.

	$user = User::get(2);

	$db = Database::factory();
	$db->User->delete($user);
	
	$db->save();

Observe que utilizamos o método `get()`, isso porque para usarmos o `delete()`, devemos informar uma instância recuperada do banco de dados. Se informarmos uma instância nova do model, o framework irá disparar uma exceção.

## deleteAll() ##
A diferença entre os métodos `delete()` e `deleteAll()` é que o primeiro remove um único registro, utilizando a chave primária como condicional. Já o segundo utiliza o condicional que você informar. Existem duas formas de informar o condicional, veja:

	$db = Database::factory();
	$db->User->where('UserId = ?', 3)->deleteAll();
	
	$db->save();

Veja que utilizando o método `where()`, que foi apresentado anteriormente. As demais formas também podem ser utilizadas. A segunda forma é mais compacta, na qual passamos o condicional como parâmetro do método `deleteAll()`, assim como mostramos anteriormente no `all()` e no `single()`.

	$db = Database::factory();
	$db->User->deleteAll('UserId = ?', 3);
	
	$db->save();
