---
layout: post
title:  "[MEDIUM] [Part 1] BDD — Testando o comportamento do sistema"
description: “Se eu fizer isso e isso, eu espero esse resultado” ? Não seria muito legal se pudéssemos escrever nossos testes assim?
date:   2017-12-05 10:00:00 -0300
categories: portuguese programming
author: Ralph Avalon (Raphael Amoedo)
---

![You_x_Your_System]({{site.baseurl}}/images/you_x_your_system.jpeg)

*Imagem original: [https://www.ultracurioso.com.br/wp-content/uploads/2016/02/mulher-bronca-crianca-12226.jpg](https://www.ultracurioso.com.br/wp-content/uploads/2016/02/mulher-bronca-crianca-12226.jpg)*

Não seria muito legal se pudéssemos dizer para os nossos testes: *“Se eu fizer isso e isso, eu espero esse resultado”* ? Tudo bem, talvez os testes já façam isso. Mas e se eu pudesse criar um teste literalmente escrevendo:

*Dado uma condição*  
*Quando eu executo uma ação*  
*Então o resultado é esse*

Isso é possível, graças a um conceito chamado BDD — Behavior-Driven Design/Development (Design/Desenvolvimento guiado por comportamento), que em resumo é uma técnica voltada para o comportamento da aplicação e é comumente usada para testes.

Um dos maiores benefícios ao utilizar essa técnica é: pessoas não-técnicas compreendem os testes e podem **escrever testes também**.

![Exemplo de um teste escrito com BDD (Fonte: [https://ralphavalonbr.wordpress.com/2016/05/28/10018/](https://ralphavalonbr.wordpress.com/2016/05/28/10018/))]({{site.baseurl}}/images/bdd_example_01.png)*Exemplo de um teste escrito com BDD (Fonte: [https://ralphavalonbr.wordpress.com/2016/05/28/10018/](https://ralphavalonbr.wordpress.com/2016/05/28/10018/))*

BDD é um conceito independente de linguagem. Existem implementações para todas as linguagens. [Cucumber](https://cucumber.io/) é a mais conhecida e possui implementação para muitas linguagens também. [JBehave](http://jbehave.org/) (Java), [Behave](https://pythonhosted.org/behave/) (Python) e [SpecFlow](http://specflow.org/) (.NET) também são bem recomendadas.

**Mas como ele entende o que eu escrevo?**

Cada frase daquela é mapeada no código e executa alguma operação que você definir. Para o exemplo acima, seguem algumas implementações:

![Exemplo de implementação em Python usando Behave]({{site.baseurl}}/images/bdd_example_02.png)

*Exemplo de implementação em Python usando Behave*

![Exemplo de implementação em Java usando JBehave (Fonte: [https://ralphavalonbr.wordpress.com/2016/05/28/10018/](https://ralphavalonbr.wordpress.com/2016/05/28/10018/))]({{site.baseurl}}/images/bdd_example_03.png)

*Exemplo de implementação em Java usando JBehave (Fonte: [https://ralphavalonbr.wordpress.com/2016/05/28/10018/](https://ralphavalonbr.wordpress.com/2016/05/28/10018/))*

Outro benefício interessante é utilizar BDD em testes de sistema¹, especialmente para páginas Web:

![Fica bem claro de entender o que está sendo feito. (Exemplo em Python com Behave)]({{site.baseurl}}/images/bdd_example_04.png)

*Fica bem claro de entender o que está sendo feito. (Exemplo em Python com Behave)*
> ¹ — Para saber mais sobre os tipos de testes: [https://ralphavalonbr.wordpress.com/2016/04/30/10014/](https://ralphavalonbr.wordpress.com/2016/04/30/10014/)

Vale lembrar que ao permitir que outras pessoas escrevam testes, minimiza o risco dos projetos e reduz custos de manutenção, pois alguém pode escrever algum teste para algum caso antes não pensado e isso pode ser tratado cedo.

**Eu tenho que escrever os testes em inglês?**

Não. O Behave, por exemplo, tem suporte a internacionalização, então o mesmo exemplo acima pode ser criado da seguinte forma:

![Behave (Python) possui suporte para muitas linguagens, inclusive português]({{site.baseurl}}/images/bdd_example_05.png)

*Behave (Python) possui suporte para muitas linguagens, inclusive português*

**Meu sistema não é em Python e sim em Golang. Tenho que usar um framework em Golang?**

Não necessariamente. É comum quando se trata de testes unitários ou de integração utilizar a mesma linguagem, pois muitos testes desse tipo utilizam mocks de respostas de métodos, serviços ou às vezes até de banco.

Porém, quando se trata de testes de sistema, não precisa utilizar a mesma linguagem. Você pode ter o seu sistema em Golang e ter seus testes de sistema em Python.

**Mas e o TDD?**

BDD (Behavior-Driven Design) e TDD (Test-Driven Design/Development)² **não **são excludentes um do outro. Eles podem ser até complementares, como mostra a imagem a seguir:

![Fonte: [http://www.seleniumframework.com/wp-content/uploads/2014/10/BDD.jpg](http://www.seleniumframework.com/wp-content/uploads/2014/10/BDD.jpg)]({{site.baseurl}}/images/bdd_example_06.jpeg)*Fonte: [http://www.seleniumframework.com/wp-content/uploads/2014/10/BDD.jpg](http://www.seleniumframework.com/wp-content/uploads/2014/10/BDD.jpg)*
> ² — Para saber mais sobre TDD: [https://ralphavalonbr.wordpress.com/2016/02/13/10004/](https://ralphavalonbr.wordpress.com/2016/02/13/10004/)

O TDD prega o seguinte paradigma:

* **Red:** Escrevemos um Teste que inicialmente não passa

* **Green:** Fazemos o Teste passar

* **Refactor:** Refatoramos o código

Por exemplo: ao adicionar o BDD em testes de sistema, basicamente o adicionamos também ao fluxo do TDD. Mas com relação ao duelo: BDD x TDD, o que vale ser levado em consideração é:

* TDD normalmente é legível (nem sempre) e útil para desenvolvedores.

* BDD é útil e sempre legível para qualquer pessoa de qualquer área.

## Conclusão:

Esses são alguns dos benefícios de utilizar o BDD. Na continuação desse post, vamos ver na prática como utilizar o framework Behave para fazer um teste de sistema. Espero que tenham gostado e até o próximo post.

- Postado originalmente em: [https://medium.com/olxbr-tech/bdd-testando-o-comportamento-do-sistema-parte-1-6c7acbf70152](https://medium.com/olxbr-tech/bdd-testando-o-comportamento-do-sistema-parte-1-6c7acbf70152)