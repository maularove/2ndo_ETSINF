# EXAMEN DE PRÁCTICAS - LTP (Tipo B)

## Anexo - Código fuente Java - Examen Tipo B

```cs
// La clase ArrayList, incompleta (solamente cabeceras de algunos m´etodos relevantes)
//
public class ArrayList<E> extends ... implements ... { ...
    boolean add(E e) {...} // a~nadir un elemento al final de la lista
    void add(int index, E e) {...} // a~nadir un elemento, en la posici´on dada como argumento
    E remove(int index) {...} // eliminar un elemento, el de la posici´on dada como argumento
    E get(int index) {...} // obtener un elemento, el de la posici´on dada como argumento
    int size() {...} // obtener el n´umero de elementos
    boolean isEmpty() {...} // comprobar si la lista est´a vac´ıa
...
}

// La clase Animal representa cualquier animal de un zool´ogico
//
public abstract class Animal implements Comparable<Animal> {
    private String name;
    public Animal(String name) { this.name = name; }
    public String getName() { return name; }
    public abstract double weight();
    
    public boolean equals(Object o) {
        return (o instanceof Animal) && weight() == ((Animal)o).weight();
    }

    public int compareTo(Animal a) { return Double.compare(weight(), a.weight()); }
}

// La clase Mammal representa un animal mam´ıfero
//
public class Mammal extends Animal {
    private double mammalWeight;

    public Mammal(String name, double weight) {
        super(name);
        this.mammalWeight = weight;
    }

    public double weight() { return mammalWeight; }
    public String toString() { return getName() + " (" + mammalWeight + " kg)"; }
}

// La clase Zoo contiene una colecci´on de animales
//
public class Zoo {
    protected ArrayList<Animal> animals;
    public Zoo() { animals = new ArrayList<Animal>(); }
    public int size() { return animals.size(); }
    public void addAnimal(Animal a) { animals.add(a); }
}
```

<br>

### ejercicio 1
Se desea añadir una clase Bird que herede de Animal y sobreescriba el método toString() para que
muestre el nombre (atributo name), peso (atributo birdWeight) y que es un pájaro (un String como
“pájaro”). Rellena los huecos para completar la implementación de la clase, reutilizando código si es
posible.

```cs
public class Bird extends Animal {

    private double birdWeight;

    // construtor
    public Bird(String name, double weight) {
        super(name);
        this.birdWeight = weight;
    }

    public double weight() {
        return birdWeight;
    }

    public String toString() {
        return "El animal " + super.getName() + " pesa " + birdWeight() + " y es un pájaro."  
    } 
}
```

<br>

---

### ejercicio 2
Sobreescribe el método equals en la clase Mammal teniendo en cuenta que el método debe devolver
true solo si los dos objetos que se comparan cumplen las siguientes condiciones:

- Son instancias de la clase Mammal.

- Tienen el mismo peso (atributo mammalWeight) y nombre (atributo name).

Y debe devolver false en caso contrario. Se debe reutilizar código de la superclase, si es posible.

```cs
public boolean equals(Object o) {
    return o instanceof Mammal &&

        // llama al equals y hace lo que ya hacía el equals
        super.equals(o) &&
        getName().equals(((Mammal)o).getName()) &&
}
```

---

scribe un m´etodo replaceAnimal en la clase Zoo teniendo en cuenta que el m´etodo debe recibir
un argumento entero (i) y un objeto Animal (a), reemplazar en la lista animals el objeto Animal
que est´e en esa posici´on i (siempre y cuando esa posici´on sea v´alida) y devolver el objeto Animal
reemplazado (Si se recibe un valor de i que no corresponda a una posici´on v´alida en animals, el
m´etodo no debe modificar el objeto y debe devolver null).


```
```
