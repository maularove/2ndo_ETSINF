# Programación en C 

crear/editar archivo kate
```css
kate nombre_archivo.c &
```

copiar / duplicar un archivo
```js
cp origen.c destino.c
```

compila código fuente 
```js
 gcc nombre_archivo.c -o nombre_archivo
```
(-wall opcional)
```css
gcc -Wall nombre_archivo.c -o nombre_ejecutable
```

informe detallado
```css
gcc -v -o numbers numbers.c
```

ejecutar programa
```css
./nombre_ejecutable
```

consultar manual de una funcion
```css
man 3 nombre_funcion
```

histórico
```js
// Lista los archivos y carpetas de la carpeta actual.
ls

// formato de lista detallada (permisos, propietario, tamaño, fecha de última modificación, etc.).
-l (long) 

// Muestra todos los archivos, incluidos los archivos ocultos (los que empiezan por un punto, como .git o .bashrc)
-a (all)

ls -la
```

scanner en c ejemplo (numbers2.c):
```js
#include <stdio.h>

int Number;

// importante usar ´int´  en main
int main()
{
    int i;

    // Preguntamos al usuario cuántos números quiere visualizar y lo leemos
    printf("Write the number to be displayed: ");
    scanf("%d", &Number);

    printf("The first %d natural numbers are:\n", Number);
    for (i=0; i<Number; i++)
    {
        printf("  %d \n", i);
    }

    printf("BYE\n");
    return(0);
}
```

---

## Opciones y Banderas del compilador GCC
Sintaxis general:
gcc [opciones] [archivos_fuente] -o [ejecutable]


| Opción / Bandera | Descripción | Ejemplo de Uso |
| :--- | :--- | :--- |
| `-o archivo` | Indica el nombre del archivo de salida (el ejecutable resultante). | `gcc numbers.c -o numbers` |
| `-Wall` | Muestra todos los avisos (*warnings*) importantes de compilación. Muy recomendado. | `gcc -Wall numbers.c -o numbers` |
| `-v` | Modo detallado (*Verbose*). Muestra los comandos ejecutados en cada etapa de compilación y la versión del compilador. | `gcc -v -o numbers numbers.c` |
| `-E` | Realiza solamente la etapa de preprocesamiento, enviando el resultado a la salida estándar. | `gcc -E numbers.c > numbers.pp` |
| `-S` | Realiza el preprocesamiento y la compilación, obteniendo el archivo en código ensamblador (`.s`). | `gcc -S numbers.c` |
| `-c` | Realiza las etapas hasta el ensamblado, obteniendo el archivo en código objeto binario (`.o`). | `gcc -c numbers.c` |
| `-I[ruta]` | Especifica la ruta del directorio de los archivos de cabecera a incluir (`#include`). *(Sin espacio entre la `I` y la ruta)* | `gcc -I/usr/include programa.c` |
| `-L[ruta]` | Especifica la ruta del directorio de los archivos de biblioteca con código objeto. *(Sin espacio)* | `gcc -L/usr/lib programa.c` |
| `-l[NOMBRE]` | Indica al enlazador qué biblioteca o librerías adicionales debe incluir (por ejemplo, `-lm` para la librería matemática). | `gcc programa.c -o programa -lm` |

## Especificadores de Formato (`printf` y `scanf`)

| Especificador | Tipo de Argumento / Dato | Descripción |
| :--- | :--- | :--- |
| `%c` | `char` / `int` | Escribe o lee un carácter simple. |
| `%d`, `%i` | `int` | Escribe o lee un número entero con signo en base decimal. |
| `%f` | `double` / `float` | Escribe o lee un número en punto flotante sin exponente (formato `mmm.ddd`). |
| `%e`, `%E` | `double` | Escribe un número flotante con exponente en notación científica (indicado con `e` o `E`). |
| `%g`, `%G` | `double` | Escribe la opción más corta entre `%e` y `%f` (o `%E` y `%F`). |
| `%o` | `int` | Escribe un entero en octal sin signo, sin ceros iniciales. |
| `%x`, `%X` | `int` | Escribe un entero hexadecimal sin signo (sin el prefijo `0x`). |
| `%u` | `int` | Escribe un entero decimal sin signo. |
| `%s` | `char *` (Cadena) | Imprime o lee una cadena de caracteres hasta encontrar el carácter nulo (`\0`). |
| `%p` | `void *` | Imprime una dirección de memoria (puntero). |

