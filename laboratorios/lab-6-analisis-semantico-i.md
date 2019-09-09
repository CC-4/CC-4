# Lab 6 \(Análisis Semántico I\)

Es hora de empezar a poner en práctica el análisis semántico. El motivo de este laboratorio es que puedan ganar experiencia en como se hace el análisis semántico de un lenguaje simple y que posteriormente en su proyecto plasmen estas ideas. En el laboratorio anterior se enteraron de como funcionaba la tabla de símbolos, en este la vamos a utilizar juntamente con otras herramientas para anotar el árbol \(_AST_\) de un lenguaje llamado **Viper** con los tipos correspondientes.

Antes de empezar, vamos a obtener los archivos necesarios desde Github Classroom:

```bash
https://classroom.github.com/a/xtYeXoTO
```

## 1. Ciclos en Grafos:

En la fase 3 del compilador les piden verificar que el grafo de herencia de un programa hecho en **COOL** esté bien formado. Según la definición del manual de COOL un grafo de herencia está bien formado si ese grafo **NO** tiene ciclos, es decir, si hay una clase **A**, esa clase **A** no puede heredar de **A** \(de ella misma\). Tampoco se puede que una clase **A** herede de una clase **B** y esa clase **B** herede de **A**. Para poder encontrar esos ciclos necesitamos diseñar un algoritmo _**recursivo**_ \(_lo que van a hacer en esta primera parte del lab_\). En el archivo **src/Graph.java** hay una función llamada _**hasCycles**_ que tienen que completar para encontrar los ciclos en un grafo:

```java
/**
 * Checks if a class has cycles.
 *
 * @param name class name
 * @param visted visited classes set
 * @return true if the class has cycles, false if not
 */
private boolean hasCycles(String name, HashSet<String> visited) {
  // WRITE YOUR CODE HERE
  return false;
}
```

Una buena idea para almacenar el grafo de _**herencia**_ es usar un **hashtable** _\(la mayoría de cosas en este proyecto sale con hashtables...\)_, ya que podemos guardar una relación padre -&gt; hijos. Lo que hace el método de la clase `add(String parent, LinkedList<String> children)`. En este caso estamos usando `Strings` en vez de `AbstractSymbols` solo para simplificar las cosas. Entonces si uno quiere saber si una clase tiene ciclos mandaríamos a llamar al método `hasCycles("algunaclase")`. Cuando logren implementar este ejercicio, va a ser bastante fácil trasladar este código a su proyecto.

### 1.1 ¿Qué tienen que hacer?

Ustedes tienen que diseñar un algoritmo _**recursivo**_ que sea capaz de verificar si una clase tiene ciclos en su _**path**_ de herencia, pero primero algunas aclaraciones:

1. Recuerden que estamos trabajando con `Strings` , no con `AbstractSymbols`.
2. Una clase no puede heredar de ella misma o sus parents de ellos mismos.
3. NO hay circuitos cerrados de herencia, siempre hay nodos sueltos en un grafo bien formado.
4. **TIENE** que ser recursivo \(queda bastante simple así, lo prometemos\).

### 1.2 Autograder

Para probar su implementación pueden utilizar lo siguiente

```bash
./check cycles
```

Si todo lo tienen bien, les debería de salir lo siguiente:

```bash
      Autograder


+1       (test1)       
+1       (test5)       
+1       (test2)       
+1       (test4)       
+1       (test3)       


=> You got a score of 5 out of 5.
```

El autograder funciona como en los proyectos, pueden ver en la carpeta **grading** las diferencias y los tests que se están probando.

## 2. Análisis Semántico del lenguaje Viper

Para el ejercicio 2 haremos el análisis semántico de algunos nodos del lenguaje Viper, así que los introduciremos a el un poco.

### 2.1 Lenguaje Viper

