# Scala

#### val or var
**val** is to set a immutable object
**var** is to set a mutable object

Example:

```scala
val = new String()
```

#### lazy val
lazy val = { println("y"); 13 }

#### Traits

Traits are used like Interfaces in java
It's much used to define what the class/object must be (Which methods or attributes the object needs implement).

```
trait Similarity {
  def isSimilar(x: Any): Boolean
  def isNotSimilar(x: Any): Boolean = !isSimilar(x)
}
```

#### Object

Used to create a singleton object of a class that is defined implicitly

```
object TESTE {
  def apply(){
  }
}
```

In the example above follows the creation of a single instance of TESTE class.
Can you create a object whether there isn't a class? yes, but you can use also with a class.

```
scala> classOf[TESTE2]
<console>:12: error: not found: type TESTE2
       classOf[TESTE2]
               ^

scala> case class TESTE2();
defined class TESTE2

scala> classOf[TESTE2]
res8: Class[TESTE2] = class TESTE2
```

#### Case classes

Immutable by default;
Decomposable through pattern matching;
Compared by structural equality instead of by reference;
Succint to instatiate and operate on;

The constructor parameters are public and can be accessed directly.

```
scala> case class Brother(name: String);
defined class Brother

scala> val brother = Brother("Luiz");
brother: Brother = Brother(Luiz)

scala> brother.name;
res0: String = Luiz

```
#### Protected

protected allows a method in a class to be accessed by own class or subclass that extends it.

#### implicit