---

## 4. Parámetros por Línea de Comandos (`argc` y `argv`)
Recibir argumentos al ejecutar el programa desde la terminal
```js
int main(int argc, char *argv[])
```

`argc` (argument count):
<br>
nº total de argumentos introducidos en la terminal (siempre es $\ge 1$)
<br>

`argv` (argument vector):
<br>
Array de cadenas de texto (char*) con los argumentos introducidos.
- `argv[0]`: siempre contiene el nombre del programa/ejecutable (ej: `./arguments`).

- `argv[1]` a `argv[argc-1]`:
<br>
Contienen los parámetros adiciones pasados por el usuario.

ejemplo iteración de argumentos:
```js
#include <stdio.h>

int main(int argc, char *argv[]) {
    // Si argc es igual a 1, solo pusimos "./saludar"
    if (argc == 1) {
        printf("¡Hola, desconocido!\n");
    } 
    // Si argc es 2, pusimos el programa + una palabra extra (ej: Juan)
    else if (argc == 2) {
        printf("¡Hola, %s!\n", argv[1]); // argv[1] contiene "Juan"
    } 
    else {
        printf("Has puesto demasiados argumentos.\n");
    }

    return 0;
}
```
si en comando lo ejecutas solo:
```js
$ ./saludar

// resultado: ¡Hola, desconocido! 
// (Aquí argc valía 1).
```

si le pasas un parámetro:
```js
$ ./saludar Juan

// resultado: ¡Hola, Juan! 
// (Aquí argc valía 2, y argv[1] guardaba la palabra "Juan").
```

---

## 5. Punteros, Cadenas y Estructuras
### Manejo de Cadenas y Punteros
- Lectura de cadenas con espacios:

leer hasta encontrar un salto de línea.
```js
scanf("%[^\n]s", str)
```

- Aritmética de Punteros en Cadenas:
```js
char cadena[200], cadena2[200];

// posicionado primer caracter de la cadena
char *p1 = cadena;
char *p2 = cadena2;

// mientras que el caracter no sea nulo / no se acabe la cadena
while (*p1 != '\0') {
    *p2 = *p1 - 32; // Ejemplo: convertir minúscula a mayúscula en ASCII
    p1++;
    p2++;
}
*p2 = '\0'; // Importante: añadir el carácter nulo final
```

> ### EN TABLA ASCII
> Estándar donde cada letra, número y símbolo tiene asignado un número entero.
>
> Si miras la tabla ASCII:
>
> - La letra `a` minúscula tiene asignado el número decimal **97**.
> - La letra `A` mayúscula tiene asignado el número decimal **65**.

### Estructuras (`struct`)
permite agrupar diferentes variables bajo un mismo nombre.

ejemplo sencillo:
```js
// Definimos la estructura "Alumno"
struct Alumno {
    char nombre[50];
    int edad;
    float nota;
};
```

ejemplo dentro de un main();
```js
int main() {
    // Creamos una variable llamada 'estudiante1' de tipo struct Alumno
    struct Alumno estudiante1;

    // Rellenamos sus compartimentos usando el punto (.)
    estudiante1.edad = 20;
    estudiante1.nota = 8.5;

    printf("La nota del alumno es %.1f\n", estudiante1.nota);
    return 0;
}
```

### 6. Paso de parámetros: Valor vs Referencia

