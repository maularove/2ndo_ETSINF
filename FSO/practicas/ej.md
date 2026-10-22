# SIMULACRO PRÁCTICAS FSO

### ejercicio 1.
***Rellene los huecos en el siguiente código teniendo en cuenta las variables y funciones ya definidas:***
```cs
#include <stdio.h>
#include <stdlib.h>

int func_add (int dd);
void func_power (int *pp);

int main() {
    int val = 50;
    char c = 'a';
    
    printf("write your option (a or b):\n");
    scanf("%c", &c);
    
    if (c == 'a') {
        printf("First option\n");
        val = func_add(val);
    } else if (c == 'b') {
        printf("Second option\n");
    }
    
    func_power(&val);
    printf("val = %d\n", val);
    exit(0);
}

int func_add (int dd) {
    return dd + dd;
}

void func_power (int *pp) {
    *pp = (*pp) * (*pp);
}
```

---

### ejercicio 2.
***Escriba en los huecos las órdenes y opciones necesarias para que al compilar el archivo fuente.c se genere el archivo de código ejecutable fuente***

```cs
$ gcc -v -o fuente fuente.c
```

---

### ejercicio 3.
***Indique la salida obtenida con la ejecución del siguiente código C.***
```cs
#include <stdio.h>
int x=2;
int m(int *y) {
    x=2;
    *y=3;
    return(x);
}

int main() {
    int x=3;
    int y=2;
    y=m(&y);
    printf("(%d,%d)\n",x,y);
}

resultado:
<br>
(3,2)
```

### ejercicio 4.
***Un shell-script puede utilizar los argumentos con que se le invoca en la línea de órdenes. Complete el siguiente código para verificar que se ha recibido un argumento al ejecutar el shell-script y, en caso contrario, mostrar un mensaje de error que muestre un ejemplo de línea de órdenes apropiada, con el nombre del script incluido.***

```cs
// lt (low to)
// $# (número total de argumentos que le has pasado al script en la línea de órdenes)
if test $# -lt 1
then
    echo "Este programa necesita un argumento. Prueba con:"
    echo "\$ $0 nombre_de_fichero"
    exit 1
fi
```

---

### ejercicio 5.
***Rellene los espacios propuestos para que al ejecutarlo se generen 5 procesos en vertical o cadena, de manera que cada proceso creado tenga un sólo hijo (excepto el último) y los 5 procesos impriman el mensaje "I am":***

```cs
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#define MAX_PROP 4

int main (int argc, char *argv[]) (
int i;
int val_return;

for (i=0; i<MAX_PROP; i++) (
val_return = fork();
    if (val_return == 0) (
        break;
    )
)

printf("I am \n");
sleep(15);
return 0;
)
```

---

### ejercicio 6.
***Completar los parámetros que falta en la orden execlp() del siguiente código para que se ejecute la orden, ls -la***
```cs
int main(int argc, char *argv[])
{
    // segundo hueco: el mismo nombre del programa (ls)
    execlp("ls", "ls", "-la", 0);
} // end main()
```

---

### ejercicio 7.
***Indica qué tendríamos que añadir o cambiar en el siguiente código para que todos los hilos finalicen correctamente:***

```cs
#include <ALL-INCLUDES >
void *Imprimir (void *ptr) {
    char *message;
    message = (char *) ptr;
    write (1, message, strlen(message));
}

int main() {
    pthread_t thread1, thread2;
    pthread_attr_t attr;
    pthread_attr_init(&attr);
    pthread_create(&thread1, &attr, Imprimir, "Soy el Hilo 1\n");
    pthread_create(&thread2, &attr, Imprimir, "Soy el Hilo 2\n");

    // solución
    pthread_exit(NULL)
}
```
El hilo principal tendría que acabar con la función thread_exit en lugar del exit.

---

### ejercicio 8.
***En la Práctica 5 hicimos la suma de los elementos una matriz, aprovechando la concurrencia que nos permite la creación de hilos. De forma que creamos un hilo por cada fila de la matriz para que realiza la suma de dicha fila. Si comparamos los tiempo de ejecución (T) real y en modo sistema, de la solución concurrente (con hilos) con la versión secuencial (sin hilos), rellenar las dos casillas siguientes con uno de los siguientes caracteres, según corresponda: '>', '<' o '='***

