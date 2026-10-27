# Modelo Primer Examen Parcial LTP

### ejercicio 1.
***Indica cuál de las siguientes afirmaciones es*** FALSA

A. ✅ En los lenguajes con tipificación estática, el tipo de los valores asignados a las variables no cambia durante la ejecución de los programas.

B. ✅ En los lenguajes con tipificación dinámica, el tipo de los valores asignados a las variables puede cambiar durante la ejecución de los programas.

C. ❌ En Java, el código `float x = 2` asigna a la variable el valor entero 2 y no el valor real 2.0.

> cuando asignas entero a float, el lenguaje aplica una coerción (conversión impícita de tipos) y lo guarda con decimales

D. ✅ El sistema de tipos de un lenguaje de programación establece la relación entre el tipo de variable y el de los valores que se le pueden asignar

---

### ejercicio 2.
***Observa el siguiente fragmento de código:***

```cs
public class Polymorphim {
    public static int add(int[] inAR) {
        
        float total;
        for (int i = 0; i < inAr.length; i++) {
            total = total + inAr[i];
        }
        return ((int)total);
    }
    
    public static int add(char[] inAr) {
        return 0;
    }

    public static void main(String[] args) {
        int[] intArray = {1, 2, 3, 4, 5};
        char[] charArray = {'a', 'b', 'c'};
        add(intArray);
        add(charArray);
    }
}  // end of class Polymorphim
```

***Indica que tipo de poliformismo podemos ver:***

Coerción explícita, coerción implícita y sobrecarga.

- `Sobrecarga`: dos métodos mismo nombre

- `Coerción implícita`: variable **float total = 0;** suma en el bucle, donde el lenguaje convierte implícitamente los valores básicos para hacerlos compatibles.

- `Coerción explícita`: en la sentencia de retorno del primer método (**return ((int)total);**) se fuerza conversión a tipo int.

---

### ejercicio 3.
***Indica cuál de las siguientes afirmaciones sobre la genericidad es*** FALSA

A. ✅ En Java, podemos definir tanto clases como métodos genéricos

> ej. clases genéricas: class Entry<K, V>

> ej. métodos genéricos individuales: <T> int lengthA(T[] array)

B. ✅ Un tipo genérico se expresa usando al menos una variable tipo

C. ❌ En Java una clase genérica solo puede tener una variable de tipo (solo puede tener un parámetro)

> Una clase genérica ***SÍ*** que puede tener múltiples parámetros o variables de tipo simultáneamente (ej. estructuras de diccionarios o pares como Entry<K, V>)

D. ✅ La genericidad permite definir una función o estructura que es común a un número potencialmente infinito de tipos

> Definición conceptual: ***Genericitat*** (polimorfismo paramétrico o universal)

> diseñar componentes de código reutilizables cuya estructura es común y válida para un número potencialmente infinito de tipos distintos

---

### ejercicio 4. 
***Considera el siguiente código Java:***

```cs
package P1;
class A {protected int x;}
class B extends A {...}
class C {...}
```

```cs
package P2;
class D extends A {...}
class E {...}
```

***Teniendo en cuenta la visibilidad en el lenguaje Java, indica desde qué clases se puede ver el atributo x:***

Se puede ver en A, B, C y D.

- `Clase A`: donde se declara x

- `Clase B`: pertenece al mismo paquete (`P1`) y es una subclase de A

- `Clase C`: aunque no hereda de A, se encuentra en el mismo paquete. Los miembros ***protected son visibles desde cualquier clase que comparta paquete***.

- `Clase D`: paquete diferente (`P2`) pero es subclase de A

Otras variantes:
- `private`: solo en su clase

- `default` (nada) en su clase y en su mismo paquete

- `protected`: en su clase y su paquete y subclases

- `public`: en todas partes

---

### ejercicio 5. 
Considera el siguiente código Java:

```cs
// reflexión
import java.lang.reflect.*;

class A {
    private int a, b;

    public A (int a, int b) {
        this.a = a; this.b = b;
    }
    private int suma() {
        return a+b;
    }
    protected int getA() {
        return a;
    }
    public int getB() {
        return b;
    }
}

public class I {
    public static String m0() {
        String s = "";
        A obj = new A(2,3);
        Method[] ns =
            obj.getClass().getDeclaredMethods();
        for (Method m : ns) 
            s += m.getName() + ", ";
        return s;        
    }
}
```

***Indica cuál es el contenido del String que devuelve el método m0 al ejecutarse:***

Devuelve los nombres de los métodos suma, getA y getB

```cs
obj.getClass().getDeclaredMethods();
```
- `obj.getClass()`: obtine info de la clase del objeto creado (*A*)

- `.getDeclaredMethods()`: devuelve todos los métodos declarados explícitamente en esa clase, sin importar su modificador de acceso (incluye public, protected, default y private).

- `m.getName()`: consulta los nombres de cada método gracias al bucle 

---

### ejercicio 7.
***Dado el siguiente programa Java en el que se utiliza el*** alcance estático:

