# EXAMEN DE PRÁCTICAS - LTP (Tipo A)

## Anexo - Código fuente Java - Examen Tipo A

```cs
// La clase Entity representa elementos de un juego
// con una caracter´ıstica com´un (poder base)
//
public abstract class Entity implements Comparable<Entity> {
    protected int basePower; // Nivel de poder básico
    
    public boolean equals(Object o) {
        return (o instanceof Entity) && basePower == ((Entity)o).basePower;
}

public int compareTo(Entity e) {
    int difP = basePower - e.basePower;
    if (difP == 0) return 0;
    if (difP > 0) return 1;
    return -1;
}

public abstract int power();
}

// Character es una subclase de Entity que representa personajes de un juego
//
public class Character extends Entity {
    private String name; // Nombre del personaje
    private int level; // Se utiliza para calcular el nivel de poder de un personaje

    // como basePower + level * 2
    public Character(String n, int l, int b) {
        name = n; level = l; basePower = b;
    }

    public String toString() { return name + " (lvl " + level + ")"; }
}

// La clase GameWorld representa un conjunto de entidades dentro de un juego
//
public class GameWorld {
    protected ArrayList<Entity> entities;
    public GameWorld() { entities = new ArrayList<Entity>(); }
    public int size() { return entities.size(); }
    public void addEntity(Entity e) { entities.add(e); }
}

// Fighter es una subclase de Character que representa cierto tipo de personajes de un juego
//
public class Fighter extends Character {
...
// el c´odigo de esta clase no es relevante para resolver los ejercicios del examen
}
// La clase ArrayList, incompleta (solamente cabeceras de algunos m´etodos relevantes)
//
public class ArrayList<E> extends ... implements ... {
...
    boolean add(E e) {...} // a~nadir un elemento al final de la lista
    void add(int index, E e) {...} // a~nadir un elemento, en la posici´on dada como argumento
    E remove(int index) {...} // eliminar un elemento, el de la posici´on dada como argumento
    E get(int index) {...} // obtener un elemento, el de la posici´on dada como argumento
    int size() {...} // obtener el n´umero de elementos
    boolean isEmpty() {...} // comprobar si la lista est´a vac´ıa
...
}
```

### ejercicio 1
La clase Character facilitada en el anexo NO compila. Escribe el método que falta en esa clase para
que compile correctamente, y de forma que dicho méetodo calcule lo que corresponda.

```cs
public int power() {
    return basePower + level * 2;
} 
```

<br>

---

### ejercicio 2
Sobreescribe el método `equals` en la clase Character teniendo en cuenta que el método debe devolver
`true` solo si los dos objetos que se comparan cumplen las siguientes condiciones:

- Son instancias de la clase Character

- Tienen el mismo poder base (atributo basePower), nombre (atributo name) y nivel (atributo
level)

Y debe devolver `false` en caso contrario. Se debe reutilizar código de la superclase

```cs
// los dos son instancias de la clase
// mismo poder base, nombre y nivel
public boolean equals(Object o) {
    return o instanceof Character &&
    super.equals(o) &&
    name.equals(((Character)o).name) &&
    level == ((Character)o).level
}
```

<br>

---

### ejercicio 3
Escribe un método `removeEntity` en la clase GameWorld teniendo en cuenta que el método debe
recibir un argumento entero (i), y eliminar de la lista entities el objeto que esté en esa posición
i, siempre y cuando esa posición sea válida. (Si se recibe un valor de i que no corresponda a una
posición válida en entities, el método no debe modificar el objeto).

```cs
public void removeEntity(int i) {
    if (i >= 0 || i < size()) {
        entities.remove(i);
    }
}
```

<br>

---

### ejercicio 4
Escribe un método `find` en la clase GameWorld teniendo en cuenta que el método debe recibir un
objeto de la clase Entity, y devolver la posición de la primera aparición de ese objeto recibido en el
atributo entities. Si el objeto recibido como argumento no estuviera en entities, el método debe
devolver -1.

```cs
public int find(Entity e) {
    for (int i = 0; i < size(); i++) {
        if (entities.get(i).equals(e)) return i;
    }
    return -1;
}
```

<br>

---

### ejercicio 5
Escribe una clase BattleWorld (para representar un mundo concreto) que extienda la clase GameWorld.
En esta subclase, se debe sobreescribir el m´etodo addEntity de forma que solo se añada a entities
el Entity recibido si es una instancia de Fighter.

```cs
// super hereda addEntity de GameWorld

// hace filtro comprueba instancia
public class BattleWorld extends GameWorld {
    public void addEntity(Entity e) {
        if (e instanceof Fighter) super.addEntity(e);
    }
}
```
