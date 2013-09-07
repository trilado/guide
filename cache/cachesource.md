# Cachesource #
No Trilado, cachesources são classes para manipulação de cache de uma fonte específica. Por exemplo, um cachesource para manipulação de dados em disco ou memória utilizando Apc. Não é necessário que você implemente um cachesource, o Trilado já vem com quatro formas de armazenamento, são elas em disco, memória RAM via APC, via memcache e memcached.

Caso necessite trabalhar com outra fonte de cache, você pode procurar em nosso fórum para saber se alguém já implementou e disponibilizou para download o Cachesource específico. Mas caso não encontre e/ou deseje implementar o seu próprio cachesource, ele deve herdar da classe `Cachesource` que é abstrata, ela contém os métodos abstratos que devem ser implementados. O seu cachesource deve se chamar `NomeCachesource`, onde 'Nome' é o que você definir para ele.

Para saber mais sobre a classe `Cachesource`, consulte nossa [API](~/api/class/Cachesource).