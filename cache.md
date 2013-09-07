l# Cache #
No Trilado Framework é possível gravar dados em cache para deixar o processamento mais rápido. Por exemplo, sua aplicação necessita listar todos os arquivos de um determinado diretório a cada requisição. Você pode fazer esse procedimento uma vez, depois é só gravar em cache durante o período que você determinar, quando necessitar novamente é só ler do cache.

As formas de armazenamento em cache variam, o Trilado tem suporte, por meio dos cachesource, a quatro formas de armazenamento. São elas em disco, memória RAM via APC, via memcache e memcached.

~! Para utilizar o Apc, Memcache e Memcached, será necessário instalar o driver, no caso primeiro, e os demais o software memcached ~!

Independete da forma que você escolher para armazenar, o procedimento de manipulação do cache será o mesmo, pois as classes herdam da classe abstrada `Cachesource`.

## Gravar ##
O método para gravar dados no cache é o `write()`, que recebe três parâmetros, sendo o primeiro a chave em que os dados serão gravados, essa chave serve para recuperar os dados posteriormente. O segundo parâmetro são os dados a serem gravados. Por último você deve informar o tempo, em minutos, que os dados permanecerão no cache.

	$user = User::get(3);
	$cache = Cache::factory();
	$cache->write('example', $user, 30);

No exemplo acima estamos buscando um usuário no banco de dados e gravando ele em cache, assim, quando necessitarmos dele novamente, não será necessário realizar uma busca no banco novamente. No exemplo, usamos 30 minutos.

## Recuperar ##
O método para recuperar os dados do cache é o `read()`, que recebe um único valor, a chave em que os dados foram gravados.

	$cache = Cache::factory();
	$user = $cache->read('example');

Caso exista valor da chave especificada, o método retorna os dados, no contrário ele retorna `null`. No exemplo acima, se não tiver passado o tempo de 30 minutos em que gravamos o cache, será retornado o objeto com os dados do usuário gravado, mas caso tenha encerrado, retorna `null`.

## Existe ##
Podemos verificar se um existe e ainda não expirou. Para isso, basta utilizarmos o método `has()`, que recebe como parâmetro a chave em que os dados foram gravados.

	$cache = Cache::factory();
	if($cache->has('example'))
	{
		echo 'cache existe';
	}

O método retorna `true` caso o valor exista, caso contrário, retorna `false`.

## Remover ##
Podemos remover os dados de um cache específico. Para isso, basta utilizarmos o método `delete()`, que recebe como parâmetro a chave em que os dados foram gravados.

	$cache = Cache::factory();
	$cache->delete('example');

O método retorna `true` caso consiga remover os dados, caso contrário, retorna `false`.

## Remover Todos ##
As vezes é necessário limpar os dados do cache. Para isso, basta utilizarmos o método `clear()`, que remove todos os registros no cache.

	$cache = Cache::factory();
	$cache->clear();

O método retorna `true` caso consiga remover os dados, caso contrário, retorna `false`.

Veja um exemplo completo de utilização do cache:

	$cache = Cache::factory();
	if($cache->has('example'))
	{
		$user = $cache->read('example');
	}
	else
	{
		$user = User::get(3);
		$user->write('example', $user, 30);
	}