# Sistema de Arquivos da Aplicação #

O sistema de arquivos do Trilado é utilizado para separação e organização do código da aplicação. Por padrão a framework utiliza o padrão MVC, que separa o código em três camadas (Model, View e Controller), no entanto é possível realizar alterações neste formato, como será apresentado a posteriori.

Por padrão, existem as seguintes divisões no sistema de arquivos da framework. 

	app/
	├──	controllers/
	├──	helpers/
	├──	locale/
	├──	models/
	├──	tmp/
	├──	vendors/
	├──	views/
	├──	wwwroot/

Cada uma destas pastas possuí um objetivo específico que será apresentado a seguir. Primeiro serão apresentadas as pastas que representam as camadas de separação do código (MVC). Em seguida serão mostradas as demais pastas e como elas são utilizadas pela framework. Por fim, será apresentado como adicionar novas pastas de separação do código ao sistema de arquivos.

## models ##

Dentro da pasta `models` é onde são colocadas classes utilizadas pela aplicação para realizar a lógica de negócios. Em geral, estes models são classes que representam tabelas do banco de dados e servem para realizar consultas e modificações nos dados. O trilado oferece uma série de métodos pré-implementados para este tipo de tarefa, além de outros recursos, que podem ser herdados da classe [Model](~/guide/model "Model"), nativa da framework.

## views ##

A pasta `views` é onde são colocados os arquivos de template para a aplicação. Estes arquivos recebem informações para apresentação dos Controllers e estruturam esta informação para apresentação.

A pasta `views` ainda apresenta algumas subdivisões, como segue:

	views
	├──	_error/
	├──	_master/
	├──	_snippet/

As pastas que iniciam com `_` são utilizadas para colocar arquivos muito utilizados da framework. A pasta `_error` armazena os arquivos que serviram como template para apresentação das páginas de erro da aplicação (por exemplo, 500 ou 404). A pasta `_master` é onde ficam os templates mais genéricos da aplicação, que são estruturas utilizadas para apresentar, em seu interior, outras views. já a pasta `_snippet` é utilizada para armazenar views de pequenas partes do layout que são muito utilizadas, como menus ou barras de compartilhamento em redes sociais.

Além das pastas da framework, é prevista a adição de novas pastas para `views`. Estas pastas servirão para dividir os códigos das Views para cada Controller. Neste caso, para cada Controller da aplicação deve ser criada uma pasta dentro da pasta `views` com o nome deste Controller e nesta pasta devem ser colocadas as Views referentes a este Controller. A classe [Controller](~/guide/controller "Controller") fornece os métodos para executar as views que seguem este formato de armazenamento.

## controllers ##

Na pasta `controllers` é onde são armazenados os arquivos que executam a lógica de negócios da aplicação. Estes arquivos recebem as requisições e chamam as Views para apresentar as informações para os clientes. Ainda existem outros métodos de apresentar informações para os clientes, sem o uso de Views. A classe [Controller](~/guide/controller "Controller") pode ser extendida pelos Controllers da aplicação para utilizar estes métodos.

## helpers ##

A pasta `helpers` armazena classes que ajudam o desenvolvedor da aplicação a realizar tarefas que ocorrem frequentemente. Como por exemplo criar tags HTML ou criar classes de Models. O trilado disponibiliza nativamente alguns [Helpers](~/guide/helpers "Helpers"), que se encontram na pasta `helpers`.

## locale ##

Na paste `locale` são colocados os arquivos de internacionalização da aplicação. Estes arquivos auxiliam no processo de tradução da interface da aplicação.

## tmp ##

A pasta `tmp` é utilizada pela framework para armazenar arquivos (HTML, imagens, etc.) em cache. Estes arquivos aumentam o desempenho da aplicação, uma vez que não é necessário que o código seja executado novamente para gerar estes arquivos.

## vendors ##

Na pasta `vendors` são armazenados aruivos de terceiros utilizados na aplicação.

## wwwroot ##

Na pasta `wwwroot` são armazenados os arquivos estáticos da aplicação. Os arquivos colocados nestas pasta ficam publiicos, neste caso utilize-a para armazenar arquivos como Javascript, CSS, imagens, etc.

## Adição de novas divisões ##

Além das divisões de arquivos nativas da framework é possível adicionar novas divisões para o código. Ao adicionar novas divisões o desenvolvedor informa a framework que existe uma nova pasta onde devem ser procurados arquivos de código fonte para a execução da aplicação.

Ao invocar uma classe qualquer a framework dispara um evento que procura e carrega a classe, caso já não tenha feito isso em um momento anteiror. Neste caso, a framework procura por classes em arquivos dentro das pastas adicionadas por padrão no arquivo `app\wwwroot\index.php`. Além das pastas adicionadas por padrão podem ser adicionadas novas pastas no arquivo `app\config.php`, como segue:

### Exemplo 1 ###

	Import::register('app/exceptions/');
	Import::register('app/managers/');

Novos pastas de código fonte podem ser adicionados por diversos motivos, como por exemplo adicionar classes de exceções específicas, ou classes de manager na aplicação. Neste caso, para adicionar uma nova pasta de códigos fonte basta escrever linhas como as apresentadas no Exemplo 1 em qualquer parte do arquivo `app\config.php`.