# Controller #
Os controllers são responsáveis pelo fluxo da aplicação e validação dos dados. O controller, no Trilado, é uma classe que herda da classe `Controller` e fica dentro do diretório `app/controllers`. Veja um exemplo:

	<?php
	class HelloController extends Controller {}

No exemplo acima, criamos o controller `Hello`. Os métodos do controller são chamados de action, que representam as páginas (ou outras ações) do sistema.

	<?php
	class HelloController extends Controller
	{
		public function world()
		{
			return $this->_print('Hello world!');
		}
	}

~! Todas as actions são obrigadas a enviar possuir um retorno. Você pode saber mais sobre os tipos de retorno na seção [Controller/Retornos](~/guide/controller/return). ~!

No exemplo acima, a action pode ser acessada pelo endereço `exemplo.com/hello/world`. Mesmo a classe tendo o nome composto pela palavra Controller, a URL de acesso não contém a palavra. Os controllers, podem ter nomes compostos, por exemplo:

	<?php
	class MyHelloController extends Controller
	{
		public function world()
		{
			return $this->_print('Hello world!');
		}
	}


Veja que o nome da classe `MyHelloController` segue o padrão UpperCamelCase, onde cada palavra é iniciada com Maiúsculas e unidas sem espaços. Nesses casos, de nomes compostos, a URL de acesso fica `exemplo.com/my-hello/world`, com as palavras separadas por um hífen.

## Parâmetros ##
As actions podem receber parâmetros, por meio da URL, informados pelo usuário. Esses parâmetros são recebidos pelas actions por meio de seus parâmetros, como um método comum. Veja o exemplo:

	<?php
	class HelloController extends Controller
	{
		public function world($name)
		{
			return $this->_print('Hello '. $name .'!');
		}
	}

No exemplo, a URL acessada será `exemplo.com/hello/world/Maria`. Podem ser passados quantos parâmetros forem necessários, inclusive, podem existir parâmetros nulos, removendo a obrigatoriedade de passagem destes parâmetros para acessar a action.

	<?php
	class NewsController extends Controller
	{
		public function show($id, $slug = null)
		{
			return $this->_print('Id: '. $id);
		}
	}

No exemplo acima, a URL pode ser acessada de duas maneiras, informando o primeiro parâmetro, `exemplo.com/news/show/1`, ou informando os dois, `exemplo.com/news/show/1/title-example`. Porém, nesse caso, se não for informado nenhum parâmetro, o Trilado irá retorna um erro 404, isso porque o parâmetro `$id` é obrigatório.

### Querystring ###
As querystring's são capturadas normalmente utilizando a variável `$_GET`. Veja um exemplo:


	<?php
	class NewsController extends Controller
	{
		public function show($id)
		{
			$search = isset($_GET['s']) ? $_GET['s'] : '';
			return $this->_print('Id: '. $id . ' Filtro: '. $search);
		}
	}

No exemplo acima, a URL pode ser acessada informando a querystring ou não, por exemplo, `exemplo.com/news/show/3` ou `exemplo.com/news/show/3?s=test`.

## Métodos ##
A classe controller contém alguns métodos para auxiliar o desenvolvedor.

### Criando Variáveis ###
No controller é possível definir variáveis que serão repassadas para view, para isso, deve-se utilizar o método `_set()`, que recebe dois parâmetros, o primeiro é o nome variável, o segundo é o valor da variável. Veja um exemplo de como utilizar:

	<?php
	class NewsController extends Controller
	{
		public function show()
		{
			$this->_set('title', 'Exemplo');
			$this->_set('tags', array('exemplo', 'código', 'trilado'));

			return $this->_view();
		}
	}

~! O nome da variável deve respeitar as mesmas regras de criação de variável em PHP, não podendo conter acentos, espaços ou caracteres especiais. Não pode começar com número. ~!

O exemplo acima poderia ser apresentado dessa maneira na view:

	<h1><?= $title ?></h1>
	<?php foreach($tags as $t): ?>
		<p><?= $t ?></p>
	<?php endforeach ?>

### Flash Message ###
Flash Message, no Trilado, é para definirmos uma mensagem que irá aparecer para o usuário. Seu uso não é obrigatório, essa opção foi criada apenas para auxiliar os desenvolvedores. O método `_flash()` recebe dois parâmetros, sendo o primeiro a classe que elemento que será gerado e o segundo texto que irá aparecer.

	<?php
	class NewsController extends Controller
	{
		public function show()
		{
			$this->_flash('success', 'Isto é uma mensagem de sucesso');

			return $this->_view();
		}

		
		public function error()
		{
			$this->_flash('error', 'Isto é uma mensagem de erro');

			return $this->_view();
		}
	}

Na view, para exibição da mensagem, devemos imprimir a constante `FLASH`. Por exemplo:

	<?= FLASH ?>

A mensagem só irá aparecer se existir, no contrário, a constante retorna vazio.

~? Utilize o CSS para estilizar a `div` com a mensagem, sendo a classe a mesma informada como primeiro parâmetro. ~?

### Preechimento Automático ###
É possível preencher as propriedades de um objeto automaticamente a partir do conteúdo passado através da variável `$_POST`. Para isso é necessário que o objeto seja um Model e as posições da `$_POST` possuam os mesmos nomes que as propriedades do objeto. Isso pode ser feito através do método `_data()`.

	<?php
	class NewsController extends Controller
	{
		public function create()
		{
			$news = new News();
			if(IS_POST)
			{
				$this->_data($news);
				$news->save();
			}
			return $this->_view($news);
		}
	}
	
~? Utilize os names dos inputs na view iguais aos nomes das propriedades dos models para fazer com que as posições da variável `$_POST` possuam os mesmos nomes destas propriedades. ~?

## Behaviors ##
No Controller ainda existem duas funções chamadas `beforeRender()` e `afterRender($response)` que são executadas respectivamente antes e depois da renderização das páginas. Estas classes são utilizadas para adicionar comportamentos padrões às actions de um controller, como por exemplo verificação de permissões especiais, ou atribuições de variáveis.

	<?php
	class NewsController extends Controller
	{
		protected $User;
		
		public function edit($id)
		{
			$news = News::get($id);
			
			if(IS_POST)
			{
				$this->_data($news);
				$news->UserId = $this->User->Id;
				$news->save();
			}
			
			return $this->_view();
		}

		public function beforeRender()
		{
			$this->User = Session::get('user');
		}
		
		public function afterRender($response)
		{
			//Isso não faz nada...
			return parent::afterRender($response);
		}
	}