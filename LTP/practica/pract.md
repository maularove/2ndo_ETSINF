# POLIMORFISMO EN JAVA: HERENCIA Y SOBRECARGA

```cs
public class Circle { 

    private double x, y; private double radius;
    
    public Circle(double a, double b, double c) { 
        x = a; y = b; radius = c; 
    } 
    
    public boolean equals(Object o) { 

        // descarta objetos que no son círculos o null
        if (!(o instanceof Circle)) { 
            return false; 
        } 

        // referencia del objeto con sus atributos
        Circle c = (Circle) o; 
        return x == c.x && y == c.y && radius == c.radius; 
    } 
        
    public String toString() { 
        return "Circle:\n\t" + "Position: (" + x + "," + y + ")\n\tRadius: " + radius; 
    }
}
```

Sobreescritura:
misma firma, en una subclase, cambia el comportamiento heredado. Se resuelve en ejecución.


```cs
public boolean equals(Object o) { 
    return x == ((Circle)o).x && y == ((Circle)o).y 
    && radius == ((Circle)o).radius;
}
```

No comprueba el tipo, lanza excepciones



