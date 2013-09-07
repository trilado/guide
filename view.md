# View #
View são as páginas que contém o HTML para visualização dos conteúdo. As views ficam dentro do diretório com o nome do controller ao qual pertecem, e, em geral, são arquivos com o nome das actions a qual pertecem (ex.: `app/views/[controller]/[action].php`), sendo que o nome do arquivo não precisa obrigatoriamente conter o mesmo nome da action, desde que no retorno esteja especificado o nome do arquivo. As variáveis passadas da action para a view podem ser usadas normalmente.

	<table>
		<thead>
			<tr>
				<th>Título<th>
				<th>Data</th>
				<th colspan="2">Ações</th>
			</tr>
		</thead>
		<tbody>
			<?php if(is_array($model->Data)): ?>
				<?php foreach($model->Data as $post): ?>
				<tr>
					<td><?= $post->Title ?></td>
					<td><?= date('d/m/Y H:i', $post->Date) ?></td>
					<td>
						<a href="~/post/edit/<?= $post->Id ?>">[editar]</a>
						<a href="~/post/delete/<?= $post->Id ?>">[deletar]</a>
					</td>
				</tr>
				<?php endforeach ?>
			<?php else: ?>
			<tr>
				<td colspan="4">Nenhum post encontrado!</td>
			</tr>
			<?php endif ?>
		</tbody>
	</table>

Baseado no .NET Framework, foi criada uma forma fácil de definir o caminho da raiz da aplicação. Dentro da view você pode utilizar `~/` para dizer que está começando da raiz.