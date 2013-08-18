# Model #
No padrão MVC, o Model representa a classe em que deve ficar lógica de negócio da aplicação e a persistência com o banco de dados. No Trilado, a classe `Model` é, também, uma representação de uma entidade (view ou tabela) do banco de dados. Ela já vem com alguns métodos implementados para auxiliar a manipulação dos dados que a instância de `Model` representa.

| Método     | Retorno  | Descrição |
| ------     | -------  | --------- |
| `get()`    | `Model`  | Consulte a API [Model::get(int $id)](~/api/class/Model#method:get). |
| `all()`    | `object` | Consulte a API [Model::all(int $p = 1, int $m = 10, string $o = 'Id', string $t = 'asc')](~/api/class/Model#method:all). |
| `search()` | `object` | Consulte a API [Model::search(int $p = 1, = 10, = 'Id', = 'asc', = array())](~/api/class/Model#method:search). |
| `save()`   | `void`   | Consulte a API [Model::save()](~/api/class/Model#method:save). |
| `delete()` | `void`   | Consulte a API [Model::delete()](~/api/class/Model#method:delete). |

Para utilizar o ORM (classe `Database`) será necessário criar uma classe que herda do `Model`, que já vem com alguns métodos implemetandos para facilitar o acesso ao banco. Veja um exemplo:

	<?php
	/** @Entity("post") */
	class Post extends Model
	{
		/**
		 * @AutoGenerate()
		 * @Column(Type="Int",Key="Primary")
		 */
		public $Id;

		/** @Column(Type="String") */
		public $Title;

		/** @Column(Type="Int") */
		public $Date;

		/** @Column(Type="String") */
		public $Content;
	}

~? Veja a documentação sobre as anotações do `Model` [aqui](~/guide/model/annotation). ~?

Além dos métodos já implementados
