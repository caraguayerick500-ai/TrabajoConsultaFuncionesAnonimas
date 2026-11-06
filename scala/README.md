```scala
case class Pelicula(titulo: String, genero: String, anio: Int, duracion: Int, calificacion: Double)
  val peliculas = List(
    Pelicula("El Padrino", "Drama", 1972, 175, 9.2),
    Pelicula("Parásitos", "Suspenso", 2019, 132, 8.5),
    Pelicula("Interestelar", "Ciencia ficción", 2014, 169, 8.7),
    Pelicula("Gladiador", "Acción", 2000, 155, 8.5),
    Pelicula("Toy Story", "Animación", 1995, 81, 8.3),
    Pelicula("Matrix", "Ciencia ficción", 1999, 136, 8.7),
    Pelicula("Coco", "Animación", 2017, 105, 8.4),
    Pelicula("Titanic", "Romance", 1997, 195, 7.9),
    Pelicula("Inception", "Ciencia ficción", 2010, 148, 8.8),
    Pelicula("Shrek", "Animación", 2001, 90, 7.9),
    Pelicula("Joker", "Drama", 2019, 122, 8.4),
    Pelicula("La La Land", "Romance", 2016, 128, 8.0)
  )

  // 1. Selección: películas con calificación >= 8.5
  val mejores = peliculas.filter(p => p.calificacion >= 8.5).map(_.titulo)
  println(mejores)

  // 2. Transformación: lista de títulos en mayúsculas
  val titulos = peliculas.map(p => p.titulo.toUpperCase)
  println(titulos)

  // 3. Validación: ¿alguna con calificación > 9? ¿todas posteriores a 1990?
  val hayMayorA9 = peliculas.exists(p => p.calificacion > 9)
  val todasDesde1990 = peliculas.forall(p => p.anio >= 1990)
  println(hayMayorA9)
  println(todasDesde1990)

  // 4. Conteo: cuántas son de animación
  val cantidad = peliculas.count(p => p.genero == "Animación")
  println(cantidad)
```