***tiempo real:***
<br>
T concurrente `>` T secuencial concurrente

<br>

***tiempo modo sistema:***
<br>
T concurrente sistema `>` T secuencial sistema

---

### ejercicio 9.
***Dado el siguiente código donde falta un ";" para finalizar una sentencia. Indique que efecto podría causar esto al compilar dicho código para que se genere el archivo con código ejecutable numbers***

```cs
#include <stdio.h>
#define N

int Number;

int main() {
    int i;
    Number =N;
    printf ("The first %d natural numbers are:\n", Number);

    for (i=0; i<Number; i++) {
        printf(" %d \n",i);
    }
    printf("BYE\n") // aquí falta el ;
    return(0);
}
```

Causa un error de compilación con un mensaje del tipo "Error: falta el carácter terminador" y no se genera el archivo numbers.

---

### ejercicio 10.
***Indique la salida obtenida con la ejecución del siguiente código C.***

```cs
#include <stdio.h>

int x = 2;

int m() {
    x=4;
    return(x);
}

int main() {
    int x=3;
    int y=2;
    y=m();
    printf("(%d,%d)\n",x,y);
}
```

La salida es:
<br> 
(3, 4)

---

### ejercicio 11.
***Marque las afirmaciones que son correctas:***

A. ❌ La orden kill -9 3456 es incorrecta porque no especifica el nombre de la señal a enviar

B. ✅ La orden kill -SIGKILL 3456 envía la señal SIGKILL al proceso con pid 3456

C. ❌ La orden killall -SIGKILL 1000 matará todos los procesos del usuario en 1000ms

D. ✅ La orden killall -SIGKILL sleep mata todos los procesos con nombre "sleep"

---

### ejercicio 12.
***Dado el siguiente código:***

```cs
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    
    printf("Parent process %ld \n", (long)getpid());
    
    fork();
    
    printf("I am %ld process, my parent is %ld\n",
    (long)getpid(), (long) getppid());
    
    sleep(15);
    return 0;
}
```

el resultado de su ejecución es el siguiente:
```cs
I am 1168 process, my parent is 1068
I am 1169 process, my parent is 1168
Indica el PID del proceso padre y el PID del proceso hijo. Padre = 1168, Hijo = 1169
```

---

### ejercicio 13.
***Dado el siguiente código donde la declaración de la variable i está comentada. Indique que efecto podría causar esto al compilar dicho código para que se genere el archivo con código ejecutable numbers***

```cs
#include <stdio.h>
#define N

int Number;
int main() {
    // int i; /* declaración comentada */
    Number =N;
    printf ("The first %d natural numbers are:\n", Number);
    
    for (i=0; i<Number; i++) {
        printf(" %d \n",i);
    }

    printf("BYE\n");
    return(0);
}
```

Causa un error de compilación y no se genera el archivo ejecutable numbers.

---

### ejercicio 14.
***Indique la salida obtenida con la ejecución del siguiente código C***

```cs
#include <stdio.h>
int x=2;

int m() {
    x=4;
    return(x);
}

int main() {
    int x=3;
    int y=2;
    y=m();
    printf("(%d,%d)\n",x,y);
}
```

La salida es:
<br>
(3,4)

---

### ejercicio 15
***Indique la salida obtenida con la ejecución del siguiente código C.***

```cs
#include <stdio.h>
int x = 2;

int m(int *y) {
    x = 2;
    *y = 3;
    return(x);
}

int main(){
    int x = 3;
    int y = 2;
    y = m(&y);
    printf("(%d, %d)\n", x, y);
}
```

La salida obtenida es:
<br>
(3,2)

---

### ejercicio 16.
***Señale cuáles de las siguientes afirmaciones son correctas:***

✅ A. El directorio /proc contiene en su interior un directorio por cada proceso actualmente en ejecución

✅ B. /proc/1034/status es un archivo de texto con información acerca del proceso con pid 1034

❌ C. La orden cat /proc/1034 mostrará información acerca del proceso con pid 1034

✅ D. La orden cat /proc/cpuinfo mostrará información acerca del procesador

---

### ejercicio 17.
***Seleccione de las siguientes órdenes, las que permiten extraer la línea de un fichero que contiene una determinada cadena.***

```cs
awk '/cadena/ { print }' fichero

// o

grep cadena fichero
```

