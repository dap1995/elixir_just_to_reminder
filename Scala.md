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

#### Private[this]

Is the most restrictive access scope.
It's defines that the method is available to the current instance of the current object.

Example below doesn't compile:
```
class Foo {
    private[this] def isFoo = true
    def doFoo(other: Foo) {
        if (other.isFoo) {  // this line won't compile
            // ...
        }
    }
}
```

because the other instance don't permit the access on others instances.

#### Implicit parameters

The final parameters list on a method can be marked implicit to make a implicit value of the context able to be passed implicitly to this method

```
class Prefixer(val prefix: String)
def addPrefix(s: String)(implicit p: Prefixer) = p.prefix + s

implicit val myImplicitPrefixer = new Prefixer("***")
addPrefix("abc")  // returns "***abc"
```

Other example can be goot to understand better:
The controller Action do this ->
  ```apply(block: (Request[AnyContent]) ⇒ Result): Action[AnyContent]```

And we makes it like this ->
  ```
  def newTask = Action { implicit request =>
  taskForm.bindFromRequest.fold(
        errors => BadRequest(views.html.index(Task.all(), errors)),
        label => {
          Task.create(label)
          Redirect(routes.Application.tasks())
        } 
    )
  }
  ```

The implicit request in this case is because bindFromRequest needs the request like implicit

But you can pass a implicit request or not.

### Implicit conversions

Implicit conversions allows to make conversions of a object without needs to explicit the conversion.
Below follows a comparative example of implicit conversion to make better understanding.

```
scala> implicit def doubleToInt(d: Double) = d.toInt
scala> val x: Int = 42.0
x: Int = 42
```

```
scala> def doubleToInt(d: Double) = d.toInt
scala> val x: Int = 42.0
<console>:11: error: type mismatch;
 found   : Double(42.0)
 required: Int
       val x: Int = 42.0
```

#### References

https://stackoverflow.com/questions/10375633/understanding-implicit-in-scala/10375941#10375941
http://alvinalexander.com/scala/how-to-control-scala-method-scope-object-private-package
