# TEMA 1

## Semántica de un programa

### ⚖️ Tabla Comparativa: Semántica Estática vs. Semántica Dinámica

| Característica | Semántica Estática (Compilación) | Semántica Dinámica (Ejecución) |
| :--- | :--- | :--- |
| **¿Cuándo actúa?** | **ANTES** de ejecutar el programa (tiempo de compilación). | **DURANTE** la ejecución del programa (tiempo de ejecución). |
| **¿Qué comprueba / describe?** | Reglas de tipos, declaración previa de variables, visibilidad, ámbitos y concordancia de parámetros. | El comportamiento real del programa, los cambios en la memoria ($\sigma$ o $s$) y la evolución de las instrucciones. |
| **Fase del compilador** | Fase de análisis semántico (tabla de símbolos, árbol sintáctico). | Intérpretes, máquinas virtuales, motor de ejecución. |
| **Utilidad principal** | Detectar errores de tipo o de declaración antes de lanzar el programa. | Construir intérpretes, depurar, verificar asertos y demostrar corrección formal. |


## Paradigma de Programación
Un paradigma de programación es una forma o estilo de pensar y estructurar cómo se escribe el código para resolver un problema

### 1. Paradigma Imperativo
- "`COMO`" se debe hacer el cálculo paso a paso.

- Da ***órdenes secuenciales*** a la máquina, ***cambiando*** el estado de la memoria y las variables *paso a paso* (muy ligado a la arquitectura tradicional de *Von Neumann*).

- Una llamada  ejecución no contiene variables

- ej. C, Pascal, Java (parte estructurada).

### 2. Paradigma Declarativo
- "`QUÉ`" se quiere lograr, no en cómo calcularlo.

- ***describes el problema*** o el ***resultado final deseado***, y dejas que un motor interno de la máquina (como un **evaluador** o un **sistema de inferencia**) *busque la manera de resolverlo*.

- ej. SQL (bbdd), Prolog (lógico), HTML.

### 3. Paradigma Orientado a Objetos (POO)
- "`Modelar el problema`" usando objetos que combinan datos (atributos) y comportamientos (métodos).

- Pilares clave: Herencia, Polimorfismo, Encapsulamiento, Abstracción.

- ej. Java, C++, Python

### 4. Paradigma Funcional
- "`Evaluación`" de funciones matemáticas puras.

- Una llamada  ejecución no contiene variables

- Evita el estado mutable y los efectos secundarios; los datos son inmutables y las funciones se pueden pasar como argumentos o resultados.

- ej. Haskell, Lisp, Scala

### 5. Paradigma Concurrente / Paralelo
- "`Ejecución de múltiples tareas o procesos`" de forma simultánea o solapada.

- reto principal: evitar problemas como la corrupción de datos, condiciones de carrera o los interbloqueos (deadlocks).

---

## Tipos de Errores en Compilación

### 1. Error Léxico (El error de "carácter o letra")
- Fallas en los símbolos individuales (palabras mal escritas o caracteres raros).

- Ejemplo en código: Meter un símbolo ilegal en medio de un número o instrucción que el lenguaje no reconoce:

```cs
int x = 5$0; // El símbolo '$' no pertenece a los tokens válidos de Java.
```

### 2. Error Sintáctico (El error de "gramática y puntuación")
- Fallas en la estructura y puntuación (olvido de `;`, llaves `{}` mal cerradas, orden incorrecto).

- Ejemplo en código: Olvidar un punto y coma ; o dejar una llave sin cerrar:

```cs
int x = 5   // ¡Error! Falta el punto y coma final. El compilador no sabe dónde acaba la orden.
```

### 3. Error Semántico (El error de "sentido común y significado")

- Estructura perfecta, pero el significado o los tipos no encajan (incompatibilidad de tipos, usar variables no declaradas).

- Ejemplo en código: Intentar guardar una montaña dentro de una caja de cerillas. Está bien escrito pero rompe las reglas de los tipos:

```cs
int b = new A(); // ¡Error! Estás intentando meter un objeto entero complejo dentro de una variable numérica 'int'.
```

---

## Semántica Operacional (Small-Step vs. Big-Step)

La semántica operacional describe cómo se ejecuta un programa definiendo reglas matemáticas sobre cómo evoluciona su estado y sus instrucciones.

