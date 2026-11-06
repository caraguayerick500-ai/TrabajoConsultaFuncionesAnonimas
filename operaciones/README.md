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

  // 4.1 sortBy: ordenar de menor a mayor duración
  val porDuracion = peliculas.sortBy(p => p.duracion).map(p => (p.titulo, p.duracion))

  // 4.2 groupBy: agrupar por género (se cuenta y se ordena por nombre para que la salida sea estable)
  val porGenero = peliculas.groupBy(p => p.genero)
  val cantidadPorGenero = porGenero.map { case (genero, lista) => (genero, lista.size) }.toList.sortBy(_._1)


  // 4.3 find: primera película de romance (y un caso sin resultado)
  val primeraRomance = peliculas.find(p => p.genero == "Romance")
  val sinResultado = peliculas.find(p => p.calificacion > 9.5)


  // 4.4 partition: separar largas (>= 140 min) y cortas
  val (largas, cortas) = peliculas.partition(p => p.duracion >= 140)
  println(s"partition largas: ${largas.map(_.titulo)}")
  println(s"partition cortas: ${cortas.map(_.titulo)}")

  // Combinación: géneros con 2 o más películas, de mayor a menor cantidad
  val generosPopulares = peliculas
    .groupBy(p => p.genero)                                   // nueva: agrupa por género
    .map { case (genero, lista) => (genero, lista.size) }     // cuenta por grupo
    .filter { case (_, cantidad) => cantidad >= 2 }           // vista en clase: filter
    .toList
    .sortBy { case (genero, cantidad) => (-cantidad, genero) } // nueva: mayor a menor
  println(s"combinación: $generosPopulares")
```
