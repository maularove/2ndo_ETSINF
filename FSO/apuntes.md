# FUNDAMENTOS DE LOS SISTEMAS OPERATIVOS

## 1. INTRODUCCIÓN Y EVOLUCIÓN DE LOS SISTEMAS OPERATIVOS (SO)

### Sistema Operativo
- Programa <mark><u>***dirigido por eventos***</u></mark>
que actúa como <mark><u>***interfaz***</u></mark> entre los usuarios y el hardware del computador.

- Facilita el uso de la máquina, proporciona un <mark><u>***entorno cómodo***</u></mark> para ejecutar programas y administra eficientemente los recursos hardware y software

<br>

---

### El Núcleo (Kernel)
Es la parte del código del SO que <mark><u>***se carga al arrancar***</u></mark> y <mark><u>***permanece continuamente en memoria para gestionar de forma eficiente los procesos, la memoria, los archivos y los sistemas de E/S.***</u></mark>

<br>

---

### Evolución de los Sistemas

#### A. Sistemas por lotes simples

- <mark><u>***No existe***</u></mark> interacción directa usuario / máquina

- Operador agrupa trabajos similares y el ***control*** se realiza mediante un <mark><u>***monitor residente***</u></mark> (pequeño programa precursor del SO encargado de secuenciar trabajos automáticamente)

<br>

#### B. Sistemas por lotes multiprogramados

- Mantienen <mark><u>***varios trabajos en memoria simultáneamente.***</u></mark>

- Cuando un trabajo **espera una operación E/S**, <mark><u>***la CPU  salta a ejecutar otro***</u></mark>, evitando que la CPU esté ociosa.

- El SO <mark><u>***requiere añadir gestión de protección de memoria***</u></mark> y <mark><u>***planificación de CPU***</u></mark>

<br>

#### C. Sistemas de tiempo compartido

- Sistemas **multiprogramados** con <mark><u>***interacción directa***</u></mark> entre el usuario y la máquina sin operador profesional.

- objetivo principal: <mark><u>***minimizar tiempo de respuesta***</u></mark>

<br>

---

## 2. HARDWARE, MODOS DE EJECUCIÓN E INTERRUPCIONES

### Ráfaga de CPU
<mark><u>***Conjunto de ciclos de CPU consecutivos***</u></mark> que necesita un proceso en ejecución.
<br>

Los procesos **alternan ráfagas de CPU y de E/S**, comenzando y terminando siempre con una ráfaga de CPU.

<br>

---

### Modos de funcionamiento de la CPU / procesador

2 modos de funcionamiento para ***aportar la necesaria protección*** y  evitar que programas maliciosos o mal diseñados puedan poner en peligro la integridad del sistema

- Son necesarios al menos dos modos (<mark><u>***modo usuario***</u></mark> / <mark><u>***modo núcleo(privilegiado)***</u></mark>)

- En _modo privilegiado_ se ejecutan operaciones críticas como <mark><u>***inhabilitar interrupciones, modificar el mapa de memoria, programar el controlador de disco o alterar el vector de interrupciones.***</u></mark>

<br>

---

### Interrupción

Mecanismo de hardware que <mark><u>***suspende temporalmente el proceso en curso***</u></mark> para que el SO _atienda una urgencia_, tras la cual se reanuda la ejecución del proceso sin afectarlo.
<br>

Al detectarse, la máquina pasa de modo usuario a modo núcleo.

<br>

---

### DMA (Acceso Directo a Memoria)

Permite realizar <mark><u>***transferencias de datos directamente entre los dispositivos y la memoria a través del bus del sistema***</u></mark> sin saturar la CPU.

<br>

---

## 3. LLAMADAS AL SISTEMA Y PROGRAMAS DEL SISTEMA

### Llamadas al Sistema (System Calls)

Mecanismo mediante el cual los <mark><u>***procesos de usuario solicitan servicios al SO***</u></mark> (como acceso a dispositivos de E/S o memoria).
<br>

Se ejecutan siempre en <mark><u>***modo núcleo***</u></mark> para garantizar la seguridad e impedir que un usuario tome el control de la máquina.

<br>

### Secuencia de una llamada al sistema

1. `Modo Usuario`: El programa en ejecución realiza la llamada (Trap o *interrupción software*).

2. `Modo Núcleo`: El SO identifica la solicitud, ejecuta el servicio y devuelve los datos o resultados.

3. `Modo Usuario`: El programa continúa con su siguiente instrucción

<br>

### Programas del sistema

Utilidades que se ejecutan como procesos de usuario (no forman parte del núcleo) para ofrecer un *entorno cómodo*.
<br>

ej. 
- intérprete de órdenes (shell)

- herramientas de manipulación de ficheros (`cp`, `rm`)

- editores (`gedit`)

- compiladores (`gcc`)

<br>

---

## 4. ÓRDENES DE UNIX, REDIRECCIONES Y TUBERÍAS

### Intérprete de Órdenes (Shell)
Programa / utilidad del S.O que <mark><u>***actúa como interfaz***</u></mark> básica leyendo, analizando y ejecutando las órdenes del usuario (en UNIX se ejecuta como un proceso de usuario)

<br>

### Análisis de una línea de comandos compleja:

```cs
cat lista | grep lopez | wc -l > n_lopez 2> error
```

- Procesosso involucrados: `cat`, `grep`, `wc` son procesos inteconectados mediante tuberías (`|`).

- Ficheros involucrados: `lista` (fichero de entrada), `n_lopez` (fichero donde se redirige la salida estándar) y `error` (fichero donde se redirige la salida de errores).

<br>

### Redirecciones en UNIX:
- Se realizan modificando las tablas de descriptores de ficheros abiertos.

- Operador `>` redirige la sálida estándar

- La expresión `2>` redirige específicamente la salida de error estándar.

