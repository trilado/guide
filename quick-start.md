# Guia Rápido #
Para aqueles apreçadinhos, ou programadores experientes que já dominam o padrão MVC.

## Model ##
No padrão MVC, o Model representa a classe em que deve ficar lógica de negócio da aplicação e a persistência com o banco de dados. No Trilado, a classe `Model` é, também, uma representação de uma entidade (view ou tabela) do banco de dados. Ela já vem com alguns métodos implementados para auxiliar a manipulação dos dados que a instância de `Model` representa.

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

		/** @Column(Type="String") */
		public $Content;
	}

~? Veja a documentação sobre as anotações do `Model` [aqui](~/guide/model/annotation). ~?

## Controller ##
Os controllers são responsáveis pelo fluxo da aplicação e validação dos dados. O controller, no Trilado, é uma classe que herda da classe `Controller` e fica dentro do diretório `app/controllers`. Veja um exemplo:

	<?php
	class HelloController extends Controller
	{
		public function world()
		{
			return $this->_print('Hello world!');
		}
	}

~! Todas as actions são obrigadas a retornarem algo para a aplicação. Você pode saber mais sobre os tipos de retorno [aqui](~/guide/controller/return). ~!

## View ##
View são as páginas que contém o HTML para visualização dos conteúdo. As views ficam dentro do diretório `app/views/[controller]/[action].php`, sendo que o nome do arquivo não precisa obrigatoriamente conter o mesmo nome da action, desde que no retorno esteja especificado o nome do arquivo. As variáveis passadas da action para a view podem ser usadas normalmente.

	<p>Seja bem-vindo <?= $name ?></p>
