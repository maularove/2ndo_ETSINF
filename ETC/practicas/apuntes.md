# Apuntes ETC Prácticas
## Instrucciones 
``li``: Guarda valor numérico constante dentro de un registro.

Procesador MIPS trabaja con instrucciones tamaño fijo (32 bits). 
<br>
En una instrucción normal tipo ensamblador, solo hay espacio físico para guardar un número de hasta 16 bits (es decir, valores entre -32.768 y 32.767)

- Si número es pequeño (ej. 25), cabe perfectamente en ***16 bits***, el ensamblador traduce el ``li`` directamente usando un ``ori`` o ``addi`` sencillo con el cero`.
- ¿Qué pasa si el número es gigante o supera los 16 bits? (ej. 753689 o dirección de memoria `0x10000000`) no cabe de una sola vez en una instrucción máquina.

Por eso, el ensamblador tiene que hacer trucos matemáticos dividiendo el número en dos mitades:
1. Los 16 bits de la parte alta (lo llamamos $K_h$).
2. Los 16 bits de la parte baja (lo llamamos $K_l$).
```c
// número decimal base 10
// lo pasaremos a hexadecimal
li $t0, 75369

// lo que es:
// lui (load upper immediate):
// carga valor de 16 bits directamente en la mitad superior (alta) de un registro, rellenando la parte abajo con ceros (0x0000).

// or (or immediate):
// realiza operación lógica OR bit a bit entre un registro y una constante de 16 bits
// rellena o completa mitad inferior (baja)
lui $at, 0x0001
ori $t0, $at, 0x2669
```
 Pasamos 75369 a hexadecimal, da 0x12669, ocupa 17 bits (+ de 16 bits) 
 <br>
 ``lui 0x0001``, ``ori 2669``

---

ejemplo:
```cs
.globl __start
.text 0x00400000
__start: li $t0, 25
         li $t1, 30
         add $s0, $t1, $t0
         add $s0, $s0, $s0
```

otro ejemplo:
<br>
- si número cabe en 16 bits:
```cs
li $t0, 500

// ensamblado lo traduce en una sola instrucción
addi $t0, $zero, 500
```

---

`la` (Load Address):
<br>
Copiar la dirección de memoria de una etiqueta directamente en un registro.
<br>

se guarda en dos instrucciones, ***lui*** y ***ori***

ejemplo:
```cs
// si dirección  es 0x10010000
lui $at, 0x1001          # Carga la parte alta de la dirección de memoria
ori $t0, $at, 0x0000     # Carga la parte baja en el registro final $t0
```
---
### Instrucción de Manipulación de Datos y Lógicas

`move` (Pseudoinstrucción):
<br>
copia el contenido de un registro a otro (ej. ***move rs, rt***).

`addi` (Add Immediate):
<br>
suma el valor de un registro con un número constante pequeño (de 16 bits, llamado "inmediato") y guarda el resultado en otro registro.
(ej. ***addi $t0, $zero, 100***)

`andi` (And Immediate):
<br>
operación lógica AND entre un registro y una constante numérica de 16 bits.
(ej. ***andi $t0, $1, 0xFFFF***).

### Instrucciones de Acceso a Memoria (Lectura y Escritura)
`lw` (Load Word):
<br>
lee palabra (4 bytes) desde una dirección en una memoria principal (RAM) y la carga dentro de un registro.

`sw` (Store Word):
<br>
lo contrario que ***lw***, coge el valor que tienes guardado en un registro y lo guarda en la memoria principal.

`sh` (Store Halfword):
<br>
guarda solo media palabra (2 bytes) desde un registro hacia la memoria principal.

### Interacción con el Sistema
`syscall` (System Call):
<br>
instrucción máquina especial que ***detiene temporalmente la ejecución normal del programa*** y ***transfiere el control al sistema operativo para pedirle un servicio*** (como imprimir un número en pantalla, leer por teclado, terminar el programa, etc.)
Simpre 

---

## Instrucciones de Salto y Bifurcación
### A. Instrucciones Máquina Nativas (Directas)
```cs
j eti                  # Salto incondicional absoluto
b eti                  # Salto incondicional (pseudoinstrucción común)
beq $rs, $rt, eti      # Salta si $rs == $rt
bne $rs, $rt, eti      # Salta si $rs != $rt
bgtz $rs, eti          # Salta si $rs > 0
bgez $rs, eti          # Salta si $rs >= 0 (¡Ojo: solo un registro!)
blez $rs, eti          # Salta si $rs <= 0 (¡Ojo: solo un registro!)
bltz $rs, eti          # Salta si $rs < 0  (¡Ojo: solo un registro!)
```

### B. Pseudoinstrucciones Comunes
```cs 
beqz $rs, eti          # Salta si $rs == 0 (se traduce a: beq $rs, $zero, eti)
bnez $rs, eti          # Salta si $rs != 0 (se traduce a: bne $rs, $zero, eti)
bgt $rs, $rt, eti      # Salta si $rs > $rt
ble $rs, $rt, eti      # Salta si $rs <= $rt
blt $rs, $rt, eti      # Salta si $rs < $rt
bge $rs, $rt, eti      # Salta si $rs >= $rt
```
---

![alt text](image-1.png)





