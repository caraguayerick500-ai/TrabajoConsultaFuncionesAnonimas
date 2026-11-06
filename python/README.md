```python
from dataclasses import dataclass

@dataclass
class Pelicula:
    titulo: str
    genero: str
    anio: int
    duracion: int        # minutos
    calificacion: float  # 0 a 10

peliculas = [
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
    Pelicula("La La Land", "Romance", 2016, 128, 8.0),
]

# 1. Selección: películas con calificación >= 8.5
mejores = list(filter(lambda p: p.calificacion >= 8.5, peliculas))
print("Selección:", [p.titulo for p in mejores])

# 2. Transformación: lista de títulos en mayúsculas
titulos = list(map(lambda p: p.titulo.upper(), peliculas))
print("Transformación:", titulos)

# 3. Validación: ¿alguna con calificación > 9? ¿todas posteriores a 1990?
hay_mayor_a_9 = any(p.calificacion > 9 for p in peliculas)
todas_desde_1990 = all(p.anio >= 1990 for p in peliculas)
print("Validación exists:", hay_mayor_a_9)
print("Validación forall:", todas_desde_1990)

# 4. Conteo: cuántas son de animación
cantidad = len(list(filter(lambda p: p.genero == "Animación", peliculas)))
print("Conteo:", cantidad)
```
