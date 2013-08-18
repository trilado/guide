# Prefixos #

Prefixos são partes da URL definidas para categorizar métodos, normalmente utilizados para criar áreas de acesso como, por exmeplo, 'admin'. 

## Config ##

Os prefixo são definidos no arquivo de rotas `app/routes.php`, veja um exemplo:

	Route::prefix('admin');

No exemplo acima foi criado o prefixo `admin`, você poderá criar vários prefixos.

## Controller ##

Dentro do controller você pode definir métodos que fazem parte do prefixo, para isso, basta colocar `admin_` antes do nome do método.

### Exemplo ###

	<?php
	class ExampleController extends Controller
	{
		public function admin_hello()
		{
			return $this->_view();
		}
	}

Nesse exemplo foi criado o método 'admin_hello()', como já existe o prefixo `admin` (criado na seção anterior), o método pode ser acessado por meio do endereço `/admin/example/hello`. Veja que o prefixo vem antes do controller.

## View ##

As views devem ser criadas normalmente, com o mesmo nome do método, no nosso exemplo fica `app/views/example/admin_hello.php`.

Vale lembrar que poderá criar um método `hello()`, sem o admin, e esse não interfere no outro, tanto na URL, como no controller ou na view.

## Prefixo vs Rotas ##

Você poderá utilizar prefixos e rotas sem problemas, porém, as rotas são executadas primeiro que os prefixos, por exemplo:
	
	Route::prefix('admin');
	Route::add('^hello$','admin/example/hello');
	
A utilização de prefixo pode ser interessante quando deseja-se criar um controller que contenha tanto a parte pública como também a parte privada. Um exemplo disso seria um `NewsController`, na qual pode ter o método `index()`, que lista as notícias para os visitantes, ou o `admin_index()`, que lista as notícias para o administrador.

~? Caso crie o prefixo `admin`, ao acessar `/admin/`, sem informar qual controller ou action, irá executar o controller e a action padrão com o prefixo, no caso `admin_index`. ~?