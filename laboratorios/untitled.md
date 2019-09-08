# Lab 1 \(COOL\)

Para este laboratorio, deben hacer los ejercicios que se les pide a continuación, estos ejercicios son bastante básicos y están con el único propósito de que ustedes sepan que se puede hacer en el lenguaje COOL. Este laboratorio será la única vez en que sea necesario programar en COOL, pero no significa que tenga que olvidar como programar en COOL ya que para los proyectos es necesario que ustedes sean capaces de crear sus propios archivos de pruebas para probar sus implementaciones de cada fase.

## 1. Hola Mundo

Este ejercicio debería de ser bastante fácil, en un archivo llamado **hello.cl**, escriban un programa en COOL que imprima `Hello, world` en consola.

## 2. IO

En un archivo llamado **io.cl**, escriban un programa en COOL que pregunte al usuario su nombre, luego su edad, luego que despliegue el nombre de la persona y cuantos años tendrá al graduarse. \(Sean optimistas, no le sumen tantos años a la edad actual\).

Su programa debe de funcionar de la siguiente manera:

```bash
Ingrese su nombre: Pepe
Ingrese su edad: 19

Pepe tendrá 22 años al graduarse :)
```

## 3. Métodos

En un archivo llamado **methods.cl**, hagan un programa que le pida al usuario un número en grados Celsius y los convierta en Farenheit. Ustedes tiene que crear un método llamado `toFarenheit` que efectúe esta conversión:

```kotlin
toFarenheit(x: Int): Int {
  // su codigo aqui
};
```

Su programa debe de funcionar de la siguiente manera:

```bash
Ingrese grados Celsius: 32

32° Celsius son 89° Farenheit
```

{% hint style="info" %}
COOL no tiene punto flotante, por que su implementación no tiene que ser exacta, si por ejemplo el usuario mete el número 32° Celsius, su salida debe de ser 89° Farenheit a pesar de que la respuesta realmente debería de ser 89.6° Farenheit.
{% endhint %}

## 3. Ciclos

En un archivo llamado **loop.cl**, escriban un programa que despliegue una tabla de conversion de -50 a 150 grados Celsius hacia grados Farenheit en incrementos de 10. Para este ejercico es obligatorio que utilicen un `while`.

Su programa debe de producir el siguiente resultado:

```bash
-50 -58.0
-40 -40.0
-30 -22.0
-20 -4.0
-10 14.0
0 32.0
10 50.0
20 68.0
30 86.0
40 104.0
50 122.0
60 140.0
70 158.0
80 176.0
90 194.0
100 212.0
110 230.0
120 248.0
130 266.0
140 284.0
150 302.0
```

## 4. Calculadora

En un archivo llamado **calc.cl**, hagan un programa que reciba una string y despliegue el resultado de la operación, las operaciones válidas son:

* +
* -
* \*
* /

Su calculadora debería de aceptar operaciones como `3 + 4`, `125 - 70`, etc. Noten que el formato siempre es el mismo de acuerdo a la siguiente expresión regular: `( )*[0-9]+( )+[+-*/]( )+[0-9]+( )*`.

{% hint style="success" %}
Creen un método para buscar espacios.
{% endhint %}

También noten que las operaciones que van a ser ingresadas por el usuario siempre son binarias, y no algo como esto: `3 + 2 - 5 / 3 * 2`, así que no se compliquen, aunque si implementan algo como esto sería bastante bueno.

Su programa debe de funcionar de la siguiente manera:

```bash
>>> 2 + 2
= 4
>>> 3 * 2
= 6
>>> 6 / 2
= 3
>>> 3 - 3
= 0
...
```

## 6. Strings

En un archivo llamado **str.cl**, escriban un programa que le pida al usuario 2 Strings y verifiquen si el segundo String está contenido en el primero.

Su programa debe de funcionar de la siguiente manera:

```bash
Ingrese String 1: abcdefghij
Ingrese String 2: cdef

cdef está contenido en abcdefghij.

...
Ingrese String 1: abcdefghij
Ingrese String 2: xyz

xzy no está contenido en abcdefghij.
```

{% hint style="success" %}
En el manual de referencia de COOL hay algo que podría ayudarnos, página número 14, en específico el método: `substr(i : Int, l : Int)`.
{% endhint %}

## Referencias

1. [The Cool Reference Manual](http://web.stanford.edu/class/cs143/materials/cool-manual.pdf) - Manual de COOL.