**Viper** es un lenguaje bastante básico, es una mezcla de python y C, pero tiene características importantes para fines didácticos así que lo estaremos utilizando en este laboratorio y en los posteriores para terminar su análisis semántico y para realizar su **generación de código**, por eso sería bueno que se acostumbren un poco al lenguaje. Ya que estamos bastante avanzados en el curso de compiladores no es necesario que les enseñemos como programar en el lenguaje, para eso existe la gramática:

{% file src="../.gitbook/assets/viper\_language\_grammar.pdf" caption="Gramática Viper" %}

También dentro de la carpeta del lab está una subcarpeta llamada **doc** donde está en formato PDF llamada **Viper\_Language\_Grammar.pdf**. Una vez hayan visto/entendido la gramática, esto les parecera conocido:

```python
  def factorial(n: int): int {
      int result = 0;
      if (n < 2) {
          result = 1;
      } else {
          result = n * factorial(n - 1);
      }
      return result;
  }
```

### 2.2 Reglas de inferencia del lenguaje Viper

**Viper** tiene pocas reglas de inferencia a comparación de **COOL** y son menos complejas, sin embargo ayudan a entender bastante la dinámica de lo que tendrían que hacer en el proyecto, solo que sin objetos. Para ver estas reglas, pueden descargar el siguiente archivo:

{% file src="../.gitbook/assets/viper\_language\_type\_rules.pdf" caption="Reglas de Inferencia Viper" %}

También pueden encontrar este archivo en la subcarpeta **doc** de su laboratorio con el nombre **Viper\_Language\_Type\_Rules.pdf**. Lo importante es que en ese documento están las reglas en el mismo formato que el manual de **COOL**, solo que en español y que son para el lenguaje **Viper** obviamente.

### 2.3 ¿Qué tienen que hacer?

En los archivos de lab dentro de **src/viper/tree** están los nodos que representan el AST de un programa de Viper. En algunos de estos nodos ustedes tendrán que realizar el análisis semántico para completar el laboratorio. Los nodos que tienen que analizar son los siguientes:

1. **Function**
2. **BoolConst**
3. **IntConst**
4. **StrConst**
5. **Add**
6. **Sub**
7. **Mul**
8. **Div**
9. **Mod**
10. **Return**

En el lenguaje Viper existen _statements_ y _expressions_, solo las expressions son las que siempre devuelven un valor y se les asigna un tipo, los statements no. Para asignar un tipo a una expression vean la función **semant** del nodo **NoReturn** para ver como es que se le asigna un tipo a una expression utilizando la clase **Type**, además vean la clase **Type** para ver los métodos que tiene, porque les va a servir tenerlos en mente. También van a notar como está declarada la función `semant` en los nodos del AST:

```java
public void semant(SymbolTable O, HashMap<String, Function> M) {
    // WRITE YOUR CODE HERE
}
```

`O` es la tabla de símbolos que utilizaron en el laboratorio anterior, `M`es el entorno de funciones que hace un mapping de nombre de función a `Function` \(_esto es útil porque así se puede extraer fácilmente los formals y el tipo de retorno_\). Algo así tendría que verse su método `semant` en su proyecto, solo que con las cosas de COOL y tomando en cuenta los nombres de clases y que son `AbstractSymbol`. En este laboratorio no vamos a utilizar a `M`.

### 2.4 Implementación

Para cada nodo del AST hay una serie de pasos que se tienen que realizar para garantizar que el análisis semántico capture todos los errores posibles, recuerden que esta es nuestra última barrera antes de **codegen** para atrapar errores.

#### Análisis de Function

El análisis de las funciones es lo más complejo que harán de este laboratorio. Recuerden que como se pueden declarar parámetros formales y variables dentro de una función, esta crea un **scope** nuevo, utilicen lo siguiente para crear un nuevo scope:

```java
O.enterScope()
```

{% hint style="info" %}
Por lo general podemos decir que en Viper cada par de llaves `{}` crean un nuevo **scope**
{% endhint %}

