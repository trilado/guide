# Instalação #

Como o objetivo do Trilado Framework é facilitar o desenvolvimento de sites, sua instalação não poderia ser complicada. Porém, alguns requisitos básicos são necessários, configurações que na maioria dos servidores, principalmente terceirizados, já vêm instaladas e definidas.

Esse tutorial de instalação foi feito para a versão **2.1.x**, portanto, pode não servir para outras versões.

## Requisitos ##

Para utilização do Trilado Framework, será necessário que o servidor contenha os seguintes requisitos:

- Servidor HTTP (Apache, Nginx ou outro);
- Módulo de Reescrita de URL (mod_rewrite);
- PHP 5.2 ou superior;
- Módulo [SPL](http://www.php.net/manual/en/book.spl.php) do PHP.

## Download ##

Faça o download do Trilado Framework, nesse caso, da versão 2.1, para isso, basta acessar o diretório de downloads no [GitHub](https://github.com/trilado/trilado/releases).

### Via Git ###

Você pode baixar o projeto via linha de comando. Como mostra o seguinte código:

	git clone https://github.com/trilado/trilado.git

Após o download, extraia os arquivos dentro do diretório público do seu servidor HTTP.

## Configuração do Módulo de Reescrita de URL ##

Esse passo também é essencial para o funcionamento do Trilado, pois, como citado acima, é necessário que o servidor HTTP contenha o módulo de reescrita de URL.

### Apache ###

O Trilado fornece, por padrão, os arquivos `/.htaccess` e `/app/wwwroot/.htaccess`. Ambos contêm a configuração de reescrita para o Apache. Nesse caso é necessário apenas a ativação do `mod_rewrite`.

### Nginx ###

