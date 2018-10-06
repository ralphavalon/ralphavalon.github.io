---
layout: post
title:  "[MEDIUM] [Part 2] BDD — Testando o comportamento do sistema"
description: Vimos no post passado os conceitos do BDD e seus benefícios. Agora vamos para a prática e utilizar a ferramenta Behave para fazer teste de sistema.
date:   2018-02-09 10:00:00 -0300
categories: portuguese programming
author: Ralph Avalon (Raphael Amoedo)
---

![BDD_portuguese]({{site.baseurl}}/images/bdd_example_05.png)

Vimos no [post passado](https://medium.com/olxbr-tech/bdd-testando-o-comportamento-do-sistema-parte-1-6c7acbf70152) os conceitos do BDD e seus benefícios. Agora vamos para a prática: implementar um teste de sistema utilizando a ferramenta [Behave](https://github.com/behave/behave).

### Pré-Requisitos:

* [Python 2.7+ ou 3.0+](https://www.python.org/downloads/)

* [Splinter](https://splinter.readthedocs.io/en/latest/install.html)

* [Behave](http://pythonhosted.org/behave/install.html)

* Driver de um Browser¹: [Google Chrome](https://sites.google.com/a/chromium.org/chromedriver/downloads), [Mozilla Firefox](https://github.com/mozilla/geckodriver/releases) ou [Internet Explorer](http://selenium-release.storage.googleapis.com/index.html) (ainda tem gente que usa, não estou julgando)

* (Opcional) Docker — Vamos utilizar um projeto já pronto e o Docker facilita bastante para não ter que instalar pré-requisitos do projeto e rodar manualmente.

¹ — Vale a pena ressaltar que a pasta onde está o Driver necessita estar no PATH.

### Vamos começar:

Primeiramente, vamos rodar o projeto. É um projeto simples utilizado para testes, exemplos e aprendizados: [https://github.com/ralphavalon/java-sample-project/tree/system_test](https://github.com/ralphavalon/java-sample-project/tree/system_test)

**Com Docker:**

`docker run -e JAVA_OPTS='-Dspring.mvc.locale=pt_BR' -p 8081:8081 ralphavalon/javasampleproject:system_test`

**Sem Docker:**

* (Necessita Java e Maven) Executar o comando na pasta do projeto:

`mvn clean package && java -Dspring.mvc.locale=pt_BR -jar target/JavaSampleProject.jar`

Se tudo foi feito com sucesso, ao acessar [http://localhost:8081](http://localhost:8081) no navegador, o projeto deve estar acessível:

![]({{site.baseurl}}/images/bdd_example_07.png)

### Entendendo o Behave:

* Antes de utilizar o Behave, vamos rapidamente entender a estrutura que ele é utilizado. Vamos utilizar uma pasta de nome *features*, mas que pode ser qualquer outro nome. Então devemos respeitar a seguinte estrutura:

*features/*  
*features/steps/*  
*features/environment.py* — (opcional)

* A pasta *features* que definimos vai ter os arquivos de extensão *.feature*, que são os arquivos com os testes a serem executados

* A pasta *steps* é onde o behave identifica os arquivos com a interpretação dos passos para código Python

* O arquivo *environment.py* define código a ser rodado antes e depois de certos eventos relacionados aos testes.

* As informações no behave são compartilhadas através da variável *context* utilizada nos métodos do framework

### Adicionando o Behave:

Vamos adicionar o arquivo *features/user.feature* e adicionar um teste simples:

    Funcionalidade: testando apenas o título

    Cenário: deve possuir o título correto
        Dado que visito a pagina "http://localhost:8081/"
        Então deveria ter o titulo "Ralph Avalon - Java Sample Project"

Precisamos abrir o Browser antes de cada teste e fechar ao terminar. Para que isso seja feito para cada teste, vamos adicionar o arquivo *features/environment.py* com as opções [before_all](https://pythonhosted.org/behave/tutorial.html#environmental-controls) e [after_all](https://pythonhosted.org/behave/tutorial.html#environmental-controls):

    from splinter import Browser

    def before_all(context):
        context.browser = Browser('chrome')

    def after_all(context):
        context.browser.quit()

Vamos adicionar então o arquivo *features/steps/user_steps.py* :

    from behave import then, when, given

    @given('que visito a pagina "{url}"')
    def visit_page(context, url):
        context.browser.visit(url)

    @then('deveria ter o titulo "{text}"')
    def should_have_title(context, text):
        assert context.browser.title == text

Vamos executar o behave na linha de comando:

`behave --lang=pt`

![Resultado do comando behave]({{site.baseurl}}/images/bdd_example_08.png)

*Resultado do comando behave*

### Preenchendo os campos:

Até agora fizemos um teste simples. Não testa nada do fluxo principal da aplicação. Primeiro queríamos configurar e executar para saber se estava tudo ok. Agora vamos aos testes reais.

A aplicação só tem duas páginas: [criação de usuário](https://github.com/ralphavalon/java-sample-project/blob/system_test/src/main/resources/templates/home.html) e [página de sucesso](https://github.com/ralphavalon/java-sample-project/blob/system_test/src/main/resources/templates/success.html). Precisamos preencher os campos de texto, selecionar o gênero e clicar no botão. Existem várias formas de pegar o campo para preencher: CSS, id, tags, etc. Vamos utilizar o [XPath](https://pt.wikipedia.org/wiki/XPath).

Para que fique extensível a usuários não-técnicos, vamos pegar os campos através das Labels do HTML.

Temos a seguinte estrutura para *input texts*:

    <div class="form-group">
        <label>Email</label>
        <input type="text" class="form-control" name="email" placeholder="exemplo@email.com"/>
    </div>

Existem várias formas de pegar essa estrutura, porém vamos utilizar a seguinte forma:

    @when('preencho o campo "{field}" com o valor "{value}"')
    def fill_field(context, field, value):
        input_field = context.browser.find_by_xpath('//label[text()="%s"]/following-sibling::input' % field).first
        input_field.fill(value)

Agora, vamos alterar nosso arquivo user.feature :

    Funcionalidade: fluxo de criação de usuário

    Cenário: deveria criar um usuário
        Dado que visito a pagina "http://localhost:8081/"
        Então deveria ter o titulo "Ralph Avalon - Java Sample Project"

        Quando preencho o campo "Nome" com o valor "Raphael Amoedo"
        E preencho o campo "Cidade" com o valor "Rio de Janeiro"
        E preencho o campo "Email" com o valor "meuemail@email.com"
        E preencho o campo "Senha" com o valor "abc123"
        E preencho o campo "Data de Nascimento" com o valor "18/04/1992"

Ao executar, vemos que ele preenche os campos e o teste passa, porém, ainda não estamos testando algo.

![O teste preenche os campos como definimos]({{site.baseurl}}/images/bdd_example_09.png)

*O teste preenche os campos como definimos*

### Escolhendo uma das opções:

Temos um *input radio* que já vem marcado por padrão como *Masculino*, mas por garantia (e por aprendizado, caso queira selecionar outra opção), vamos clicar na opção desejada.

Temos a seguinte estrutura para *input radio*:

    <div class="radio">
     <input type="radio" name="gender" id="gender-male" value="MALE"/>
     <span>Masculino</span>
    </div>

Então, podemos adicionar o seguinte código para que possamos selecionar através do texto:

    @when('marco a opcao com o texto "{text}"')
    def mark_option(context, text):
        radio = context.browser.find_by_xpath('//input[@type="radio"]/following-sibling::span[text()="%s"]' % text).first
        radio.click()

Com isso, já podemos adicionar ao nosso test.feature o passo:

    E marco a opcao com o texto "Masculino"

### Clicando no botão e validando o resultado:

Queremos também clicar no botão e verificar se o resultado é o que esperamos, afinal, precisamos testar se a aplicação se comporta como queremos. Para isso, vamos adicionar os passos:

    @when('clico no botao com o texto "{text}"')
    def click_button(context, text):
        button = context.browser.find_by_xpath('//button/span[text()="%s"]' % text).first
        button.click()

    @then('o texto "{text}" esta presente')
    def is_text_present(context, text):
        assert context.browser.is_text_present(text)

Vamos adicionar esses passos ao nosso test.feature:

    Funcionalidade: fluxo de criação de usuário

    Cenário: deveria criar um usuário
        Dado que visito a pagina "http://localhost:8081/"
        Então deveria ter o titulo "Ralph Avalon - Java Sample Project"

        Quando preencho o campo "Nome" com o valor "Raphael Amoedo"
        E preencho o campo "Cidade" com o valor "Rio de Janeiro"
        E preencho o campo "Email" com o valor "meuemail@email.com"
        E preencho o campo "Senha" com o valor "abc123"
        E preencho o campo "Data de Nascimento" com o valor "18/04/1992"
        E marco a opcao com o texto "Masculino"
        E clico no botao com o texto "Salvar"

        Então o texto "Usuario Raphael Amoedo adicionado com sucesso" esta presente

Ao executar:

![Veremos que o usuário foi criado e o teste foi um sucesso]({{site.baseurl}}/images/bdd_example_10.png)

*Veremos que o usuário foi criado e o teste foi um sucesso*

### E se eu quiser rodar o mesmo teste com parâmetros diferentes?

Ótima pergunta. Utilizando o behave é possível utilizar o conceito de Scenario Outline (Esquema do Cenário):

![]({{site.baseurl}}/images/bdd_example_11.png)

* ***Cenário*** vira ***Esquema do Cenário***

* Criamos uma tabela de ***Exemplos*** no formato acima, sendo o nome das colunas iguais as variáveis a serem utilizadas

* Onde queremos utilizar a variável devemos colocar entre os sinais: **<>**

* No exemplo acima, o teste será rodado duas vezes, cada um com a combinação diferente, conforme definido.

### Considerações finais

É isso, pessoal, espero que tenham gostado. Fizemos apenas o caso de sucesso, mas a ideia é deixar em aberto para que possam testar os casos de erro e brincarem com a aplicação e com os testes.

**Extras:**

* Behave suporta também funcionalidades como tags, onde você anota tags nos testes e pode rodar os testes com tags específicas.

* Para utilizar Behave com testes de API REST, existem outras ferramentas como [https://github.com/stanfy/behave-rest](https://github.com/stanfy/behave-rest) ou [https://github.com/alexgarzao/victory](https://github.com/alexgarzao/victory)

* Para entender melhor sobre o Splinter, a documentação oficial ajuda muito: [http://splinter.readthedocs.io/en/latest/](http://splinter.readthedocs.io/en/latest/)

- Postado originalmente em: [https://medium.com/olxbr-tech/bdd-testando-o-comportamento-do-sistema-parte-2-5878d56502ef](https://medium.com/olxbr-tech/bdd-testando-o-comportamento-do-sistema-parte-2-5878d56502ef)