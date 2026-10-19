# EJERCICIOS T1
¿Cuál es la traducción correcta de la pseudoinstrucción `la $t0, var`?

```c
// dirección
.data 0x1000000C

// 4 bytes
var: .word 26
chain: .asciiz “cornonavirus”
// Se va a ejecutar el siguiente fragmento de código:

    .text
....
la $t0, var
la $t1, chain
lw $s0, 0($t0)
lb $s1, 5($t1)
....
```

### 1º paso: descomponer número en "parte alta" y "parte baja"
<br>

***0x1000000C*** número de 32 bits, dividido en dos mitades
- 16 bits superiores (parte alta / primeros cuatro dígitos) $\rightarrow$ `0x1000`
- 16 bits inferiores (parte baja / últimos cuatro dígitos) $\rightarrow$ `0x000C`

entonces:
```c
lui $at, 0x1000
ori $t0, $at, 0x000C
```

---

ej. 2
```c
// dirección
.data 0x1000000C

// 4 bytes
var: .word 26
chain: .asciiz “cornonavirus”
// Se va a ejecutar el siguiente fragmento de código:

    .text
....
// guarda dirección de memoria de var (0x1000000C)
la $t0, var
la $t1, chain

// lee dato 
lw $s0, 0($t0)
lb $s1, 5($t1)
....
```

¿tras la ejecución de lw $s0, 0($t0), indica cuál serña el contenido de los registros $t0 y $s0?

```c
$t0 = 0x1000000C

$s0 = 26
```

---

```cs
// dirección
.data 0x1000000C

// 4 bytes
var: .word 26

// asciiz cuenta cada letra como un byte
chain: .asciiz “camioneta”

    .text
....
// guarda dirección de memoria de var (0x1000000C)
la $t0, var
la $t1, chain

// lee dato palabra (4byte)
lw $s0, 0($t0)

// lee dato byte 
lb $s1, 5($t1)
....
```

indica contenido del registro $s1 tras la ejecución de la instrucción lb $s1, 5($t1)
> n

---

```cs
// dirección
.data 0x1000000C

// 4 bytes
var1: .word 500
var2: .word 100

// asciiz cuenta cada letra como un byte
cadena: .asciiz “practica etc”

    .text
....
// guarda dirección de memoria de var (0x1000000C)
la $t0, var1
la $t1, cadena
lw $s0, 3($t0)
li $t0, var2
lw $s1, -4($t0)
lb $s2, 7($t1)
....
```

***¿que instrucción producirá un error?***
<br>

`lw $s0, 3($t0)`
- intenta leer palabra completa (word = 4 bytes)
- dirección efectiva a la que intenta acceder: 
$$\text{Dirección} = \text{Base} + \text{Desplazamiento} = \text{0x1000000C} + 3 = \mathbf{\text{0x1000000F}}$$

> word debe ser múltiplo de 4

---
Supongamos la siguiente declaración:
```cs
.data 0x10001008
A: .word 2000
B: .byte 190
C: .byte 210
Delta: .word 12000
```
***como leer correctamente 'Delta' en el registro $1.***
```cs
la $t0, 0x10001010 
lw $t1, 0($t0)
```
***Explicacion:***

dirección A (.word 2000):
<br>
`0x10001008` (donde se ubica) + 4 = `0x1000100C` (siguiente disponible)
<br>

dirección B (.byte 190): 
<br>
`0x1000100C` (donde se ubica) + 1 = `0x1000100D` (siguiente disponible)
<br>

dirección C (.byte 210): 
<br>
`0x1000100D` (donde se ubica) + 1 = `0x1000100E` (siguiente disponible)


> (**siguiente disponible: se rellenan dos bytes para que sea múltiplo de 4**)
<br> 

dirección Delta (.word 12000):
<br>
`0x10001010` 

---

Supongamos la siguiente declaración:
```cs
.data 0x10010000
H: .space 4
I: .byte 100
J: .byte 200
K: .word 300
```

completa:
```cs
lui $t0, 0x1001
lw $t2, 4($t0)
addi $t2, $t2, 0x300
sw $t2, 0($t0)
```

---

Supongamos la siguiente declaración:
```cs
.data 0x10002000
A: .space 4
B: .space 4
C: .word 0
```

completa:
```cs
lui $t0, 0x1000
ori $t0, $t0, 0x2000
lui $t1, 0x2000
sw $t1, 4($t0)
```