```java
package tiposporblemas;
import java.util.List;
import java.util.stream.Collectors;

public class TiposPorblemas {

    record Pelicula(String titulo, String genero, int anio, int duracion, double calificacion) {}
    
    public static void main(String[] args) {
        List<Pelicula> peliculas = List.of(
            new Pelicula("El Padrino", "Drama", 1972, 175, 9.2),
            new Pelicula("Parasitos", "Suspenso", 2019, 132, 8.5),
            new Pelicula("Interestelar", "Ciencia ficción", 2014, 169, 8.7),
            new Pelicula("Gladiador", "Acción", 2000, 155, 8.5),
            new Pelicula("Toy Story", "Animación", 1995, 81, 8.3),
            new Pelicula("Matrix", "Ciencia ficción", 1999, 136, 8.7),
            new Pelicula("Coco", "Animación", 2017, 105, 8.4),
            new Pelicula("Titanic", "Romance", 1997, 195, 7.9),
            new Pelicula("Inception", "Ciencia ficción", 2010, 148, 8.8),
            new Pelicula("Shrek", "Animación", 2001, 90, 7.9),
            new Pelicula("Joker", "Drama", 2019, 122, 8.4),
            new Pelicula("La La Land", "Romance", 2016, 128, 8.0)
        );

        // 1. Selección: películas con calificación >= 8.5
        List<String> mejores = peliculas.stream()
            .filter(p -> p.calificacion() >= 8.5)
            .map(Pelicula::titulo)
            .collect(Collectors.toList());
        System.out.println("Seleccion: " + mejores);

        // 2. Transformación: lista de títulos en mayúsculas
        List<String> titulos = peliculas.stream()
            .map(p -> p.titulo().toUpperCase())
            .collect(Collectors.toList());
        System.out.println("Transformacion: " + titulos);

        // 3. Validación: ¿alguna con calificación > 9? ¿todas posteriores a 1990?
        boolean hayMayorA9 = peliculas.stream().anyMatch(p -> p.calificacion() > 9);
        boolean todasDesde1990 = peliculas.stream().allMatch(p -> p.anio() >= 1990);
        System.out.println("Validacion exists: " + hayMayorA9);
        System.out.println("Validacion forall: " + todasDesde1990);

        // 4. Conteo: cuántas son de animación
        long cantidad = peliculas.stream()
            .filter(p -> p.genero().equals("Animacion"))
            .count();
        System.out.println("Conteo: " + cantidad);
    }
}
```