| Tipo de Paso | Sintaxis al Llamar | Sintaxis en Función | Efecto |
| :--- | :--- | :--- | :--- |
| **Por Valor** | `funcion(var);` | `void funcion(int x)` | La función recibe una **copia**. Modificar `x` **no** cambia la variable original. |
| **Por Referencia** | `funcion(&var);` | `void funcion(int *x)` | La función recibe la **dirección de memoria**. Modificar `*x` **sí** cambia la variable original. |

ejemplo por valor ((**NO funciona como esperamos para modificar la variable**):):
```js
void sumarCinco(int numero) {
    numero = numero + 5; // Modifica la copia, no el original
}

int main() {
    int x = 10;
    sumarCinco(x); // Pasamos 'x' por valor (una fotocopia)
    
    printf("x vale: %d\n", x); // ¡Seguirá valiendo 10! La función modificó la fotocopia.
    return 0;
}
```

ejemplo por referencia (**SÍ modifica el original**):
```js
// Usamos un puntero (int *numero) para recibir la dirección de memoria
void sumarCincoReal(int *numero) {
    *numero = *numero + 5; // Modifica el contenido que hay en esa dirección original
}

int main() {
    int x = 10;
    sumarCincoReal(&x); // Pasamos la DIRECCIÓN de x usando '&'
    
    printf("x vale: %d\n", x); // ¡Ahora valdrá 15! Porque modificamos el original.
    return 0;
}
```

---

### Utilidades y Órdenes del shell para procesos
crear nuevo directorio
```js
mkdir nombre_carpeta
```

entrar al directorio
```js
cd nombre_carpeta
```

lista información sobre la ejecución de los procesos en Linux
```js
ps u

// lista completa y detallada
ps -la
```
Columnas clave que debes conocer:
- ``PID``: El número de identificación del proceso.   
- ``PPID``: El PID del proceso padre (quién lo creó).   
- ``STAT``: El estado del proceso. Los más comunes son ``R`` (Running, ejecutándose), ``S`` (Sleeping, esperando a que pase algo) y ``Z`` (Zombie).  

---

muestra tabla dinámica con procesos que más CPU y memoria consumen
```js
top
```

matar procesos
```js
// mata el proceso cuyo número PID indiques
kill -9 PID
kill -SIGKILL PID

// mata de golpe todos los procesos que tengan ese nombre
killall nombre_programa

mata proceso que corre en primer plano
Ctrl + C
```

---

### Directorio Virtual Linux (/proc)
Sistema en Linux crea directorio virtual llamado /proc que es como el panel de control del kernel
```js
/proc
```

Dentro de esas carpetas hay ficheros de texto con información:
- ``cmdline``: Muestra comando exacto con el que lanzó el proceso
- ``cmdline``: Muestra cuánta memoria RAM física (VmRSS) o virtual (VmSize) está consumiendo.
- `cpuinfo`: Información sobre el procesador de tu ordenador

---

filtro `grep`: busca palabras o patrones dentro de un texto o listado
```js
ps aux | grep bash
```

---

### Automatizando con Shell Scripts (Bash)
Un Shell Script es un archivo de texto plano donde escribes varias órdenes de Linux en orden para que se ejecuten solas.

