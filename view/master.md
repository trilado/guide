# Master #
Master é o mesmo que template, ou seja, o layout da sua aplicação. É na Master onde são importados os arquivos javascript e css, por exemplo. Uma master é também uma view, deve estar salva dentro de `app/views/_master/` com o nome que será usado na anotação `@Master()` ou na configuração `default_template`. Veja um exemplo de master:

	<!DOCTYPE html>
	<html>
		<head>
			<title>Trilado Framework</title>
		</head>
		<body>
			<?= FLASH ?>
			<?= CONTENT ?>
		</body>
	</html>

Dentro da master são utilizadas duas constantes, a `FLASH` e a `CONTENT`, a segunda é obrigatória para o funcionamento correto do Trilado.

| Constante | Descrição       |
| --------- | --------------- |
| FLASH     | retorna uma mensagem enviada no método `Controller->_flash()` |
| CONTENT   | retorna o conteúdo a ser impresso, como de uma view, por exemplo |

~? O valor da constante deve ser impresso usando o `echo` ou `<?=`. ~?

Dentro da uma master pode-se utilizar as variáveis criadas na action, como por exemplo em título da página. Veja:

Conteúdo do Controller, que define a variável `$title`:

	<?php
	class ExampleController extends Controller
	{
		public function index()
		{
			$this->_set('title', 'Página Exemplo');
			return $this->_content('exemplo');
		}
	}

Conteúdo da master, que imprime a variável:

	<!DOCTYPE html>
	<html>
		<head>
			<title><?= $title ?></title>
		</head>
		<body>
			<?= FLASH ?>
			<?= CONTENT ?>
		</body>
	</html>

Nesse caso, é obrigatório que todas as actions tenham a definição da variável, caso contrário, o PHP irá disparar um erro informando que a variável `$title` não foi definida. Exitem duas formas de resolver esse problema, a primeira é verificar se a variável existe, por exemplo:

	<!DOCTYPE html>
	<html>
		<head>
			<title><?= isset($title) ? $title : 'Trilado Framework' ?></title>
		</head>
		<body>
			<?= FLASH ?>
			<?= CONTENT ?>
		</body>
	</html>

A outra forma é criar um construtor para o método e definir um valor padrão para a variável dentro do construtor. Por exemplo:

	<?php
	class ExampleController extends Controller
	{
		public function __construct()
		{
			$this->_set('title', 'Trilado Framework');
		}
		public function index()
		{
			$this->_set('title', 'Página Exemplo');
			return $this->_content('exemplo');
		}
	}

