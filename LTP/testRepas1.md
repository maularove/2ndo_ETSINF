# TEST REPASO TEMA 1

### ¿A qué tipo de polimorfismo corresponde la siguiente definición?

> Hace referencia a funciones u operadores que pueden aplicarse a argumentos de tipos diferentes y que se comportan de forma diferente dependiendo del tipo de los argumentos a los que se aplican.

- A. Herencia.
- **B. Sobrecarga. ✅**
- C. Genericidad.
- D. Abstracción.

 ---

### El polimorfismo paramétrico se conoce también como:

- A. Coerción.
- **B. Genericidad. ✅**
- C. Herencia.
- D. Sobrecarga.

 ---

### Un ejemplo de lenguaje no tipificado es:

> Un lenguaje tipificado (o tipado) es aquel que distingue entre diferentes tipos de datos (enteros, texto, booleanos, etc.) y aplica reglas sobre cómo se pueden usar y combinar

> Un lenguaje no tipificado (o no tipado), en cambio, no distingue tipos de datos a nivel de lenguaje o maneja todos los datos como una única estructura genérica (por ejemplo, simples cadenas de caracteres, términos o secuencias de bytes).

- A. Haskell.
- **B. Prolog. ✅**
- C. Java.
- D. C.

 ---

### Dada la clase genérica `A`, definida como `class A<T> { ... }`, ¿cuál de las siguientes declaraciones define una clase genérica `B` descendiente de `A`?

- A. `class B<T> implements A<T> { ... }`
- **B. `class B<T> extends A<T> { ... }` ✅**
- C. `class B<T extends A> { ... }`
- D. `class B extends A<Integer> { ... }`

**Respuesta:** B. `extends` indica que `B` hereda de `A` y conserva el parámetro genérico `T`.

 ---

### ¿Cuándo una clase debe ser obligatoriamente abstracta?

- **A. Cuando algunos de sus métodos son abstractos. ✅**
- B. Cuando desciende de una clase abstracta.
- C. Cuando sus atributos son abstractos.
- D. Cuando redefine alguno de los métodos heredados.

**Respuesta:** A. Una clase que declara uno o más métodos abstractos debe declararse también como `abstract`.

 ---

### Indica cuál es el resultado producido por el siguiente código en Java:

```java
class Animal {
          public void move() {
                    System.out.println("Animals can move");
          }
}

class Dog extends Animal {
          public void move() {
                    System.out.println("Dogs can walk and run");
          }
}

public class Test {
          public static void main(String[] args) {
                    Animal a = new Animal();
                    Animal b = new Dog();
                    a.move();
                    b.move();
          }
}
```

- A.
     ```text
     Animals can move
     Animals can move
     ```
- B.
     ```text
     Dogs can walk and run
     Dogs can walk and run
     ```
- **C.**
     ```text
     Animals can move
     Dogs can walk and run
     ```
- D. Ninguna de las anteriores, ya que `Animal b = new Dog();` da un error.

**Respuesta: C.** `b` tiene como tipo de referencia `Animal`, pero apunta a un objeto `Dog`. Por polimorfismo, se ejecuta la implementación sobrescrita de `Dog.move()`.

 ---

### ¿Cuál de las siguientes afirmaciones es FALSA?

- A. Java permite definir tanto clases como métodos genéricos.
- **B. Las clases genéricas en Java deben ser necesariamente abstractas. ✅**
- C. En las clases genéricas de Java es posible restringir las clases a las que se puede instanciar un parámetro genérico.
- D. En Java, una clase genérica puede tener varios parámetros genéricos.

**Respuesta: B.** Las clases genéricas no tienen que ser abstractas; pueden instanciarse siempre que no sean abstractas por otros motivos.


 ---

### La idea propuesta por Kowalski «Programa = Lógica + Control» significa que:

- A. Es incorrecta; lo que propuso fue «Programa = Datos + Algoritmos».
- B. Es otra forma de designar las ternas de Hoare de la semántica axiomática.
- C. Especificar el control es lo más importante al escribir un programa declarativo.
- **D. En los programas declarativos, el programador puede centrarse en describir la lógica del problema. ✅**

**Respuesta: D.** En la programación declarativa, el programador describe la lógica del problema y el lenguaje o sistema de ejecución se encarga, en gran medida, del control.

---

### Indica cuál de las siguientes afirmaciones es CIERTA

- **A. La concurrencia introdujo problemas como los interbloqueos o la inanición. ✅**
- B. El objetivo de la programación concurrente es la aceleración de algoritmos gracias al uso de varios procesadores.
- C. Todos los lenguajes concurrentes pertenecen al paradigma imperativo.
- D. No es posible la concurrencia en Java.

**Respuesta: A.** La ejecución concurrente puede provocar problemas de sincronización, como los interbloqueos (*deadlocks*) y la inanición (*starvation*).

 ---

### En un lenguaje de programación declarativo, ¿cuál de las siguientes afirmaciones es CIERTA?

- **A. Un programa se puede ver como una especificación ejecutable. ✅**
- B. Un programa es una secuencia de instrucciones de control para la máquina que lo ejecuta.
- C. Un elemento fundamental es el bucle `while`.
- D. Mediante la instrucción de asignación podemos provocar los denominados efectos laterales.

**Respuesta: A.** En la programación declarativa, el programa describe qué resultado se desea obtener, por lo que puede interpretarse como una especificación ejecutable.

