---
layout: post
title:  "[MEDIUM] Programação Funcional - Visão Geral"
description: Orientação a objetos vai acabar? Programação funcional em tudo? Vamos entender um pouco dos conceitos e tirar nossas próprias conclusões.
date:   2018-04-24 10:00:00 -0300
categories: portuguese programming
author: Ralph Avalon (Raphael Amoedo)
---

![E agora, professor?]({{site.baseurl}}/images/functional_programming_overview_01.jpeg)

Fonte: [https://www.youtube.com/watch?v=2OIPi1-3bzU](https://www.youtube.com/watch?v=2OIPi1-3bzU)

Talvez um dos assuntos mais comentados atualmente, programação funcional ganha cada vez mais popularidade. Não é uma coisa necessariamente nova, mas que vem sendo cada vez mais utilizada. Orientação a objetos vai acabar? Programação funcional em tudo? Vamos entender um pouco dos conceitos e tirar nossas próprias conclusões.

*Obs: Para os exemplos, utilizarei Javascript por ser uma linguagem de fácil compreensão e por você poder executar os comandos no Developer Console do seu navegador.*

### Mas afinal, o que é Programação Funcional?

É um paradigma de programação que se baseia em composições de funções puras (***pure functions***) — são funções que tem 3 características básicas:

* **Retorna sempre o mesmo resultado quando passados os mesmos parâmetros**

    const sum = (a,b) => a + b  
    sum(1,2); //3  
    sum(1,2); //3  
    sum(1,2); //3  

Ou, se preferir:

    var sum = function(a, b) {
        return a + b;
    }
    sum(1,2); //3
    sum(1,2); //3
    sum(1,2); //3

E aí fica a pergunta: Qual das duas funções (ou as duas) a seguir mantém essa característica de retornar o mesmo resultado?

    const customSum = (a) => a + Math.random()
    const customDate = (a) => a + Date.now()

A resposta é: **nenhuma das duas**. Além de sempre retornarem um valor diferente para cada chamada, elas também não respeitam a próxima característica básica de uma função pura:

* **Depende unicamente dos argumentos passados**

    //Função pura  
    const sum = (a,b) => a + b

    //Função não-pura  
    const myVar = 1  
    const sumImpure = (a) => a + myVar

No exemplo acima, a função sumImpure é impura porque depende de uma variável externa, que possui/pode possuir outro escopo, sendo assim um estado compartilhado (shared state), e a ideia de uma função pura é também evitar shared state, portanto, dependa apenas dos argumentos passados.

Mas… mesmo dependendo dos argumentos passados, ainda poderia existir fatores que impeçam o retorno do mesmo resultado sempre, como por exemplo, uma chamada HTTP. E por isso, a terceira e última característica de uma função pura é:

* **Não produz efeitos colaterais (side effects)**

Efeito colateral é toda interação entre uma função e o mundo externo à função. Então, alguns exemplos de efeitos colaterais são:

1. Fazer chamadas HTTP

1. Alterar qualquer tipo de variável externa

1. Alterar qualquer tipo de propriedade do objeto

1. Printar algo no console

1. Escrever em um arquivo

1. Chamar outras funções que possuam efeitos colaterais

Esses são alguns dos exemplos de efeitos colaterais. Mas, voltando para a programação funcional, a ideia é que os dados em funções puras sejam **imutáveis** — um objeto imutável é um objeto que não pode ser modificado depois de criado.

Um exemplo de imutabilidade é um objeto string no Javascript:

    var myString = "abc"
    myString.replace("a", "c") //cbc
    myString //abc

Pode reparar que executamos uma operação sobre a variável myString que gerou um outro valor, mas não alteramos o valor original da variável.

Sem imutabilidade na programação funcional, o fluxo de dados no seu programa é comprometido, pois o dado original poderia sofrer alteração em alguma função no fluxo do programa.

## Composição de função (Function composition)

É o processo de combinar duas ou mais funções para produzir uma nova função ou realizar alguma operação. Se você lembra do conceito de função composta na matemática, a expressão f(g(x)) — ou f . g (lê-se: f composta com g) — deve fazer sentido no mundo programático. Caso você não se lembre, não tem problema, vamos mostrar isso na prática aqui.

Imagine que tenhamos uma lista de números e queremos pegar os números pares e elevar ao quadrado. Uma possível implementação seria:

    const listaDeNumeros = [1,2,3,4,5,6,7,8,9]
    listaDeNumeros
       .filter((numero) => numero % 2 === 0) // [2,4,6,8]
       .map((numero) => numero * numero) // [4,16,36,64]

Ou ainda:

    const listaDeNumeros = [1,2,3,4,5,6,7,8,9];
    const isPar = (numero) => numero % 2 === 0;
    const elevaAoQuadrado = (numero) => numero * numero;

    listaDeNumeros
        .filter(isPar)
        .map(elevaAoQuadrado)

Mas o ponto a ser focado é: estamos passando uma função como parâmetro de uma outra função para executar uma operação. Javascript tem essa característica de tratar funções como variável, de poder passar funções como parâmetro, retornar funções nas funções, etc. E essa característica tem o nome de Funções de Primeira Classe (***first-class functions***). Linguagens como Haskell, Scala, Python e outras também possuem essa característica. Por que ela é importante? Porque ela permite um outro conceito da programação funcional extremamente importante:

### Funções de Ordem Superior (Higher-Order Functions)

Não se preocupe. Não são funções divinas ou algo do tipo. Uma função de ordem superior é qualquer função que: ou recebe uma função como argumento, ou retorna uma função ou as duas coisas.

*Igual aquele filter que a gente utilizou?*

Sim, exatamente igual ao filter nos exemplos acima.

### Mas e o Lambda? EU SEI QUE TEM LAMBDA EM ALGUM LUGAR.

Caso você não saiba o que é o lambda, funciona como uma função anônima — uma função sem nome. No Javascript, podemos utilizar lambda utilizando arrow functions como nos exemplos acima e como o exemplo a seguir.

    var isPar = function(numero) {
        return numero % 2 === 0;
    }

    var listaDeNumeros = [1,2,3,4,5,6,7,8,9]
    listaDeNumeros
       .filter(isPar) // Você não precisa criar a função isPar se o objetivo é usar ela unicamente nesse lugar, então, usa-se lambda para isso

    listaDeNumeros
       .filter((numero) => numero %2 === 0) //Equivalente a função isPar, porém existe nesse contexto

* *Obs: No caso do Javascript, arrow functions também servem para outras coisas, mas não é o foco do post. Para saber mais, recomendo esse link: [https://www.vinta.com.br/blog/2015/javascript-lambda-and-arrow-functions/](https://www.vinta.com.br/blog/2015/javascript-lambda-and-arrow-functions/)*

### Programação Funcional x Programação Orientada a Objetos

Antes de qualquer tipo de premonição de morte da orientação a objetos, vamos entender um pouco da diferença entre os dois. A programação funcional é declarativa ao invés de imperativa, mas o que isso quer dizer?

Um código **Imperativo** frequentemente utiliza statements — pedaços de código que realizam alguma ação, sendo alguns exemplos de statements utilizados: for, if, switch, throw, etc…

    const listaDeNumeros = [1,2,3,4,5,6,7,8,9]
    let listaPares = []

    for(let i = 0; i < listaDeNumeros.length; i++) {
        let numero = listaDeNumeros[i];
        if(numero % 2 === 0) {
            listaPares.push(numero);
        }
    }

    //listaPares agora possui [2,4,6,8]

Um código **Declarativo** depende mais de expressões — pedaços de código que calculam/executam sobre algum valor. Normalmente são algumas combinações de chamadas de função, valores e operadores que são avaliados para produzir o valor resultante.

    const listaDeNumeros = [1,2,3,4,5,6,7,8,9]
    listaDeNumeros
       .filter((numero) => numero % 2 === 0) // [2,4,6,8]

Voltando a discussão: apesar de diferentes paradigmas, não são obrigatoriamente excludentes. Em alguns casos é comum ver os dois serem utilizados, principalmente em linguagens multi-paradigmas como o próprio Javascript. Muito se prega que a principal diferença além do modelo de código é a questão dos efeitos colaterais, uma vez que na programação orientada a objetos, o resultado pode variar dependendo do estado do objeto.

![Fonte: [https://pt.stackoverflow.com/questions/13372](https://pt.stackoverflow.com/questions/13372)]({{site.baseurl}}/images/functional_programming_overview_02.png)

*Fonte: [https://pt.stackoverflow.com/questions/13372](https://pt.stackoverflow.com/questions/13372)*

### Conclusões

Uma vez que se aplica a imutabilidade, ganha-se previsibilidade, pois você garante que o valor original nunca vai ser realmente alterado e sim serão executadas operações que trabalhem em cima daquele valor que retornam um novo valor, que, graças às funções puras, sempre vão retornar o mesmo valor dados os mesmos parâmetros.

Não existe hoje um guia que diga quando utilizar um paradigma de programação e quando utilizar outro. Cada paradigma tem a sua importância e o seu caso de uso, mas é importante conhecer os benefícios de cada um e ver o(s) que melhor aplica(m) ao problema.

- Postado originalmente em: [https://medium.com/olxbr-tech/programa%C3%A7%C3%A3o-funcional-vis%C3%A3o-geral-59ebdb4be244](https://medium.com/olxbr-tech/programa%C3%A7%C3%A3o-funcional-vis%C3%A3o-geral-59ebdb4be244)