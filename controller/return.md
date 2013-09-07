# Retornos #
Uma action nada mais é que um método de um classe que herda de `Controller`. A action deve obrigatoriamente possuir um retorno para a classe que irá renderizar a página, para isso, a classe `Controller` implementa vários métodos que podem ser utilizado para retorno da action.

## _view() ##
Esse é o método mais comum, que retorna uma view com o template. O método pode receber três parâmetros, que são opcionais, conforme os exemplos a seguir:

### _view() ###
Retorna uma view com o mesmo nome da action. Por exemplo, se a action se chamar `add`, a view será `app/views/example/add.php`.

	<?php 
	class ExampleController extends Controller
	{
		public function add()
		{
			return $this->_view();
		}
	}


### _view('name') ###
Retorna uma view com o nome especificado no parâmetro.

	<?php 
	class ExampleController extends Controller
	{
		public function add()
		{
			return $this->_view('form');
		}
	}

No exemplo, a view será `app/views/example/form.php`.

### _view($data) ###
Retorna uma view com o nome da action. Além disso, cria uma variável com o nome `$model`, que pode ser acessada da view, com o valor passado como parâmetro. Podem ser passados parametros dos tipo `array` e `object`, porém **não** podem ser enviados valores do tipo `string`.

	<?php 
	class ExampleController extends Controller
	{
		public function add()
		{
			$test = new stdClass;
			$test->Name = 'Jhon';
			return $this->_view($test);
		}
	}

No exemplo acima, como a action não está especificando o nome da view, o Trilado irá considerar o arquivo com o nome da action, no caso, `app/views/example/add.php`

### _view('name', $data) ###
Retorna uma view com o nome especificado no parâmetro cria uma variável com o nome `$model` com o valor do segundo parâmetro.No exemplo está `array`, porem o valor pode ser `object`, **não** podendo ser `string`.

	<?php 
	class ExampleController extends Controller
	{
		public function add()
		{
			$test = new stdClass;
			$test->Name = 'Jhon';
			return $this->_view('form', $test);
		}
	}

No exemplo, a view será `app/views/example/form.php`

### _view('controller_name', 'view_name') ###
Retorna uma view com o nome especificado no segundo parâmetro, que pertence ao controller com o nome especificado no primeiro parâmetro. Apesar de usar o nome controller, essa forma apenas reaproveita uma view de outro controller, sem a execução da action. 

	<?php 
	class ExampleController extends Controller
	{
		public function add()
		{
			return $this->_view('basic','form');
		}
	}

No exemplo, a view será `app/views/basic/form.php`

### _view('controller_name', 'view_name', $data) ###
Retorna uma view com o nome especificado no segundo parâmetro, que pertence ao controller com o nome especificado no primeiro parâmetro. Apesar de usar o nome controller, essa forma apenas reaproveita uma view de outro controller, sem a execução da action. O terceiro parâmetro cria automaticamente uma variável com o nome `$model` que recebe o segundo valor passado como parâmetro. Podem ser passados parametros dos tipo `array` e `object`, porém **não** podem ser enviados valores do tipo `string`.

	<?php 
	class ExampleController extends Controller
	{
		public function add()
		{
			$test = new stdClass;
			$test->Name = 'Jhon';
			return $this->_view('basic', 'form', $test);
		}
	}

No exemplo, a view será `app/views/basic/form.php`

## _page() ##
Esse método retorna uma view, porém, sem template, apenas o conteúdo da view. O método pode receber três parâmetros, que são os mesmo do método `_view`.

	<?php 
	class ExampleController extends Controller
	{
		public function add()
		{
			$test = new stdClass;
			$test->Name = 'Jhon';
			return $this->_page('form', $test);
		}
	}

## _snippet() ##
Os snippet's são views bastantes utilizadas, que não pertencem a controllers, ficam no diretório `app/views/_snippet`. O método pode receber dois parâmetros, o primeiro é obrigatório, que é o nome do snippet. O segundo é opcional, que criar automaticamente uma variável com o nome `$model` com o valor do parâmetro. Esse pode também ser string.

	<?php 
	class ExampleController extends Controller
	{
		public function hello()
		{
			return $this->_snippet('message');
		}
	}

Veja outro exemplo:

	<?php 
	class ExampleController extends Controller
	{
		public function hello()
		{
			$title = 'Message Example';
			return $this->_snippet('message', $title);
		}
	}

Nos exemplos, o snippet utilizado será `app/views/_snippet/message.php`.

## _content() ##
Define um conteúdo a ser apresentado no template na renderiação. Não precisa da utilização de view. Recebe um parâmetro com o valor a ser impresso, que é obrigatório.

	<?php 
	class ExampleController extends Controller
	{
		public function hello()
		{
			$data = 'Content Example';
			return $this->_content($data);
		}
	}

## _print() ##
Imprime um conteúdo da tela, sem utilização de view ou template, e encerra a execução do código. Recebe um parâmetro, que é o conteúdo a ser impresso.

	<?php 
	class ExampleController extends Controller
	{
		public function hello()
		{
			$data = 'Content Example';
			return $this->_print($data);
		}
	}

## _json() ##
Define um JSON a ser impresso na respota da requisição. Recebe um parâmetro, que é obrigatório. O valor do parâmetro é convertido para o formato JSON.

	<?php 
	class ExampleController extends Controller
	{
		public function hello()
		{
			$test = new stdClass;
			$test->Name = 'Jhon';
			return $this->_json($test);
		}
	}

O método irá imprimir um conteúdo com o cabeçalho JSON:

	{"d":{"Name":"Jhon"}}

## _xml() ##
Define um XML a ser impresso na respota da requisição. Recebe um parâmetro, que é obrigatório. O valor do parâmetro é convertido para o formato XML.

	<?php 
	class ExampleController extends Controller
	{
		public function hello()
		{
			$test = new stdClass;
			$test->Name = 'Jhon';
			return $this->_xml($test);
		}
	}

O método irá imprimir um conteúdo com o cabeçalho XML:

	<?xml version="1.0" encoding="UTF-8"?>
	<d>
		<Name>Jhon</Name>
	</d>

~! Os métodos são definidos como `final` e não podem ser sobrescritos. ~!