### 1. Small-Step (Paso Pequeño: $\rightarrow$)

> En Small-Step ($\rightarrow$): Devuelve una configuración $\langle \text{sentencia}, \text{estado} \rangle$. Por eso en small-step verás siempre cosas como $\langle \text{skip}, \{X \mapsto 0\} \rangle$. 

- Desglosa la ejecución en pasos individuales.

- Cada transición ($\rightarrow$) transforma una configuración inicial $\langle \text{sentencia}, \text{estado} \rangle$ en una nueva configuración paso a paso hasta llegar a un estado final (como ***skip***)

#### Reglas clave:
***Asignación ($x := e$)***:
<br>
Evalúa primero la expresión *e* en el estado actual *s* hasta obtener un valor *v*, y luego actualiza la memoria.

$$\langle x := e, s \rangle \rightarrow \langle \text{skip}, s[x \mapsto v] \rangle$$

<br>

***Secuencia ($c_1; c_2$)***:
<br>
Si el primer comando es *skip*, desaparece y continúa el segundo. Si no, se ejecuta un paso de $c_1$.

- Si $c_1$ es *skip*: $\langle \text{skip}; c_2, s \rangle \rightarrow \langle c_2, s \rangle$

- Si $c_1$ no es skip:  $\frac{\langle c_1, s \rangle \rightarrow \langle c_1', s' \rangle}{\langle c_1; c_2, s \rangle \rightarrow \langle c_1'; c_2, s' \rangle}$

<br>

***Bucle `while`***:
- *si la condición es verdadera* (true): bucle se desdobla en su cuerpo seguido de otro while, manteniendo la memoria intacta en este primer paso.

$$\langle \text{while } b \text{ do } c, s \rangle \rightarrow \langle c;\ \text{while } b \text{ do } c, s \rangle \quad \text{si } \langle b, s \rangle \Rightarrow \mathbf{true}$$

- *Si la condición es falsa* (false): El bucle se convierte directamente en *skip*

$$\langle \text{while } b \text{ do } c, s \rangle \rightarrow \langle \text{skip}, s \rangle \quad \text{si } \langle b, s \rangle \Rightarrow \mathbf{false}$$

<br>

***Condicional `if-then-else`***:

- **Si la condición es verdadera** ($\mathbf{true}$): Selecciona la rama then ($c_1$), manteniendo la memoria intacta en este paso.

$$\langle \text{if } b \text{ then } c_1 \text{ else } c_2, s \rangle \rightarrow \langle c_1, s \rangle \quad \text{si } \langle b, s \rangle \Rightarrow \mathbf{true}$$

- **Si la condición es falsa** ($\mathbf{false}$): Selecciona la rama else ($c_2$), manteniendo la memoria intacta en este paso.

$$\langle \text{if } b \text{ then } c_1 \text{ else } c_2, s \rangle \rightarrow \langle c_2, s \rangle \quad \text{si } \langle b, s \rangle \Rightarrow \mathbf{false}$$

<br>

### Big-Step (Paso Grande: $\Downarrow$)

> En Big-Step ($\Downarrow$): Devuelve ÚNICAMENTE el estado final ($\sigma'$ o $s'$), ¡SIN la instrucción/sentencia! 

