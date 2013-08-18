# Hook #
Em alguns casos quando ser necessário alterar o modo de funcionamento do Trilado. Usando hook não é necessário modificar o código-fonte do Framework.

Para utilizar um hook, você deverá criar uma classe, nela você deverá criar um método com o nome e os parâmetros de acordo com o hook e retornar os dados processados.

## Render ##
Após renderizar o conteúdo a ser impresso, o Trilado executa os hooks respectivos para esta tarefa de renderização. As classes adicionadas nesse hook devem conter o método `render()`.

A classe com o método do `render()`:

	<?php
	class MyRender
	{
		public function render($content)
		{
			$content = str_replace('AA', 'BB', $content);
			return $content;
		}
	}

O controller que adicionará o hook:

	<?php 
	class ExampleController extends Controller
	{
		public function __construct()
		{
			$this->Template->addHook(new MyRender());
		}
	}

No exemplo acima, a classe `MyRender` contém o método `render()`, que será chamado logo após a renderização do conteúdo. Como exemplo, substituimos todas ocorrência de AA por BB e retornamos o conteúdo de volta ao framework para que ele continue seu funcionamento.

## Mensagem Flash ##
Após renderizar a mensagem de flash a ser impressa, o Trilado executa os hooks que lhe forem vinculados para essa tarefa. As classes adicionadas nesse hook devemm conter o método `renderFlash()`.

A classe com o método do `renderFlash()`:

	<?php
	class MyRender
	{
		public function renderFlash($content)
		{
			$content = str_replace('AA', 'BB', $content);
			return $content;
		}
	}

O controller que adicionará o hook:

	<?php 
	class ExampleController extends Controller
	{
		public function __construct()
		{
			$this->Template->addHook(new MyRender());
		}
	}

No exemplo acima, a classe `MyRender` contém o método `renderFlash()`, que será chamado logo após a renderização da mensagem. Como exemplo, substituimos todas ocorrência de AA por BB e retornamos o conteúdo de volta ao framework para que ele continue seu funcionamento.

## Internacionalização ##
Após realizar a tradução de um texto, o Trilado executa os hooks que lhe forem vinculados para essa tarefa. As classes adicionadas nesse hook devem conter o método `get()`.

A classe com o método do `get()`:

	<?php
	class MyRender
	{
		public function get($content)
		{
			$content = str_replace('AA', 'BB', $content);
			return $content;
		}
	}

O controller que adicionará o hook:

	<?php 
	class ExampleController extends Controller
	{
		public function __construct()
		{
			$this->I18n->addHook(new MyRender());
		}
	}

No exemplo acima, a classe `MyRender` contém o método `get`, que será chamado logo após a tradução de um texto. Como exemplo, substituimos todas ocorrência de AA por BB e retornamos o texto de volta ao framework para que ele continue seu funcionamento.

~? Nessa versão, o Trilado apresenta apenas esses três hooks. No decorrer de sua evolução iremos implementando mais. ~?