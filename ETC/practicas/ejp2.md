# EJERCICIOS T2
ej. 1
***¿Cuál de las siguientes es una traducción válida de la pseudo-instrucción?***
```cs
ble $rs, $rt, A             # Salta a A si $rs <= $rt
```

`ble` => saltar a la etiqueta si $rs \le rt$.

lo que hace:
```cs
// si rt < rs; $at = 1$
// si rt >= rs; $at = 0$
slt $at, $rt, $rs

// compara resultados
// si son iguales ($at == 0) salta a A
beq $at, $zero, A
```

---

ej. 2
Supongamos estos comandos:
```cs
li $v0, 5
syscall
move $a0, $v0
li $v0, 11
syscall
```

***¿Cuál es el efecto del siguiente fragmento de código?***
> Escribe en la consola el carácter cuyo código ASCII se introduce previamente por teclado

---

ej. 3 ***Completa el programa, debe leer caracteres del teclado y escribir su código ASCII en la consola. Programa debe finalizar cuando se introduce el carácter 'f'***

```cs
li $t0, 0x66

// 12: código syscall para leer carácter
bucle: li $v0, 12

// llamada al sistema
syscall
beq $v0, $t0, fin

// llamadas del sistema reciben sus argumentos en el resgistro $a0
move $a0, $v0

// 1: cógido syscall para imprimir un número entero
li $v0, 
syscall

// j / b: volver al inicio del bucle sin ninguna condición
j bucle

// 10: código servicio syscall para terminar / detener la ejecución del programa de forma limpia (exit)
fin: li $v0, 
syscall
```

| Carácter | Decimal | Hexadecimal (0x) | Binario | ¿Qué es? |
|:---:|:---:|:---:|:---:|:---:|
| 'A' (Mayúscula) | 65 | 0x41 | 01000001 | Inicio de las mayúsculas |
| 'a' (Minúscula) | 97 | 0x61 | 01100001 | Inicio de las minúsculas |
| '0' (Número) | 48 | 0x30 | 00110000 | Inicio de los dígitos numéricos |
| ' ' (Espacio) | 32 | 0x20 | 00100000 | El espacio en blanco |

---

ej. 4
***Completa el siguiente programa que lee caracteres del teclado y los imprime en pantalla solo cuando son letras minúsculas.
Programa determina cuando se introduce el carácter 'F'***
```cs
li $s0, 'a'
li $s1, 'z'
li $s2, 'F'
bucle:  li $v0, 12
syscall
beq $v0, $s2, fin

// blt: saltar si es menor que (less than)
blt $v0, $s0, bucle

// bgt: saltar si es mayor (greater than)
bgt $v0, $s1, bucle

// lo que hay en v0 se copia en a0
move $a0, $v0

// 11: código llamada al sistema para imprimir un único caracter
li $v0, 11
```

---

ej. 5 Dado el siguiente código
```cs
i = 3
j = 0
if  i > j:
    i = i + 1
else:
    i = i - 1
print(i)
```
***Completa los espacios para traducirlo a código ensamblador:***
```cs
        .globl__main
        .text 0x00400000
__main: li $t0, 0       #j
        li $t1, 1       #i
        ble $t1, $t0, else
        addi $t1, $t1, 1
        b cont
else:   
        addi $t1. $t1, -1
cont:   move $a0, $t1
        li $v0, 1 
```

---