---

### ejercicio 18.
***Indique la salida obtenida con la ejecución del siguiente código C.***

```cs
#include <stdio.h>
int x = 2;

int m(int *y) {
    int x = 4;
    *y = 3;
    return(x);
}

int main() {
    int x = 3;
    int y = 2;
    y = m(&y);
    printf("(%d, %d)\n", x, y);
}
```

La salida obtenida es:
<br>
(3,4)

---

### ejercicio 19.
***Marque las afirmaciones que son correctas:***

A. ❌ El shell es el gestor de procesos del sistema operativo

_(el shell es una interfaz de comandos para que el usuario interactúe con el sistema)_

<br>


B. ✅ El kernel es el componente principal del sistema operativo, su código se ejecuta en modo privilegiado

C. ✅ El shell interpreta las órdenes que introduce el usuario

D. ✅ El kernel se encarga de realizar la gestión de los fork (llamada al sistema / system call)

---

### ejercicio 20.
***Rellena los espacios propuestos para que al ejecutarse se generen 5 procesos en vertical o cadena, de manera que cada proceso creado tenga un sólo hijo (excepto el último) y los 5 procesos impriman el mensaje "I am: "***

```cs
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

#define NMAX_PROP 5

int main(int argc, char *argv[]) {
    int i;          // <--- Falta declarar la variable i del bucle
    int val_return;

    for (i = 0; i < NMAX_PROP; i++) {
        val_return = fork();
        if (val_return == 0) {
            // child process (se deja vacío para que el hijo continúe el bucle)
        } else {
            // parent process (el padre rompe el bucle para no crear más hijos)
            break;
        }
    }

    printf("I am\n");
    sleep(15);
    return 0;
}
```

### ejercicio 21.
***Completa las casillas con los valores que se visualizarán al ejecutar el siguiente programa***

```cs
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#define NMAX_PROP 2

int main(int argc, char *argv[]) {

    int val_return;

for (int i=0; i<NMAX_PROP; i++) {
    val_return = fork();
    if (val_return == 0) {
        printf("I am %d( process, my parent is %d\n", (long)getpid(),(long)getppid());
    } else {
        printf("I am %d( process, my parent is %d\n", (long)getpid(),(long)getppid());
    sleep(10);
}
}

printf("I am %d( process, my parent is %d\n", (long)getpid(),(long)getppid());
sleep(10);
return 0;
}
```

La salida es:
```cs
Salida inicial:
I am 1341 process, my parent is 1340
I am 1340 process, my parent is 1068
I am 1342 process, my parent is 1340

Salida después de 20 segundos:
I am 1341 process, my parent is 1
I am 1341 process, my parent is 1068
I am 1342 process, my parent is 1
```

---

### ejercicio 22.
***Indica cuál de las siguientes respuestas es correcta para el siguiente código:
#include <<ALL-HEADERS>>***

```cs
void *Imprimir(void *ptr) {
    char *message;
    message = (char *) ptr;
    printf("%s \n", message);
    pthread_exit(NULL);
}

int main() {
    pthread_t thread1, thread2;
    pthread_attr_t attr;
    pthread_attr_init(&attr);
    pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_JOINABLE);
    
    pthread_create(&thread1, &attr, Imprimir, "Soy el Hilo 1");
    pthread_create(&thread2, &attr, Imprimir, "Soy el Hilo 2");
    
    pthread_attr_destroy(&attr);
    
    pthread_exit(NULL);
}
```

El hilo principal correspondiente a la función main, puede finalizar antes de que finalice el hilo creado con _pthread_create_

<br>

El efecto de `pthread_exit(NULL)` en el `main`: 
<br>

Cuando el hilo principal (`main`) termina ejecutando `pthread_exit(NULL)`, ***solo se apaga el hilo principal***, pero el proceso en sí no muere. Esto permite que los hilos secundarios (`thread1` y `thread2`) sigan ejecutándose. Por lo tanto, el hilo principal finaliza (sale) y deja a los hilos trabajando o terminando después.

---

### ejercicio 23.
***Completa los huecos en el código del bucle para que pueda mostrar un listado de los argumentos pasados en la línea de órdenes:***

```cs
for (i = 0; i < argc; i++) {
    printf("Argumento %u es %s\n", i, arg[i]);
}
```