```cs
class AlcanceEstatico {
    
    static int x = 0;
    
    void inc() {
        int x = 0;
        x = x + 1;
        dec();
    }

    void dec() {
        x = x - 1;
    }

    void main() {
        inc();
        dec();
        System.out.print(x);
    }
}
```

> ***¿Qué es alcance estático (o léxico)?***
<br>

> Un método accede a su variable local de primeras, si no la encuentra, sube al ámbito léxico estático en el que fue definido.

<br>


> Ocultación de variables (Shadowing)
<br>

> Si existe una variable local y global con el mismo nombre, en la clase la local tiene prioridad, y por tanto si se modifica será solo en local.

El valor que se escribirá en pantalla después de la ejecución main es:
<br>

*-2*

---

### ejercicio 8.
***Indica cuál de las siguientes afirmaciones es*** CIERTA

A. ✅ Un lenguaje declarativo tiene un nivel de abstracción mayor que un lenguaje Imperativo.

> Al no ir paso a paso ni fijarse en el "como" como el imperativo, tendrá mayor abstracción

B. ❌ Los lenguajes imperativos delegan mayor cantidad de control a la máquina que los declarativos.

> Los lenguajes declarativos al ser el "qué" en vez del "como" como el imperativo, necesitan mayor cantidad de control. 

C. ❌ El modelo del paradigma declarativo es una máquina de estado.

> el modelo basado en una máquina de estados (y en la arquitectura tradicional de Von Neumann) corresponde al ***paradigma imperativo***

D. ❌ Los programas imperativos son la especificación de un problema

> ***son los programas declarativos*** los que actúan como una especificación del problema

---

### ejercicio 9.
***Indica cuál es la siguiente afirmación*** CORRECTA:

- ✅ El paradigma imperativo está vinculado a la arquitectura tradicional (Von Neumann).

---

### ejercicio 10.
***Indica cuál de las siguientes afirmaciones es*** FALSA:

A. ✅ La programación concurrente tiene asociados algunos problemas como son la corrupción de datos y los interbloqueos, entre otros.

B. ✅ Dada la finalidad de la programación paralela, no se concibe sin varios procesadores.

C. ✅ Un ejemplo de modelo de programación interactiva son los sistemas empotrados.

> ***sistemas empotrados*** (como microcontroladores en electrodomésticos o automóviles): 

> interactuan constantemente con el entorno externo exterior y los usuarios mediante entradas y salidas continuas.

D. ❌ Los programas imperativos son más sencillos de analizar que los programas declarativos

---

### ejercicio 11.
***¿Qué tipo de error se produce al compilarlo?***

```cs
class A {
}

class B extends A {
    public int b = new A();
}
```

Se produce un error semántico.

---

### ejercicio 12.

Considera la siguiente breve sintaxis, en notación BNF, para las expresiones aritméticas válidas en un cierto lenguaje:

---

### ejercicio 13.
***Indica qué etapa de un compilador detectaría un error en tiempo de ejecución (por ejemplo, que se ha realizado una división por cero al haber leído el cero de una base de datos):***

Ninguna de las etapas de análisis lo detectaría

---

### ejercicio 14.
Dada la siguiente transición (incompleta) empleando la semántica operacional de paso pequeño (small-step):

```cs
//  instrucciones es while x > 0 do x:= x-1
// memoria principal x=2
(while X > 0 do X := X - 1, {X → 2}) →

// cuerpo bucle (c): X:=X-1
// como x > 0, x = 2, es true    
    (X > 0, {X → 2}) => True
        (X, {X → 2}) => 2
        (0, {X → 2}) => 0
#        
```

***¿Qué configuración debe aparecer en la posición #?***

```cs
(X:= X - 1; while X > 0 do X := X - 1, {X → 2})
```

La regla del while en paso pequeño (small-step)

$$\frac{\langle b, s \rangle \Rightarrow \mathbf{true}}{\langle \text{while } b \text{ do } c,\ s \rangle \rightarrow \langle c;\ \text{while } b \text{ do } c,\ s \rangle}$$

---

### ejercicio 15.

***Dada las siguientes reglas que definen la de paso pequeño (small-step) de una instrucción some***:

Si miramos las tres reglas que te han dado en el enunciado:

1. $\langle \text{some}(b, \text{skip}), \sigma \rangle \rightarrow \langle \text{skip}, \sigma \rangle$ (No aplica porque nuestro comando c no es un `skip`)

2. La regla con el condicional `false` (no aplica porque la condición ha dado `true`).

3. La tercera regla (la que tiene $\langle b, \sigma \rangle \Downarrow \text{true}$ arriba):

$$\frac{\langle b, \sigma \rangle \Rightarrow \text{true}}{\langle \text{some}(b, c), \sigma \rangle \rightarrow \langle \text{skip}, \sigma \rangle}$$

<br>

Esta regla nos dice: Si la condición b evaluada en la memoria $\sigma$ da como resultado ***true***, entonces el comando `some(b,c)` se transforma en `skip`, manteniendo exactamente la misma memoria $\sigma$.

