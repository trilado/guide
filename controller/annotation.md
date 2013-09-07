# Anotações #
As anotações no Trilado, assim como em outros frameworks e linguagens de programação, funcionam como metadados de métodos e propriedades.

No controller, as anotações estão disponíveis apenas para as actions, nas quais podem ser definidas: o template que a action irá usar; e qual usuário pode acessar o conteúdo da action.

## @Auth() ##
A marcação `@Auth()` define quem poderá ter acesso à uma determinada action. Ela funciona em conjunto com a classe Auth e recebe como parâmetro o nome, entre aspas, dos papéis que porem ter acesso.

	<?php
	class NewsController extends Controller
	{
		/** @Auth("admin","manager") */
		public function add()
		{
			return $this->_print('add');
		}

		public function show($id)
		{
			return $this->_print('show: '. $id);
		}
	}

No exemplo acima, estamos definindo que os usuário com os papéis "admin" e "manager" poderão ter acesso. Caso um usuário que não esteja autenticado tente acessar essa action, ele será redirecionado para a página de login, conforme a configuração `default_login`. Se o usuário estiver autenticado, porém, não estiver em um dos papéis informados, o Trilado irá retorna um erro 403 de acesso negado.

Caso queria definir para todas actions, é só definir a marcação no construtor.

	<?php
	class NewsController extends Controller
	{
		/** @Auth("admin","manager") */
		public function __construct() {}

		public function add()
		{
			return $this->_print('add');
		}

		public function edit($id)
		{
			return $this->_print('edit: '. $id);
		}
	}

Você pode sobrescrever a marcação, por exemplo, caso queria definir para todas os actions de um controller, exceto de algum específico.

	<?php
	class NewsController extends Controller
	{
		/** @Auth("admin","manager") */
		public function __construct() {}

		public function add()
		{
			return $this->_print('add');
		}

		/** @Auth("admin") */
		public function edit($id)
		{
			return $this->_print('edit: '. $id);
		}

		/** @Auth("*") */
		public function show($id)
		{
			return $this->_print('edit: '. $id);
		}
	}

No exemplo acima, definimos no construtor que todas as action só serão acessadas por "admin" ou "manager", porém, a action `edit()` queremos que somente o "admin" tenha acesso. Já a action `show()`, queremos que todos (informando o "*"), mesmo sem autenticação, tenham acesso.

Nesse exemplo, que contém apenas três actions, não fica muito legal escrever no construtor e sobrescrevê-lo, mas imagine um controller com dez actions e uma delas não necessita de autenticação.

## @Master() ##
A marcação `@Master()` define qual será o template para uma determinada action. Assim como na maração `@Auth()`, você pode definir a marcação `@Master()` no construtor que se aplicará em todas as actions do controller. Essa marcação também pode ser sobrecrita.

	<?php
	class NewsController extends Controller
	{
		/** @Master("internal") */
		public function __construct() {}

		public function add()
		{
			return $this->_print('add');
		}

		public function edit($id)
		{
			return $this->_print('edit: '. $id);
		}

		/** @Master("public") */
		public function show($id)
		{
			return $this->_print('edit: '. $id);
		}
	}

Caso uma action não tenha uma master definida, nem pelo construtor, será aplicada a master da configuração `default_template`. Você pode, ainda, inserir marcações de autenticação e template em uma única action.

	<?php
	class NewsController extends Controller
	{
		/** 
		 * @Master("internal") 
		 * @Auth("admin","manager")
		 */
		public function __construct() {}

		public function add()
		{
			return $this->_print('add');
		}

		public function edit($id)
		{
			return $this->_print('edit: '. $id);
		}

		/** 
		 * @Auth("*")
		 * @Master("public") 
		 */
		public function show($id)
		{
			return $this->_print('edit: '. $id);
		}
	}

Mesmo definindo as marcações no construtor, se você tiver muitos controllers, dar manutenção pode-se tornar um pouco chato, já que deverá alterar em todos os controllers. Uma forma de facilitar esse trabalho é criar herança entre os controllers, por exemplo:

	<?php
	class AdminController extends Controller
	{
		/** 
		 * @Master("internal") 
		 * @Auth("admin","manager")
		 */
		public function __construct() {}
	}

O controller para definir a master não precisa conter actions, apenas o construtor. Os demais, ao herdarem de `AdminController` estarão com suas marcações.

	<?php
	class NewsController extends AdminController
	{
		public function add()
		{
			return $this->_print('add');
		}

		public function edit($id)
		{
			return $this->_print('edit: '. $id);
		}

		/** 
		 * @Auth("*")
		 * @Master("public") 
		 */
		public function show($id)
		{
			return $this->_print('edit: '. $id);
		}
	}

Mesmo os controllers que herdarem de outro controller, como no exemplo acima, poderão sobrescrever suas marcações, como foi apresentado na action `show()`.