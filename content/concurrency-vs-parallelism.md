# Concorrência vs. Paralelismo

Quando o assunto é assíncronia, ou seja, tratar as coisas sem uma sequência de etapas pré-definida, temos dois modelos:

## Concorrência

Na concorrência as etapas são alternadas de forma frequente, pensando no nosso exemplo do garçom, é como se 1 garçom atendesse mais de uma mesa durante seu trabalho e alternasse sua atenção entre elas.

Caso queira ver na prática com o PHP, temos esse código a seguir:

**Input**

```
<?php

function routina(): Generator
{
    for ($i = 0; $i < 3; $i++)
    {
        echo "Corrotina:$i\n";
        yield;
    }
}

$generator = routina();
$generator->rewind();

for ($i = 0; $i < 3; $i++)
{
    echo "Principal:$i\n";
    $generator->next();
}
  
```

**Output**

```
Corrotina:0
Principal:0
Corrotina:1
Principal:1
Corrotina:2
Principal:2
```


**Obs**: Caso queira entender mais como funciona a questão de corrotina dentro do PHP, aconselho a estudar sobre [*Generator syntax*](https://www.php.net/manual/pt_BR/language.generators.syntax.php)

## Paralelismo

No paralelismo as etapas acontecem de verdade juntas, em linhas de tempo paralelas, no nosso exemplo do restaurante seria como se houvessem no mínimo, dois garçons.
