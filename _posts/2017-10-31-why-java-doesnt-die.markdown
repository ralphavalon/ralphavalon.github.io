---
layout: post
title:  "[MEDIUM] Por que o Java não morre?"
description: Basta uma nova linguagem surgir que logo começam as projeções. Rumo aos 30 anos da linguagem, parece que Java se tornou a linguagem que todos amam odiar. Por que o Java não morre então?
date:   2017-10-31 10:00:00 -0300
categories: portuguese programming
author: Ralph Avalon (Raphael Amoedo)
---

![World_x_Java]({{site.baseurl}}/images/world_x_java.jpeg)
Fonte da imagem original: http://bit.ly/2lM5BhH

*“Kotlin vai matar o Java.” “Scala vai matar o Java.” “Groovy vai matar o Java.” *Basta uma nova linguagem surgir que logo começam as projeções. Rumo aos 30 anos da linguagem (atualmente possui 22), parece que Java se tornou a linguagem que todos amam odiar.

É comum ver alguns olhares estranhos ao dizer: “É em Java.”, muito provavelmente seguido das frases: “*Java é velho*”, “*Java é lento*” ou “*Usa {insira alguma linguagem aqui}*”. Apesar de tudo isso e de inúmeros posts dizendo que a linguagem vai morrer, ainda é [a linguagem mais utilizada no mundo](https://www.tiobe.com/tiobe-index/). Por que isso?

Algumas pessoas diriam: ***JVM***. Bem, não. A JVM é incrível mas as linguagens que “vão matar o Java” também utilizam a JVM. Outras poderiam dizer: ***Portabilidade***. Bem, também não. Hoje em dia, a linguagem mais simples criada já tem essa funcionalidade que fez o Java crescer tanto em seu início. Mas antes de entrar nas razões reais, é preciso desmitificar algumas coisas:

***Java é lento.*** — Java **ERA **lento. Ganhou essa fama principalmente pelo antigo J2EE que precisava implementar milhares de coisas para fazer uma coisa simples. Hoje em dia, não é muito difícil encontrar benchmarks mostrando que Java se equipara e até supera em performance a [C++](http://blog.optionscity.com/java-vs.-c-performance-face-off-part-ii), [Go](https://benchmarksgame.alioth.debian.org/u64q/go.html), [Python](https://benchmarksgame.alioth.debian.org/u64q/compare.php?lang=java&lang2=python3) e outras linguagens.

![Comparação de um algoritmo Java vs Python — Fonte: [http://bit.ly/2xAntxg](http://bit.ly/2xAntxg)]({{site.baseurl}}/images/java_x_python.png)*Comparação de um algoritmo Java vs Python — Fonte: [http://bit.ly/2xAntxg](http://bit.ly/2xAntxg)*

***Java é verboso.*** — Ok, se escrevia muito usando Java, mas depois de frameworks como [Spring Boot](https://projects.spring.io/spring-boot/) e [Lombok](http://jnb.ociweb.com/jnb/jnbJan2010.html) e próprias evoluções da linguagem, isso também não se aplica.

Tendo isso em mente, vamos aos reais motivos pelo qual o Java não morre:

* **Compatibilidade** — É tranquilo atualizar o Java da versão 4 (por exemplo) para o 8 sem que isso quebre o seu código. Na verdade, só por atualizar a versão do Java e da JVM, essa JVM está mais otimizada e seu código rodará ainda mais rápido.

* **Comunidade** — Sim, a comunidade é um fator importante na continuidade de uma linguagem. A comunidade literalmente direciona o crescimento da linguagem com as [JSRs (Java Specification Requests)](https://pt.wikipedia.org/w/index.php?title=JSR&redirect=yes) e com a [JCP (Java Community Process)](https://pt.wikipedia.org/wiki/Java_Community_Process). Quando se fala de Java, se fala de inúmeros frameworks para qualquer coisa que se possa imaginar. E isso sem contar a comunidade Spring e todo o seu ecossistema.

* **Multiplataforma** — Não, não me refiro a Windows/Linux/Mac. Java serve para aplicações, Web ou não, mas também serve para TVs (Java TV), cartões (Java Card), IoT (Java ME, Java Embedded), etc.

* **Multiparadigma** — Apesar de ser uma linguagem orientada a objetos, é uma linguagem que está sempre se reinventando. Programação Funcional? [Java tem suporte](https://dzone.com/articles/functional-programming-java-8). Programação Reativa? [Java tem suporte](https://dzone.com/articles/rxjava-part-1-a-quick-introduction). Desenvolvimento Modularizado? [Java tem suporte](http://blog.caelum.com.br/java-9-na-pratica-jigsaw/).

## EXTRA:

* **Cultura**— Esse pode ser só uma impressão minha e minha opinião, por isso coloquei no Extra, mas a comunidade Java tem uma cultura muito maior de boas práticas que outras linguagens, o que impacta diretamente na manutenção do código. Cultura de testes, SOLID, Clean Code, Design Patterns e outros são muito comuns de se ver dentro da comunidade Java.

## Conclusão:

Querem matar o Java de qualquer maneira, mas não vai ser tão fácil. Com uma comunidade grande que direciona o crescimento da linguagem, Java tem se reinventado e resistido a cada linguagem que surge. Então, fica no ar a pergunta: O que vai matar o Java se o Java não morre?

- Postado originalmente em: [https://medium.com/olxbr-tech/por-que-o-java-n%C3%A3o-morre-15c15736102](https://medium.com/olxbr-tech/por-que-o-java-n%C3%A3o-morre-15c15736102)