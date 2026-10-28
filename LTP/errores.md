# APUNTES DE ERRORES MIOS

## Tipificación

- **Estática**: el tipo de cada variable se conoce y se comprueba en compilación. Una variable int x seguirá siendo entera siempre (Java, C, Hashkell).

- **Dinámica**: el tipo lo tienen los valores, no las variables, y se comprueba al ejecutar.
Puedes hacer `x = 5` y después `x = "hola"` (Python, JavaScript)

---

## Genericidad

Un método genérico NO puede estar en una clase normal, como `static <T> int largo(T[] a)`

---

protected es el único que hereda de paquetes.

`private`: solo la clase.
<br>

`default`: la clase y su paquete.
<br>

`protected`: la clase, su paquete y las subclases de otros paquetes.
<br>

`public`: todos.

---

## INTERBLOQUEO
Un interbloqueo es cuando dos hilos se esperan mutuamente y se quedan bloqueados para siempre

## CONDICIÓN DE CARRERA
ambos hilos leen el mismo valor, suman y pisan el resultado del otro
<br>

se produce corrupción de datos

## ORDEN

éxico → sintáctico → semántico → código intermedio → optimización → generación de código → enlazado (así lo muestra el esquema de las diapositivas).

## ENLAZADO
La generación produce el código objeto de tu programa. 
<br>

El enlazado lo une con otro código objeto y librerías para obtener el ejecutable.

```cs
“combina con otras compilaciones” = enlazado.
```

---

## JAVA ES UNA IMPLEMENTACIÓN MIXTA
típico ejemplo de lenguaje compilado puro, va directo a código máquina. Java compila a bytecode, y la JVM lo interpreta
<br>

Mixtas: Java, Pascal (P-code) y Prolog (WAM).

---

La BNF describe la sintaxis (qué cadenas son programas legales), no el significado.