Si la función se llama **main** hay un par de cosas que se tienen que considerar, una de ellas es que la función **main** no puede tener parámetros definidos y la otra es que siempre tiene que tener un tipo de retorno **int**. Cuando sea el caso que tenga parámetros definidos tienen que utilizar lo siguiente para imprimir un error:

```java
SemantErrors.mainFunctionShouldHaveNoArgs(line, col)
```

{% hint style="success" %}
Utilicen `formals.size()` para verificar esto
{% endhint %}

Y cuando tenga un tipo de retorno diferente de **int**, tienen que utilizar lo siguiente:

```java
SemantErrors.mainFunctionShouldHaveAnIntRetType(line, col)
```

Ustedes tienen que agregar los formals al **scope** que acaban de crear, pero ustedes tienen que verificar que los nombres de los parámetros no se repitan, por ejemplo esto estaría incorrecto:

```python
def foo(x: int, x: int)
```

Cuando suceda lo anterior tienen que utilizar lo siguiente:

```java
SemantErrors.formalIsAlreadyDefined(formal.line, formal.col, formal.name)
```

{% hint style="success" %}
Utilicen lo siguiente para agregar el formal al scope actual:

```java
O.add(formal.name, formal.type)
```

Noten que como valor mandamos el tipo del formal ¿Por qué?
{% endhint %}

Después deberían de mandar a llamar recursivamente a `semant` para los `statements` y la expresión de retorno del nodo `ret`. Cuando estas dos llamadas regresen si `ret` no tiene tipo **void** y la función si utilizar lo siguiente:

```java
SemantErrors.unexpectedReturnValue(ret.line, ret.col)
```

Si `ret` es **void** y la función tiene un tipo de retorno diferente de **void** utilizar lo siguiente:

```java
SemantErrors.missingReturnStatement(line, col)
```

Y en general si `ret` no es igual al tipo de retorno de la función entonces:

```java
SemantErrors.incompatibleTypes(ret.line, ret.col, ret.getType(), type)
```

Al finalizar el análisis deberían de cerrar el scope, para evitar otros errores:

```java
O.exitScope()
```

#### Constantes

Esto es bastante sencillo, si es una constante entera, el tipo de la expresión es **int**. Lo mismo pasa con las demás constantes, strings **str** y booleans **bool**.

#### Operaciones Aritméticas

Primero tienen que mandar a llamar recursivamente a `semant` de las expresiones que conforman el nodo. Las operaciones aritméticas siempre tienen que tener operandos de tipo **int** y siempre devuelven como resultado un **int**. Cuando algún operando no sea de tipo **int** tienen que utilizar el siguiente errror:

```java
SemantErrors.badOperandTypesForBinaryOp(int line, int col, String operator)
```

Siempre tienen que asumir que el tipo de una expresión aritmética es un **int**, de lo contrario nos encontrariamos con errores en cascada poco informativos, consideren lo siguiente:

```bash
true + 2 + 2 + 2
```

Si no asumieramos lo de arriba pasaría lo siguiente:

```text
bad operand types for binary operator '+'
bad operand types for binary operator '+'
bad operand types for binary operator '+'
```

A pesar que solo el primer operando de esa serie de sumas es el incorrecto.

#### Return

Cuando hagan el análisis semántico de **Return** recuerden que el tipo del return es el mismo que el de la expresión `e` del return.

{% hint style="success" %}
Implementen este nodo de primero
{% endhint %}

### 2.5 Autograder

Para probar su implementación pueden utitlizar lo siguiente:

```bash
./check viper
```

Si todo lo tienen bien, les debería de salir lo siguiente:

```bash
      Autograder


+1 (unexpectedreturn)  
+1    (diffrettype)    
+1       (arith)       
+1   (mainwithargs)    
+1       (basic)       
+1     (badarith)      
+1     (mainnoint)     
+1       (good)        
+1    (badformals)     
+1      (string)       
+1       (bool)        
+1    (missingret)     


=> You got a score of 12 out of 12.
```

