# Form #
A classe `Form` foi criada para auxiliar o programador no desenvolvimento de formulários. Ela contém métodos para criação de alguns campos de textos.

## input() ##
Retorna o HTML para geração de um campo de texto. Esse método recebe três parâmetros, sendo o primeiro o valor do atributo `name` e `id`. O segundo é o valor que preencherá o campo, ou seja, o valor do atributo `value`, pode ser nulo. O terceiro é um `array` que, também pode ser nulo, recebe como chave o nome do atributo e como valor o valor do atributo.

	<form method="POST" action="">
		<div>
			<label for="Name">Nome</label>
			<?= Form::input('Name') ?>
		</div>
		<div>
			<label for="Email">E-mail</label>
			<?= Form::input('Email', $model->Email) ?>
		</div>
		<div>
			<label for="Login">Login</label>
			<?= Form::input('Login', $model->Login, array('class' => 'example')) ?>
		</div>
		<div>
			<input type="submit" value="Registrar" />
		</div>
	</form>

No exemplo acima utilizamos as três formas de parâmetros.

## textarea() ##
Retorna o HTML para geração de uma área de texto. Esse método recebe três parâmetros, sendo o primeiro o valor do atributo `name` e `id`. O segundo é o valor que preencherá a área de texto, pode ser nulo. O terceiro é um `array` que, também pode ser nulo, recebe como chave o nome do atributo e como valor o valor do atributo.

	<form method="POST" action="">
		<div>
			<label for="Title">Título</label>
			<?= Form::input('Title', $model->Title) ?>
		</div>
		<div>
			<label for="Content">Conteúdo</label>
			<?= Form::textarea('Content', $model->Content) ?>
		</div>
		<div>
			<input type="submit" value="Salvar" />
		</div>
	</form>

## hidden() ##
Retorna o HTML para geração de um campo de texto oculto. Esse método recebe três parâmetros, sendo o primeiro o valor do atributo `name` e `id`. O segundo é o valor que preencherá o campo, ou seja, o valor do atributo `value`, pode ser nulo. O terceiro é um `array` que, também pode ser nulo, recebe como chave o nome do atributo e como valor o valor do atributo.

	<form method="POST" action="">
		<div>
			<label for="Name">Nome</label>
			<?= Form::input('Name') ?>
		</div>
		<?= Form::hidden('Id', $model->Id) ?>
		<div>
			<input type="submit" value="Salvar" />
		</div>
	</form>

## password() ##
Retorna o HTML para geração de um campo de senha. Esse método recebe três parâmetros, sendo o primeiro o valor do atributo `name` e `id`. O segundo é o valor que preencherá o campo, ou seja, o valor do atributo `value`, pode ser nulo. O terceiro é um `array` que, também pode ser nulo, recebe como chave o nome do atributo e como valor o valor do atributo.

	<form method="POST" action="">
		<div>
			<label for="Name">Nome</label>
			<?= Form::input('Name') ?>
		</div>
		<div>
			<label for="Email">E-mail</label>
			<?= Form::input('Email', $model->Email) ?>
		</div>
		<div>
			<label for="Password">Senha</label>
			<?= Form::password('Password') ?>
		</div>
		<div>
			<label for="ConfirmPassword">Confirmar Senha</label>
			<?= Form::password('ConfirmPassword') ?>
		</div>
		<div>
			<input type="submit" value="Registrar" />
		</div>
	</form>

## submit() ##
Retorna o HTML para geração de um botão de submissão de formulário. Esse método recebe três parâmetros, sendo o primeiro o valor do atributo `name` e `id`. O segundo é o texto do botão, ou seja, o valor do atributo `value`, pode ser nulo. O terceiro é um `array` que, também pode ser nulo, recebe como chave o nome do atributo e como valor o valor do atributo.

	<form method="POST" action="">
		<div>
			<label for="Title">Título</label>
			<?= Form::input('Title', $model->Title) ?>
		</div>
		<div>
			<label for="Content">Conteúdo</label>
			<?= Form::textarea('Content', $model->Content) ?>
		</div>
		<div>
			<?= Form::submit('save', 'Salvar') ?>
		</div>
	</form>

## select() ##
Retorna o HTML para geração de um combobox. Esse método recebe quatro parâmetros, sendo o primeiro o valor do atributo `name` e `id`. O segundo é um `array` contendo as opções, onde a chave do `array` é o valor da opção e o valor do array é o texto da opção. O terceiro o valor que virá selecionado, pode ser nulo. O por último um `array` que, também pode ser nulo, recebe como chave o nome do atributo e como valor o valor do atributo.

	<form method="POST" action="">
		<div>
			<label for="Name">Nome</label>
			<?= Form::input('Name') ?>
		</div>
		<div>
			<label for="Email">E-mail</label>
			<?= Form::input('Email', $model->Email) ?>
		</div>
		<div>
			<label for="Gender">Sexo</label>
			<?= Form::select('Gender', array('Feminino','Masculino'), $model->Gender) ?>
		</div>
		<div>
			<input type="submit" value="Registrar" />
		</div>
	</form>

## radio() ##
Retorna o HTML para geração de um conjunto de botões *radio*. Esse método recebe quatro parâmetros, sendo o primeiro o valor do atributo `name` e `id`. O segundo é um `array` contendo as opções, onde a chave do `array` é o valor da opção e o valor do array é o texto da opção. O terceiro o valor que virá selecionado, pode ser nulo. O por último um `array` que, também pode ser nulo, recebe como chave o nome do atributo e como valor o valor do atributo.

	<form method="POST" action="">
		<div>
			<label for="Name">Nome</label>
			<?= Form::input('Name') ?>
		</div>
		<div>
			<label for="Email">E-mail</label>
			<?= Form::input('Email', $model->Email) ?>
		</div>
		<div>
			<label for="Gender">Sexo</label>
			<?= Form::radio('Gender', array('Feminino','Masculino'), $model->Gender) ?>
		</div>
		<div>
			<input type="submit" value="Registrar" />
		</div>
	</form>
