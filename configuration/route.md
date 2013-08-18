# Rotas #

Rotas são, resumidamente, reescritas de URL's. O Trilado oferece rotas simples utilizando expressões regulares.

Para criar uma rota, deve-se editar o arquivo `app/routes.php` e adicionar uma chamada do método `Route::add()` passando como parâmetro o novo caminho e o caminho original. Veja um exemplo:

	Route::add('^about$','profile/about');

No exemplo acima ao acessar `about`, o usuário estará acessado o endereço `profile/about`. O caractere '^' é utilizado na [Expressão Regular](http://pt.wikipedia.org/wiki/Express%C3%A3o_regular) para especificar que a URL deve começar com a palavra 'about' e o '$' que irá terminar com a mesma, ou seja, a URL deve ser examente igual à 'about'.

Pode-se ainda, utilizar expressões regulares mais avançadas:

	Route::add('^news/([\d]+)/([a-z0-9\-]+)$','news/show/$1/$2');

Nesse caso a URL que começar com a palavra 'news/[numero]/[slug]' irá chamar o controller `NewsController` e a action `show()`, passando como primeiro parâmetro o 'número' e como segundo o 'slug'.