Resultado final:

$$\langle \text{skip},\ \{x \mapsto 4, y \mapsto 3\} \rangle$$

---

### ejercicio 16.
***indica cuál es la pmd(S,Q), la precondición más débil del siguiente programa S, teniendo en cuenta la postcondición Q indica:***

```cs
S       (if x > 7 then z:= x + 3 else x := 0)
Q       (x = 0)
```

$$\text{pmd}(\text{if } b \text{ then } S_1 \text{ else } S_2,\ Q) \equiv (b \land \text{pmd}(S_1, Q)) \lor (\neg b \land \text{pmd}(S_2, Q))$$

el resultado es:

$x \le 7 \land z = 3$.

---

### ejercicio 17.
***Considera la terna de Hoare:***

```cs
{P} x := y; x := x - 2; z := x {x>0}
```

Basta con ver que { x > 0 }, para que x cumpla la condición, y debe ser mayor a 2.

- Postcondición inicial ($Q$): $x > 0$
- Programa completo ($S$): $x := y;\ x := x - 2;\ z := x$ 

---

### ejercicio 18.

***¿Qué problemas puede introducir el uso de la reflexión?***
<br>

Problemas de seguridad y rendimiento

---

### ejercicio 19.
___Indica cuál de las siguientes afirmaciones sobre los lenguajes de programación___ CIERTA:

A. ❌ Los lenguajes de script no pueden ser orientados a objetos

> lenguajes de script modernos son multiparadigma.

> ej. Python o JavaScript

B. ❌ Todos los lenguajes declarativos son perezosos

> existen muchos otros lenguajes declarativos o funcionales que utilizan una evaluación estricta o ansiosa (como Scheme o Erlang).

C. ❌ Ningún lenguaje es concurrente y declarativo simultáneamente

> ***Sí*** que existen los llamados lenguajes declarativos concurrentes (así como extensiones lógicas y funcionales diseñadas específicamente para la concurrencia).

D. ✅ En programación imperativa y programación funcional una llamada  ejecución no contiene variables.

> Al evaluar o realizar una llamada en los modelos formales de ejecución (semántica operacional), las expresiones o llamadas que se evalúan en un estado concreto resuelven sus variables a valores concretos del entorno o memoria, sin dejar variables libres sin ligar en la invocación final de ejecución.

---

### ejercicio 20.

***En la compilación de un programa, la optimización del código intermedio se realiza durante la fase de***:

Síntesis (Generación código)

---

### ejercicio 21.

¿En qué momento del proceso de compilación se detectará el error?
```cs
public class Main {
    public static int foo(int n, int m) {
        return n + m;
    }
    
    public static void main(String[] args) {
        int x = 20;
        foo(x, y); // <-- ¡Aquí está el error!
    }
} 
```

En el análisis semántico.

---

### ejercicio 21.

La semántica dinámica de un programa:

A. ❌ Se obtiene a partir del texto del programa durante la fase de análisis semántico.

> Eso corresponde a la semántica estática (comprobación de tipos y declaraciones en compilación).

B. ❌ Se refiere a los posibles cambios en el texto del programa

> La semántica no cambia el código fuente del programa.

C. ❌ Es un concepto inexistente

> Es un concepto fundamental en teoría de lenguajes de programación.

D. ✅ Permite razonar acerca de la ejecución del mismo. Según la descripción semántica utilizada es posible desarrollar un intérprete, verificar propiedades del programa formuladas mediantes asertos, etc.

---

### ejercicio 22. 
(el 17 de la cap tres.jpg)

---

### ejercicio 23.

¿Qué significa un post-incremento ($y := x++$)?

- Significa que primero se asigna el valor actual de $x$ a la variable $y$ ($y := x$).

- Y justo después, la variable $x$ se incrementa en uno ($x := x + 1$). 

la respuesta es:

$$\langle y := x;\ x := x + 1, s \rangle \Downarrow s'$$

---

### ejercicio 24.

Dada la siguiente ejecución con la semántica operacional de paso grande (big-step), cuál es el valor de (*):

$$\langle \text{while } X > 0 \text{ do } X := X - 1,\ \{X \mapsto 2\} \rangle \Downarrow (*)$$

- En Small-Step ($\rightarrow$): Devuelve una configuración $\langle \text{sentencia}, \text{estado} \rangle$. Por eso en small-step verás siempre cosas como $\langle \text{skip}, \{X \mapsto 0\} \rangle$.   

- En Big-Step ($\Downarrow$): Devuelve ÚNICAMENTE el estado final ($\sigma'$ o $s'$), ¡SIN la instrucción/sentencia!

la respuesta es:
<br>

($\{X \mapsto 0\}$)

---

### ejercicio 25.
Considera la terna de Hoare:

- Programa $S$: (if x > 0 then z := 1 else z := x); x := z

- Postcondición $Q$: $x > 0 \land z = 5$

***¿Cuál de las siguientes precondiciones P hace qu ela terna sea correcta?***

- *false*

---

