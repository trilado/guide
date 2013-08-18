# Autenticação #
Um dos recursos interessantes no Trilado Framework é a autenticação automática, que permite ao programador criar páginas restritas de modo muito fácil.

A primeira coisa a fazer é definir no arquivo de configuração, `app/config.php`, para qual o caminho irá ser direcionar o usuário, quando ele não estiver autenticado e tentar acessar uma página restrita.

	Config::set('default_login', '~/example/login');

Nesse caso o usuário será redirecionado para a action `login` dentro do controller `ExampleController`.

## Controller ##

É necessário criar a página de login. Para isso, crie a classe `ExampleController`, e implemente o método (ou action) `login()`, conforme o exemplo:

	<?php
	class ExampleController extends Controller
	{
		public function login()
		{
			if(is_post)
			{
				if($_POST['Login'] == 'test' && $_POST['Password'] == '123')
					Auth::set('admin');
				else
					$this->_flash('error', 'Login ou senha incorretos!');
			}
			return $this->_view();
		}
	}

O código acima é apenas um exemplo de login, sem acesso a base de dados. Nesse exemplo, se o usuário digitar o login e senha corretos, o método `Auth::set()` cria uma autenticação com o papel 'admin', porém, quem irá definir quais páginas podem ser acessadas pelo 'admin' é o desenvolvador (você).

Para verificar se o usuário tem permissão ou não, podemos utilizar o método `allow()` informando quais papéis têm acesso.

	public function add()
	{
		Auth::allow('admin');
		//código aqui
		return $this->_view();
	}

No exemplo acima, caso o usuário não tenha acesso de `admin`, ele será redirecionado para a página de login, no caso foi definido como `example/login`.

~? Utilizando anotações, você pode fazer esse mesmo processo do método `allow()`. Veja a seção [Anotações](~/guide/controller/annotation) dentro Controllers. ~?

## View ##
Na view será feito o formulário para o usuário logar.

	<form method="post" action="">
	    <label>
	        Login
	        <input type="text" name="Login" />
	    </label>
	    <label>
	        Login
	        <input type="password" name="Password" />
	    </label>
	    <input type="submit" value="Entrar" />
	</form>