Calcula el ***resultado final de golpe***. Relaciona una sentencia y un estado inicial directamente con el estado final resultante ($\langle c, s \rangle \Downarrow s'$), omitiendo los pasos intermedios.

#### Reglas clave:
***Asignación ($x := e$)***:
<br>
Evalúa la expresión *e* a un valor *v* y devuelve directamente el estado actualizado

$$\frac{\langle e, s \rangle \Downarrow v}{\langle x := e, s \rangle \Downarrow s[x \mapsto v]}$$

<br>

***Secuencia ($c_1; c_2$)***:
<br>
Ejecuta $c_1$ llevando al estado $s'$, y a partir de ese estado ejecuta $c_2$ hasta el estado final $s''$.

$$\frac{\langle c_1, s \rangle \Downarrow s', \quad \langle c_2, s' \rangle \Downarrow s''}{\langle c_1; c_2, s \rangle \Downarrow s''}$$

***Bucle `while`***:
- Caso Base (Condición falsa): Si la condición evalúa a falso, el estado no cambia.

$$\frac{\langle b, s \rangle \Downarrow \mathbf{false}}{\langle \text{while } b \text{ do } c, s \rangle \Downarrow s}$$

- Caso Recursivo (Condición verdadera): Si es verdadero, ejecuta el cuerpo c (llegando a un estado intemedio s') y vuelve a evaluar el `while` desde ese nuevo estado de forma recursiva hasta que la condición sea falsa.
<br>


$$\frac{\langle b, s \rangle \Downarrow \mathbf{true}, \quad \langle c, s \rangle \Downarrow s', \quad \langle \text{while } b \text{ do } c, s' \rangle \Downarrow s''}{\langle \text{while } b \text{ do } c, s \rangle \Downarrow s''}$$

<br>

***Condicional `if-then-else`***:

- Caso Rama then (**Condición verdadera**): Si la condición es verdadera, ejecuta la rama $c_1$ hasta llegar al estado final $s'$.

$$\frac{\langle b, s \rangle \Downarrow \mathbf{true}, \quad \langle c_1, s \rangle \Downarrow s'}{\langle \text{if } b \text{ then } c_1 \text{ else } c_2, s \rangle \Downarrow s'}$$

- Caso Rama else (**Condición falsa**): Si la condición es falsa, ejecuta la rama $c_2$ hasta llegar al estado final $s'$.

$$\frac{\langle b, s \rangle \Downarrow \mathbf{false}, \quad \langle c_2, s \rangle \Downarrow s'}{\langle \text{if } b \text{ then } c_1 \text{ else } c_2, s \rangle \Downarrow s'}$$

<br>

---

### PMD (Precondición más débil)

4 reglas de transformación:

***Asignación ($x := e$)***:
<br>
Sustitiuyes en la postcondición $Q$ todas las apariciones de la variable $x$ por la expresión $e$.

$$\text{pmd}(x := e, Q) \equiv Q[x \mapsto e]$$

<br>

***Secuencia de instrucciones ($c_1; c_2$):***
<br>
Se resuelve por partes yendo de atrás hacia adelante.
<br>
Primero calculas la $\text{pmd}$ del último comando ($c_2$) con la postcondición final, y el resultado de eso lo usas como la nueva postcondición para calcular la $\text{pmd}$ del primer comando ($c_1$).

$$\text{pmd}(c_1; c_2, Q) \equiv \text{pmd}(c_1, \text{pmd}(c_2, Q))$$

<br>

***Condicional (`if-then-else`)***:
<br>
Combina la condición del if con las $\text{pmd}$ de ambas ramas mediante un operador lógico "y/o".

$$\text{pmd}(\text{if } b \text{ then } S_1 \text{ else } S_2,\ Q) \equiv (b \land \text{pmd}(S_1, Q)) \lor (\neg b \land \text{pmd}(S_2, Q))$$

## 🛡️ Lógica de Hoare y Precondición Más Débil ($\text{pmd}$)

Una **Terna de Hoare** se escribe como $\{P\}\ S\ \{Q\}$:
* **$P$ (Precondición):** Condición que debe cumplirse ANTES de ejecutar el programa $S$.
* **$S$ (Programa/Instrucciones):** El código que se va a ejecutar.
* **$Q$ (Postcondición):** Condición que debe ser verdadera DESPUÉS de ejecutar $S$.

La **Precondición Más Débil ($\text{pmd}(S, Q)$)** es la condición exacta y mínima necesaria antes de $S$ para garantizar que se alcance $Q$. Para resolver cualquier ejercicio, se calcula **de atrás hacia adelante**:

1. **Asignación ($x := e$):** Sustituyes $x$ por la expresión $e$ en $Q$.
   $$\text{pmd}(x := e, Q) \equiv Q[x \mapsto e]$$

2. **Secuencia ($c_1; c_2$):** Calculas de derecha a izquierda.
   $$\text{pmd}(c_1; c_2, Q) \equiv \text{pmd}(c_1, \text{pmd}(c_2, Q))$$

3. **Condicional ($\text{if } b \text{ then } S_1 \text{ else } S_2$):**
   $$\text{pmd}(\text{if } b \text{ then } S_1 \text{ else } S_2, Q) \equiv (b \land \text{pmd}(S_1, Q)) \lor (\neg b \land \text{pmd}(S_2, Q))$$