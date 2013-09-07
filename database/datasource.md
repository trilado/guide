# Datasource #
No Trilado, datasources são classes para manipulação de dados de uma fonte específica. Por exemplo, um datasource para manipulação de dados MySQL ou XML. Não é necessário que você implemente um datasource, o Trilado já vem com dois em seu núcleo, são eles para o banco de dados MySQL e SQL Server. 

Caso necessite trabalhar com outra fonte de dados, você pode procurar em nosso fórum para saber se alguém já implementou e disponibilizou para download o datasource específico. Mas caso você não encontre ou deseje implementar seu próprio Datasource, ele deve herdar da classe `Datasource` que é abstrata, ela contém os métodos abstratos que devem ser implementados para o funcionamento do datasource. O seu datasource deve se chamar `NomeDatasource`, onde 'Nome' é o que você definir para ele e será utilizado nas configurações de `database`.

Para saber mais sobre a classe `Datasource`, consulte nossa [API](~/api/class/Datasource).