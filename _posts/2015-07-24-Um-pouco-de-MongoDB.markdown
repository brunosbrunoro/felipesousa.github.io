---
title: "Primeiros passos com MongoDB"
layout: post
date: 2015-07-24
tag:
- databases
- mongodb
- nosql
blog: true
star: true
---

## Summary:

MongoDB é uma aplicação de open source, de alta performance, orientado a documentos. Foi escrito em C++. Muitas aplicações podem, dessa forma, modelar informações de modo muito mais natural, pois os dados podem ser aninhados em hierarquias complexas e continuar a ser indexáveis e fáceis de buscar.

Este será um ~~guia~~ que visa apenas listar alguns comandos simples, sem muitas apresentações, apenas sobre algumas partes funcionais da ferramenta. Informações sobre a filosofia e outras coisinhas, [visite a documentação oficial.](http://docs.mongodb.org/)

* Iniciar MongoDB.

{% highlight bash %}
mongo
{% endhighlight %}
##### Todos os comandos a seguir serão executados após termos iniciado o MongoDB.


* Listar base de dados existentes no banco.

{% highlight bash %}
show dbs
{% endhighlight %}

* Criar uma base de dados.

{% highlight bash %}
use NomeDoBanco
{% endhighlight %}

* Verificar em qual base de dados estamos atualmente.

{% highlight bash %}
db
{% endhighlight %}

### Collections

Collection é como uma estrutura de dados é chamada em MongoDB.

* Criar um collection.

{% highlight bash %}
db.createCollection(name, options);
{% endhighlight %}

Na criação da collection utilizamos o comando acima com dois parâmetros, o `nome` e as opções, sendo essas configurações de tamanho(em bytes) da collection, quantos documentos são permitidos, enfim, por padrão apenas o valor do `nome` é necessária, o segundo parâmetro é opcional, [leia mais sobre collections aqui.](http://docs.mongodb.org/manual/reference/method/db.createCollection/)

*exemplo da criação de uma collection "pessoas"*:

{% highlight bash %}
db.createCollection('pessoas')
{% endhighlight %}

* Listar as collections na base de dados atuais:

{% highlight bash %}
show collections
{% endhighlight %}

### Inserir Dados

Pronto, passos simples de como realizamos a criação e listagem de collections. Vamos agora ver como adicionamos dados as essas collections.

Um ponto importante a citar é que, o mongoDB utiliza arquivos em formatos JSON's para armazenar seus dados. Sabendo disso, para adicionarmos informações em nossas collections basta escrever no formato de arquivos *.json*. Leia um pouco sobre padrões de json [aqui.](http://jsonapi.org/)

* Inserir dados em uma collection:

{% highlight bash %}
db.nomeDaCollection.insert();
{% endhighlight %}

Com o comando acima, podemos adicionar arquivos, veja um exemplo de como podemos adicionar dados em uma collection através do método .insert():

{% highlight bash %}
db.pessoas.insert({nome: "felipe", idade: 17, sexo: "masculino"});
{% endhighlight %}

Como visto o exemplo acima, usamos o padrão de escrita de arquivos json para inserir dados.

### Consulta de dados

Para consultarmos uma collection e observar os dados que existem nela de 2 formas:

{% highlight bash %}
db.nomeDaCollection.find();
{% endhighlight %}
ou

{% highlight bash %}
db.nomeDaCollection.find().pretty();
{% endhighlight %}

A diferença é simples! Na primeira opção temos como output os dados jogados sem nenhuma organização, na segunda, com o implemento do método `.pretty()` os dados são mostrados de uma forma muito mais agradável e legível. Exemplo:

{% highlight bash %}
db.pessoas.find().pretty();
{% endhighlight %}

{% highlight json %}

{
	"_id" : ObjectId("55b190caf8ab876af97e521b"),
	"nome" : "felipe",
	"idade" : 17,
	"sexo" : "Masculino"
}

{% endhighlight %}

### Update de Dados

No mongoDB, o método `update()` serve como método de atualização de algum dado, como também de criação daquele campo caso não exista o campo.

{% highlight bash %}
db.nomeDaCollection.update(query, modificador, callback);
{% endhighlight %}

O método `update()` recebe três parâmetros, sendo eles `query`, que vai ser **ONDE** nós vamos alterar os dados, `modificador`, que vai ser **PELO QUE** aquele dado vai ser alterado, e um callback. Vejamos um exemplo:

{% highlight bash %}
db.pessoas.update({name: "felipe"}, { $set:{idade: 20} });
{% endhighlight %}

Nesse exemplo, estamos dizendo que estamos alterando o valor do campo idade onde o `name` do dado for "felipe".

*Observe que no 2º parametro utilizamos o `$set` para descrevermos que apenas aquela chave de **campo: valor** vai ser alterada quando executarmos o método, caso o `$set` não seja incluído, todos os campos de todos os dados vão ser substituidos.*

### Remover Dados

Para removermos dados de uma collection utilizamos o comando:

{% highlight bash %}
db.nomeDaCollection.remove();
{% endhighlight %}

Como parâmetro do método `.remove()` passsamos o dado que queremos alterar. Veja o exemplo:

{% highlight bash %}
db.pessoas.remove({name: "felipe"});
{% endhighlight %}

Com isso, acabo de remover todos os dados do usuário que possui o `name` como "felipe";

*Para removermos todos os dados da collection basta passar como parâmetro `{}` no método `.remove()`.*

### Deletar Collections e Base de dados

Para deletar um collection usamos o comando:

{% highlight bash %}
db.nomeDaCollection.drop();
{% endhighlight %}

*lembrando que o mongo não pede confirmação para deletar os dados, então avalie corretamente se a collection selecionada é a que você quer apagar.*

Para deletar uma base de dados, usamos o comando:

{% highlight bash %}
db.dropDatabase();
{% endhighlight %}

Com isso temos o básico em MongoDB. Existem muito mais coisas a se aprender sobre essa ferramenta fantástica. [Leia mais na documentação oficial](http://docs.mongodb.org/).
