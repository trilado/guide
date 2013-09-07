# Erros #
Por padrão, o Trilado vem com o debug habilitado. Caso você acesse sua aplicação via localhost, ao disparar um erro, o framework irá apresentar uma tela de debug com informações detalhadass no erro.

Ao colocar a aplicação no ambiente de produção, você **não** irá querer passar informações detalhada dos erros para os visitantes. Pensando nisso, definimos que o Trilado não irá apresentar esse debug quando o usuário não estiver acessando localmente, ao invés disso, ele irá apresentar uma página de erro que você pode personalizar.

Para personalizar uma página, basta criar um arquivo com o número do erro dentro do diretório `app/views/_errors/`. Por exemplo, o erro 404, você pode criar o arquivo `app/views/_errors/404.php`. O mesmo serve para o erro 500 e 403.

Caso você não crie as páginas de erro, o Trilado irá apresentar uma página padrão ao usuário.