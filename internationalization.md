# Internacionalização #
Ao criar uma aplicação, você pode querer disponibilizá-la em diversos idiomas, sem a necessidade de implementá-la novamente. Isso é possível utilizando o sistema de internacionalização que o Trilado disponibiliza.

Para fazer uma aplicação em português e inglês, basta definir qual das duas será a linguagem padrão, por exemplo, o português, depois crie um arquivo de tradução com a singla do idioma, por exemplo `app/locale/en.lang`.

~! As singlas devem estar em minúsculo e em caso de quatro letras, use hífen `-` ao invés de underline `_`. ~!

Dentro do arquivo, escreva a tradução, na qual a linha que começar com `msgid` deverá ser na linguagem padrão e linha que começar com `msgstr` será a tradução. Veja um exemplo:

	msgid "isso é apenas um teste"
	msgstr "this is an test"

	msgid "olá mundo"
	msgstr "hello world"

Você pode comentar as linhas usando `#` no início do texto, como por exemplo:

	msgid "isso é apenas um teste"
	msgstr "this is an test"

	#isso é um comentário
	msgid "Olá mundo"
	msgstr "Hello world"

Para utilizar a tradução no meio texto, o Trilado oferece duas funções, a `__()` e a `_e()`, na qual a primeira retorna o valor traduzido e a segunda imprime o valor. Caso o valor não tenha sido traduzido pelo programador, dentro do arquivo de tradução, será retornado o próprio valor.

	<h1><?= __('Olá mundo') ?></h1>
	<p><?php _e('Seja bem-vindo') ?></p>

No exemplo acima estamos utilizando as duas formas. A primeira o conteúdo está sendo retornado pela função e impresso pelo PHP, já no segundo o valor está sendo impresso diretamente pela função. Outro detalhe é que o primeiro definimos a tradução, a função irá apresentar `Hello world` quando, somente quando, acessarmos a versão em inglês, já a outra irá apresentar o próprio texto `Seja bem-vindo`, pois não traduzimos.

~? Os textos são case sensitive, ou seja, tem diferenciação de maiúscula para minúscula. ~?

Para apresentarmos a versão em inglês, basta acessarmos o endeço do site com `en/`, pois é a sigla que definimos no nome do arquivo. No nosso exemplo ficaria `exemplo.com/en/`.

Uma página que estivesse no seguinte endereço `exemplo.com/news/view/3`, caso tivesse tradução para o inglês, poderiamos acessar o endereço `exemplo.com/en/news/view/3`.
