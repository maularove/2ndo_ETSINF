# EJERCICIOS T4
Las etapas en las que viajan los datos son: 
- `IF` (búsqueda)
- `ID` (descodificación y lectura de registros)
- `EX` (ejecución)
- `MEM` (memoria)
- `WB` (escritura en registros)

## Tipos de Conflictos y Cómo Resolverlos

### A. Conflictos de Datos

Ocurre cuando una instrucción necesita un dato (ya sea de la ALU o de la memoria mediante un `lw`) que aún no se ha escrito o calculado.
<br>

***Alternativa 1: Ciclos de parada:***
<br>
El procesador frena automáticamente la ejecución introduciendo retrasos (stalls), lo que empeora el CPI.
<br>

***Alternativa 2: Instrucciones `nop`:***
<br>
Modificas el código a mano añadiendo instrucciones `nop` para dejar una "distancia segura" (mínimo 3 instrucciones) entre instrucciones dependientes.
<br>

***Alternativa 3: Reordenación de código:***
<br>
Mueves instrucciones independientes para llenar los huecos de dependencia sin penalizar el rendimiento ni añadir instrucciones extra (es la opción más eficiente sin coste de hardware).
<br>

### B. Conflictos de Control
Son provocados por los cambios en el flujo de ejecución (instrucciones de salto como beqz).   

***Alternativa 1: Ciclos de parada:*** 
<br>
El procesador espera a que se resuelva el salto, introduciendo ciclos de parada adicionales. 
<br>  

***Alternativa 2: Predicción de saltos (Predict not Taken):*** 
<br>
El procesador asume por defecto que el salto no se va a cumplir y continúa ejecutando la siguiente instrucción correlativa, evitando pararse a menos que el salto se tome.

---

## Escritura y lectura en el mismo ciclo
Los registros se escriben en el primer semiciclo y se leen en el segundo.
<br>

Si la instrucción productora está en ***WB*** y la consumidora en ***ID*** en el mismo ciclo, ***la lectura es correcta***.

Distancia segura:
<br>
Para que no haya conflicto (riesgo RAW - Read After Write), debe haber al menos 3 instrucciones de separación entre la que produce el dato y la que lo lee.

---

ej. Sea el siguiente fragmento de código MIPS que se ejecuta en un procesador segmentado con 5 etapas
```cs
ori $8, $0, 20
lui $7, 0x0005
ori $7, $7, 0xFFFF
lw $4, 0($8)
add $6, $6, $4
sw $7, 0($8)
addi $8, $8, -4
andi $1, $8, 0x3A
```

Identificamos tres puntos críticos donde: 
- una instrucción ***lee un registro*** que la instrucción anterior 
- ***acaba de escribir*** sin la separación de ciclos suficiente