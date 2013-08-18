# Active Record #
Para facilitar a manipulação de dados, o Trilado Framework implementa, também, o padrão Active Record, que consiste em métodos de manipulação na própria instância de `Model`. Veja um exemplo:

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

No exemplo acima, estamos criando a classe `Post` que herda de `Model`. Essa classe está fazendo uma representação da tabela `post`. Por herdar de `Model`, a classe `Post` já implementa os métodos do padrão Active Record.

## Selecionar ##
O método `get()` seleciona um registro na entidade referente ao model buscando-o pela chave primária, de acordo com a anotação `Key="Primary"`:

	$post = Post::get(3);

## Listar ##
Para retornarmos uma lista com os últimos 10 post's, por exemplo, poderiamos então utilizar o método `all()`, conforme o exemplo a seguir:

	$posts = Post::all(1, 10, 'Date', 'DESC');

Este método é desenvolvido para utilizar, por padrão, paginação nos resultados. Sendo assim, no exemplo acima o resultado será um objeto contendo duas propriedades, que são: 

| Propriedade | Descrição  |
| ----------- | ---------- |
| `Data` | que contém um `array` com os dados paginados. |
| `Count`| que contém a quantidade total de resultados. |

Para utilizar a paginação, os parametros passados são:

| Parâmetro | Descrição |
| --------- | --------- |
| `p`       | Número da página. |
| `m`       | Quantidade máxima de registros por página. |
| `o`       | Coluna, em banco, pela qual será feita a ordenação. |
| `t`       | Tipo da ordenação (`asc` ou `desc`). |


~! Veja que a contagem de páginas não é 'zero-based', não começa em zero. ~!

## Buscar ##
Para retornarmos uma lista com os últimos 10 post's, por exemplo, poderiamos então utilizar o método `search()`, conforme o exemplo:

	$posts = Post::search(1, 10, 'Date', 'DESC', array('Title' => '%example%'));

 No exemplo acima, o resultado será um objeto contendo duas propriedades, que são:

| Propriedade | Descrição  |
| ----------- | ---------- |
| `Data` | que contém um `array` com os dados paginados. |
| `Count`| que contém a quantidade total de resultados. |

Este método funciona semelhantemente ao método `all`, isto é, utiliza o mesmo sistema de paginação, e os mesmos parâmetros. Além destes parâmetros, iguais ao método `all`, existe ainda um parametro para realizar a busca. O ultimo parâmetro é o array `filters` que deve ser preenchido com filtros a partir dos quais irá se realizar a pesquisa no banco de dados.

## Salvar ##
Para salvar um novo registro, deve-se criar uma nova instância da classe referente ao model, preencher os valores das propriedades e chamar o método `save()`.

	$post = new Post();
	$post->Title = 'Example';
	$post->Date = time();
	$post->Content = 'Hello World!';

	$post->save();

Caso alguma propriedade obrigatória, definida pela marcação `@Required()`, esteja vazia, será disparada uma exceção `ValidationException`, porém, somente se a configuração `validate` do banco de dados estiver com o valor `true`. Em caso de erro ao salvar, a exceção `DatabaseException` será disparada.

## Editar ##
Para editar um registro, deve-se primeiro chamar o método `get()`, que contém uma instância da classe referente ao model, preencher os novos valores das propriedades e chamar o método `save()`.

	$post = Post::get(2);
	$post->Title = 'New Example';

	$post->save();

De modo semelhante ao anterior, se alguma propriedade obrigatória, definida pela marcação `@Required()`, estiver vazia, será disparada uma exceção `ValidationException`, porém, somente se a configuração `validate` do banco de dados estiver com o valor `true`. Em caso de erro ao salvar, a exceção `DatabaseException` será disparada.

## Deletar ##
Para excluir um registro, deve-se primeiro chamar o método `get()`, que contém uma instância da classe referente ao model e chamar o método `save()`.

	$post = Post::get(5);
	$post->delete();

----------

~? A classe que herda de `Model` pode conter novos métodos ou ter os existentes sobrescritos. ~?