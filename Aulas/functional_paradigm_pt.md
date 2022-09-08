# O Paradigma Funcional

<!-- 
Neste capítulo, apresentamos as principais propriedades da programação funcional. 
Na programação funcional, a computação procede reescrevendo funções e não modificando o estado. 
A característica fundamental das linguagens nesse paradigma, pelo menos em sua forma “pura”, 
é justamente a de não possuir o conceito de memória (e, portanto, efeitos colaterais). 
Uma vez que um ambiente é definido, uma expressão sempre denota o mesmo valor.
Discutiremos o paradigma puro nas primeiras seções, explicando os aspectos fundamentais. 
As linguagens de programação funcionais, no entanto, mesclam esses ingredientes “puros” em um contexto que adiciona 
outros mecanismos.

Abordaremos a máquina SECD, uma máquina abstrata para linguagens funcionais de ordem superior (higher-order)
que constitui o protótipo de muitas implementações reais. 
Estaremos, neste ponto, em condições de discutir as razões pelas quais o paradigma de programação funcional 
é interessante em relação às linguagens imperativas comuns. 

O capítulo termina com uma seção mais teórica que fornece uma introdução sucinta ao λ-calculus, 
um sistema formal de computabilidade que inspira todas as linguagens funcionais e que tem sido, 
desde a época de ALGOL e LISP, um modelo constante para o projeto de linguagens de   programação.
--> 

## Computações sem Estado

As linguagens convencionais baseiam seu modelo computacional no conceito de mudança de estado.
O coração deste modelo é o conceito de variável modificável, ou seja, 
um "container" com nome associado ao qual podem ser atribuídos valores diferentes, enquanto tal associação nome-"container" é mantida no ambiente.

Analogamente, a principal construção em linguagens convencionais é 
o comando de atribuição, que modifica o valor (_r-value_)
guardado em uma variável, mas não modifica a associação entre o nome da variável e sua localização ou endereço (_l-value_).

```
l-value = r-value
```

As linguagens de programação convencionais diferem no nível de abstração, tipos e construções que permitem a manipulação de variáveis, 
mas todas compartilham o mesmo modelo computacional, uma 
visão abstrata da máquina subjacente (hardware convencional), em que
a computação prossegue modificando os valores armazenados: 
a Máquina de von Neumann, nomeada em homenagem ao matemático húngaro-americano que, na década de 1940, materializou a Máquina de Turing no projetode um protótipo físico, dando origem ao computador moderno.

Este não é, no entanto, o único modelo possível sobre o qual basear 
uma linguagem de programação. Há alternativas à computação via modificação de variáveis, ou seja, sem referência a Estado.
Por exemplo, a computação é realizada via reescrita de expressões,
isto é, com mudanças que ocorrem apenas no ambiente e
não envolvem o conceito de memória.
Se não houver variáveis modificáveis, 
não há mais necessidade de atribuição,
o comando principal em linguagens convencionais.
A computação torna-se a modificação sofisticada do ambiente 
em que a possibilidade de manipulação de funções (de ordem superior) 
desempenha um papel fundamental.
Sem o comando de atribuição, 
a iteração como mecanismo de controle
(em que o estado é modificado repetidamente até que os valores de certas variáveis satisfaçam uma condição)
também perde importância: 
Construções iterativas e recursivas são dois mecanismos que permitem
computações infinitamente longas.
No modelo computacional _sem estado_, a iteração desaparece,
a recursão permanece como uma construção de controle de sequência fundamental.
Funções de ordem superior e recursão são os ingredientes básicos desse modelo computacional _sem estado_. 
As linguagens de programação que têm este modelo como base
são chamadas de linguagens funcionais e o paradigma 
relacionado é o _paradigma de programação funcional_.

Este é um paradigma tão antigo quanto o imperativo.
Desde a década de 1930, ao lado da Máquina de Turing, existe 
o λ-cálculo, um modelo abstrato para caracterizar funções computáveis.

LISP foi a primeira linguagem de programação explicitamente inspirada no
λ-cálculo e outras surgiram nos anos seguintes
(Scheme, ML, Miranda, Haskell, para citar algumas).
Linguagens como Miranda e Haskell são consideradas 
"puramente funcionais" dado que não possuem componentes imperativos.

### Expressões

## 11.2 Avaliação


+ Evaluation by value: In evaluation by value (which is also called applicative-order evaluation or eager evaluation, or innermost evaluation), 
a redex is evaluated only if the expression which constitutes 
its argument part is already a value.
More precisely, leftmost evaluation in applicative order 
works as follows.

1. Scan the expression to be evaluated from the left, choosing the first application encountered. Let it be
(f_exp a_exp).

2. First evaluate (recursively applying this method)
f_exp until it has been reduced
to a value (of functional type) of the form
(fn x => ...).

3. Then evaluate the argument part, a_exp, of the application, 
so that it is reduced to a value, val.

4. Finally, reduce the redex ((fn x => ...)val)
and goto to (1).

+ Evaluation by name: In the evaluation by name strategy 
(which is also called normal order or outermost),
a redex is evaluated before its argument part.

+ Lazy Evaluation: To maintain the advantages of evaluation by name, the
lazy strategy proceeds like that by name but the first time 
that a “copy” of a redex is encountered, 
its value is saved and will be used should any other copies 
of the same redex be encountered.
The by-name and lazy strategies are examples of the
call by need strategies in which a redex is reduced 
only if it is required in a computation.

## 3 Programação Funcional

### 3.1 Local Environment

The mechanism of global definitions in the environment that 
we have used this far has too little structure for a modern language. 
As in conventional languages, it is appropriate 
to provide explicit mechanisms to introduce definitions with limited
scope, as for example:

``` 
let x = exp in exp1 end
``` 

This introduces the binding of x to the value of exp in a scope 
which includes only exp1.
The presence of functional expressions already introduces nested
scopes and associated environments which are 
composed of the formal parameters of the function bound to the 
actual parameters. From the point of view of evaluation,
we can indeed consider it as syntactic sugar for:

``` 
(fn x => exp1) exp
```


### 3.2 Interactiveness

Every functional language has an interactive environment. 
The language isused by entering expressions which the abstract machine evaluate and whose value it returns. 
Definitions are particular expressions which modify the global environment (and may return a value).

This model immediately suggests interpreter based implementations, 
even if there are efficient implementations that use compilation to generate compiled code the first time a definition is stored 
in the environment.

### 3.3 Values

Primitive types and functions.

+ types
+ pattern matching
+ infinite objects
+ aspectos imperativos

## 11.4 Máquinas Abstratas

## 11.5 Avaliação

## 11.6 Lambda-calculus

