# TCC *vs* LCC

Explain under which circumstances *Tight Class Cohesion* (TCC) and *Loose Class Cohesion* (LCC) metrics produce the same value for a given Java class. Build an example of such as class and include the code below or find one example in an open-source project from Github and include the link to the class below. Could LCC be lower than TCC for any given class? Explain.

## Answer

LCC et TCC sont des moyens de mesurer la cohésion d'une classe. Une classe est fortement cohésive si les méthodes qui la composent sont reliées entre-elles. C'est-à-dire, que toutes les méthodes travaillent sur le même ensemble de variables. Dans une bonne architecture, chaque classe effectue une seule fonction, or, une classe faiblement cohésive indique qu'elle réalise plusieurs fonctions et qu'elle devrait par conséquent être divisée en plusieurs classes. 

LCC et TCC mesurent cette cohésion sous forme d'une valeur comprise entre 0 et 1. Plus LCC et TCC sont elevés, plus la classe est cohésive. TCC <= LCC, TCC est égal à TCC quand une classe est optimalement cohésive. C'est-à-dire, si toutes les méthodes d'une classe sont reliées entre-elles, ainsi TCC et LCC seront égaux à 1.

Plus précisément, LCC et TCC se calculent de la manière suivante 

```
NP = maximum number of possible connections

= N * (N − 1) / 2 where N is the number of methods

NDC = number of direct connections (number of edges in the connection graph)

NID = number of indirect connections

Tight class cohesion TCC = NDC / NP

Loose class cohesion LCC = (NDC + NID) / NP
```

TCC compare le nombre de connexions directes par rapport au nombre de connexions possibles alors que LCC additionne le nombre de connexions directes avec le nombre de connexions indirectes et le compare au nombre de connexions possibles, il est donc impossible pour LCC d'être strictement supérieur à TCC.

### Exemple d'une classe optimalement cohésive (TCC = LCC = 1)

```java
class Operation {
    private double value1;
    private double value2;

    public double addition() {
        return value1+value2;
    }

    public double substract() {
        return value1-value2;
    }
    
    public double multiply() {
        return value1*value2;
    }
}
```

## 
