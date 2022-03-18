# Using PMD

Pick a Java project from Github (see the [instructions](../sujet.md) for suggestions). Run PMD on its source code using any ruleset. Describe below an issue found by PMD that you think should be solved (true positive) and include below the changes you would add to the source code. Describe below an issue found by PMD that is not worth solving (false negative). Explain why you would not solve this issue.

## Answer

Exécutons le PMD sur [ce repo](https://github.com/apache/commons-collections).

### True positive

```
/home/jessy/M2/VV/commons-collections/src/test/java/org/apache/commons/collections4/map/LRUMapTest.java:434:	SimplifyBooleanReturns:	Avoid unnecessary if..then..else statements when returning booleans
```

La suggestion ci-dessus fait référence au code suivant

```java
@Override
protected boolean removeLRU(final LinkEntry<K, V> entry) {
	if ("a".equals(entry.getValue())) {
		return false;
	}
	return true;
}
```

En effet, la méthode pourrait être simplifiée ainsi

```java
@Override
protected boolean removeLRU(final LinkEntry<K, V> entry) {
    return !"a".equals(entry.getValue()
}
```

### False Negative

```
/home/jessy/M2/VV/commons-collections/src/main/java/org/apache/commons/collections4/properties/PropertiesFactory.java:105:	UselessParentheses:	Useless parentheses.
```

Cette suggestion indique qu'il y a des parenthèses inutiles et fait référence au code suivant.

```java
@Override
public synchronized boolean equals(final Object o) {
	return (o instanceof Properties) && ((Properties) o).isEmpty();
}
```

Il est vrai que pour la machine, les parenthèses autour de *o instanceof Properties* ne sont pas utiles. Cependant, elle simplifie la lecture du code d'un point de vue humain. Par conséquent, il n'est pas nécessaire de retirer les parenthèses.