- ``Shebang`` (***#! /bin/bash***): primera línea obligatoria de cualquier script para indicarle al sistema que debe interpretarlo usando Bash.

- `Dar premisos de ejecución:`
```js
chmod +x mi_script
```

---

### Variables y Argumentos en Scripts:
- ``$1``, ``$2``, ``$3``...: Recogen los argumentos que le pasas al script al ejecutarlo en la terminal (ej: ``./script juan 20`` -> ``$1`` es "juan").   
- ``$#``: Cuenta el número total de argumentos que le has pasado.   - ``$@``: Contiene la lista completa de todos los argumentos.  

### Estructuras de Control (``for`` y ``if``)
Bucle `for` (para repetir algo varias veces o recorrer listas)
```c
for i in $@
do
    echo "Argumento: $i"
done
```

condicional ``if`` con la orden ``test`` (para comparar números, textos o comprobar si un archivo existe)
```c
if test $proceso -gt 5
then
    echo "Hay más de 5 procesos"
else
    echo "Hay 5 o menos procesos"
fi
```
`-gt`: greater than
<br>

`-ep`: igual
<br>

`-lt`: menor que

---

### Filtros avanzados
reemplazar unas letras por otras o borrar cosas
```c
// pone los tabuladores donde los dos puntos
tr ':' '\t' < archivo.txt
```

recortar columnas de un texto
```c
// solo quiero la primera y la tercera
awk '{print $1, $3}' archivo.txt
```

---

### Estructura Básica de un Shell Script en Bash
```c
#!/bin/bash
# Cabecera obligatoria (Shebang)

echo "El script se llama: $0"
echo "Número de argumentos: $#[cite: 18]"

# Bucle for para recorrer argumentos[cite: 18]
for arg in $@
do
    echo "Procesando: $arg"
done

# Condicional if usando test para comparar números (-gt = mayor que)[cite: 20]
if test $# -gt 0
then
    echo "Se han introducido argumentos."
else
    echo "No hay argumentos."
fi
```

---

# Creación de Procesos en UNIX - FSO

Llamadas al sistema para la gestión, clonación (`fork`), sustitución (`exec`), y sincronización (`wait`/`exit`) de procesos.

---

## 1. Llamadas al Sistema Principales

| Llamada | Descripción | Valor de Retorno / Uso |
| :--- | :--- | :--- |
| `fork()` | Clona el proceso actual creando un hijo idéntico. | Retorna `0` al hijo, el `PID` del hijo al padre, y `-1` si hay error. |
| `exit(status)` | Termina normalmente el proceso y pasa su estado al padre. | No retorna valor. Si el padre no hace `wait`, genera un *zombie*. |
| `wait(&stat)` | Suspende al padre hasta que finalice cualquiera de sus hijos. | Retorna el `PID` del hijo que finalizó (o `-1` si no hay hijos). |

---

## 2. La Familia `exec()` (Sustitución de Imagen de Memoria)
Cambia el código y memoria de un proceso por un nuevo programa ejecutable[cite: 29, 34, 38]. El `PID` se mantiene.

* **Sufijos de las variantes:**
  * **`l` (List):** Argumentos pasados como lista de strings individuales (terminados en `NULL`).
  * **`v` (Vector):** Argumentos pasados en un array de punteros (`argv`).
  * **`p` (Path):** Busca el ejecutable automáticamente usando la variable de entorno `PATH`.
  * **`e` (Environment):** Permite definir un entorno de ejecución personalizado (`envp`).

### Ejemplos de sintaxis:
```c
// Usando ruta y lista (execl)
execl("/bin/ls", "ls", "-l", NULL);

// Usando búsqueda por PATH y vector (execvp)
char *args[] = {"ls", "-l", NULL};
execvp("ls", args);
```

---

### Ejemplo 1. Clonador básico
al llamar `fork()`, el programa se duplica y se ejecuta por dos caminos distintos a la vez (el padre y el hijo).

código(`probar_fork.c`):
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t resultado;

    printf("--- ANTES del fork (Solo hay 1 proceso) ---\n");

    resultado = fork(); // ¡Aquí el proceso se divide en dos![cite: 29, 37]

    if (resultado == 0) {
        // Esto solo lo ejecuta el HIJO
        printf("--> Hola, soy el HIJO. Mi PID es %d y mi padre es %d\n", getpid(), getppid());
    } else {
        // Esto solo lo ejecuta el PADRE
        printf("--> Hola, soy el PADRE. Mi PID es %d y el PID de mi hijo creado es %d\n", getpid(), resultado);
    }

    return 0;
}
```

compilarlo y ejecutarlo:
```js
gcc -Wall probar_fork.c -o probar_fork
./probar_fork
```