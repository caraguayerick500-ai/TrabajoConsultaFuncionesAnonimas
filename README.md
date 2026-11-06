<div align="center">

# Trabajo de Consulta: Funciones Anónimas

**Programación Funcional · Scala • Java • Python**

</div>

| | |
|---|---|
| **Estudiante** | Erick Xavier Caraguay Banegas |
| **Institución** | Universidad Técnica Particular de Loja (UTPL) |
| **Carrera** | Ciencias de la Computación |
| **Materia** | Programación Funcional |
| **Docente** | Ing. Luis Quiñones |
| **Fecha** | 06/11/2026 |
| **Entrega** | Semana 5 |



---

## Parte 1 - Explorar: La programación funcional en el mundo real.

### Caso 1: Netflix (pandas)

| Aspecto | Descripción |
|---|---|
| **Problema que resuelve** | Según el blog técnico de Netflix, el equipo CORE usa librerías estadísticas de Python, entre ellas pandas, para automatizar el análisis de miles de señales relacionadas cuando sus sistemas de alerta detectan un problema. |
| **Lenguaje o herramienta** | Python |
| **Ventaja del enfoque funcional** | Analizar muchos datos rápido y con poco código, sin armar herramientas desde cero. |
| **Fuente consultada** | Netflix Technology Blog, “Python at Netflix”, y TechRepublic, “How Netflix uses Python” |

### Caso 2: Streams de Java

| Aspecto | Descripción |
|---|---|
| **Problema que resuelve** | Procesar colecciones de datos con operaciones tipo filtrar, transformar y reducir, sin escribir ciclos a mano. Es una API oficial de Java para operaciones de estilo funcional sobre flujos de elementos, como transformaciones map-reduce sobre colecciones. |
| **Lenguaje o herramienta** | Java |
| **Ventaja del enfoque funcional** | La mayoría de las operaciones de un stream reciben parámetros que describen un comportamiento, y suelen ser lambdas o referencias a métodos. Además, el procesamiento es perezoso, y la documentación explica que filtrar, mapear y sumar se pueden fusionar en una sola pasada sobre los datos. |
| **Fuente consultada** | Documentación oficial de Oracle, “Package java.util.stream” |

### Fragmento de código real (opcional)

Fuente: https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html

```java
int sum = widgets.stream()
                 .filter(b -> b.getColor() == RED)   // lambda: selecciona los rojos
                 .mapToInt(b -> b.getWeight())       // lambda: extrae el peso
                 .sum();                             // reduce: suma los pesos
```

**Qué hace:** según la misma documentación, filtra los elementos rojos y suma sus pesos.

---

## Parte 2 - Entender: ¿Qué es una función anónima?

### 2.1 ¿Qué es una función anónima y de dónde viene el nombre *lambda*?

Una función anónima es una función que se escribe directamente donde se necesita, sin darle un nombre. Se usa cuando la lógica es corta y solo se necesita en un lugar.

El nombre *lambda* viene del cálculo lambda (λ), un modelo matemático de funciones creado por Alonzo Church en la década de 1930. De ahí lo tomaron los lenguajes funcionales y, más tarde, Python (lambda) y Java (expresiones lambda).

```scala
// Ejemplo breve
val doble = (x: Int) => x * 2
println(doble(5))   // 10
```

### 2.2 ¿En qué se diferencia de una función nombrada?

La lógica es la misma. La nombrada se declara aparte con un nombre y se puede reutilizar, en cambio la anónima se escribe en el mismo sitio donde se usa.

```scala
val numeros = List(1, 2, 3, 4, 5, 6)

// Función nombrada
def esPar(n: Int): Boolean = n % 2 == 0
println(numeros.filter(esPar))          // List(2, 4, 6)

// Misma lógica con función anónima
println(numeros.filter(n => n % 2 == 0))  // List(2, 4, 6)
```

| Función nombrada | Función anónima |
|---|---|
| Se declara con `def` y un nombre | No tiene nombre |
| Se puede reutilizar en varios lugares | Se escribe donde se usa |
| Conviene si la lógica es larga o repetida | Conviene si es corta y de un solo uso |


### 2.3 ¿Qué significa que las funciones sean ciudadanos de primera clase?

Significa que una función se trata como cualquier otro valor: se puede guardar en una variable, pasar como argumento y devolver como resultado.

Por eso se puede pasar una lambda a `map` o `filter`: estas operaciones reciben una función como parámetro y la aplican a cada elemento de la lista.

```scala
// 1. Una función guardada en una variable
val triple = (x: Int) => x * 3

// 2. Esa función pasada como argumento a map
println(List(1, 2, 3).map(triple))        // List(3, 6, 9)

// 3. Lo mismo, escribiendo la lambda directamente dentro de map
println(List(1, 2, 3).map(x => x * 3))    // List(3, 6, 9)
```

### 2.4 ¿Qué es un closure?

Un closure es una función anónima que usa una variable definida fuera de ella. La función "recuerda" esa variable.

```scala
val minimo = 3   // variable definida fuera de la lambda

// La lambda usa 'minimo', que no es su parámetro
println(List(1, 2, 3, 4, 5).filter(n => n > minimo))   // List(4, 5)
```
---

## Parte 3 - Aplicar: ¿En qué problemas sirven las funciones anónimas?

### Lista de datos utilizada

En todos los ejemplos se usa la misma lista de 12 peliculas:

| Título | Género | Año | Duración | Calificación |
|---|---|---|---|---|
| El Padrino | Drama | 1972 | 175 | 9.2 |
| Parásitos | Suspenso | 2019 | 132 | 8.5 |
| Interestelar | Ciencia ficción | 2014 | 169 | 8.7 |
| Gladiador | Acción | 2000 | 155 | 8.5 |
| Toy Story | Animación | 1995 | 81 | 8.3 |
| Matrix | Ciencia ficción | 1999 | 136 | 8.7 |
| Coco | Animación | 2017 | 105 | 8.4 |
| Titanic | Romance | 1997 | 195 | 7.9 |
| Inception | Ciencia ficción | 2010 | 148 | 8.8 |
| Shrek | Animación | 2001 | 90 | 7.9 |
| Joker | Drama | 2019 | 122 | 8.4 |
| La La Land | Romance | 2016 | 128 | 8.0 |


### 3.1 Catálogo de tipos de problemas

Se documentan 4 a 7 de los siguientes tipos:

| Tipo de problema | Pregunta que responde | Operaciones típicas |
|---|---|---|
| Selección | ¿Qué elementos cumplen una condición? | `filter` |
| Transformación | ¿Cómo convierto cada elemento en otro valor? | `map` |
| Validación | ¿Existe alguno?, ¿todos cumplen? | `exists`, `forall` |
| Conteo | ¿Cuántos cumplen una condición? | `count` |
| Extremos | ¿Cuál es el mejor o el peor según un criterio? | `maxBy`, `minBy` |
| Aplanamiento | ¿Cómo junto los resultados de cada elemento? | `flatMap` |
| Acumulación | ¿Qué valor resume la lista? ¿Cómo evoluciona? | `foldLeft`, `scanLeft` |

---

### Lista de datos utilizada en Scala, Python y Java

**Scala**
```scala
case class Pelicula(titulo: String, genero: String, anio: Int, duracion: Int, calificacion: Double)
```

**Java**
```java
record Pelicula(String titulo, String genero, int anio, int duracion, double calificacion) {}
```

**Python**
```python
@dataclass
class Pelicula:
    titulo: str
    genero: str
    anio: int
    duracion: int
    calificacion: float
```

#### 3.1.1 Selección (`filter`)

**Situación real:** una plataforma de streaming quiere mostrar en su página principal solo las películas mejor valoradas (calificación de 8.5 o más).

**Scala**
```scala
val mejores = peliculas.filter(p => p.calificacion >= 8.5).map(_.titulo)
```

**Java**
```java
List<String> mejores = peliculas.stream()
    .filter(p -> p.calificacion() >= 8.5)
    .map(Pelicula::titulo)
    .collect(Collectors.toList());
```

**Python**
```python
mejores = list(filter(lambda p: p.calificacion >= 8.5, peliculas))
print([p.titulo for p in mejores])
```

#### 3.1.2 Transformación (`map`)

**Situación real:** el catálogo muestra los títulos en mayúsculas en los banners de la aplicación, por lo que hay que convertir cada título.

**Scala**
```scala
val titulos = peliculas.map(p => p.titulo.toUpperCase)
```

**Java**
```java
List<String> titulos = peliculas.stream()
    .map(p -> p.titulo().toUpperCase())
    .collect(Collectors.toList());
```

**Python**
```python
titulos = list(map(lambda p: p.titulo.upper(), peliculas))
```

#### 3.1.3 Validación (`exists`, `forall`)

**Situación real:** antes de publicar una promoción, el equipo de contenido necesita saber si existe alguna película con calificación mayor a 9 y si todas son posteriores a 1990.


**Scala**
```scala
val hayMayorA9 = peliculas.exists(p => p.calificacion > 9)
val todasDesde1990 = peliculas.forall(p => p.anio >= 1990)
```

**Java**
```java
boolean hayMayorA9 = peliculas.stream().anyMatch(p -> p.calificacion() > 9);
boolean todasDesde1990 = peliculas.stream().allMatch(p -> p.anio() >= 1990);
```

**Python**
```python
hay_mayor_a_9 = any(p.calificacion > 9 for p in peliculas)
todas_desde_1990 = all(p.anio >= 1990 for p in peliculas)
```

#### 3.1.4 Conteo (`count`)

**Situación real:** el equipo de marketing necesita saber cuántas películas de animación hay en el catálogo para preparar una sección familiar.

**Scala**
```scala
val cantidad = peliculas.count(p => p.genero == "Animación")
```

**Java**
```java
long cantidad = peliculas.stream()
    .filter(p -> p.genero().equals("Animación"))
    .count();
```

**Python**
```python
cantidad = len(list(filter(lambda p: p.genero == "Animación", peliculas)))
```

## Parte 4 - Ampliar: Cuatro operaciones nuevas.

Las operaciones elegidas son **`sortBy`**, **`groupBy`**, **`find`** y **`partition`**. Todas se prueban con la misma lista de películas de la Parte 3.

### 4.1 Ficha: `sortBy`

| Campo | Descripción |
|---|---|
| **Qué hace** | Ordena la lista de menor a mayor según un valor que se calcula de cada elemento. |
| **Lambda que recibe** | Recibe un elemento y devuelve el valor por el que se ordena (un número, un texto, etc.). No devuelve `Boolean`. |
| **Problema que resuelve** | Una plataforma quiere mostrar las películas de la más corta a la más larga. Es un tipo de problema nuevo de ordenamiento, que no está en la tabla de la sección 3.1. |

**Ejemplo en Scala**
```scala
val porDuracion = peliculas.sortBy(p => p.duracion).map(p => (p.titulo, p.duracion))
```

**Salida**
```text
List((Toy Story,81), (Shrek,90), (Coco,105), (Joker,122), (La La Land,128), (Parásitos,132), (Matrix,136), (Inception,148), (Gladiador,155), (Interestelar,169), (El Padrino,175), (Titanic,195))
```

Para ordenar de mayor a menor se puede devolver el valor negativo: `sortBy(p => -p.duracion)`.

### 4.2 Ficha: `groupBy`

| Campo | Descripción |
|---|---|
| **Qué hace** | Reúne los elementos en grupos según una clave. Devuelve un `Map` donde cada clave apunta a la lista de elementos que le corresponden. |
| **Lambda que recibe** | Recibe un elemento y devuelve la clave del grupo (aquí, el género). |
| **Problema que resuelve** | El equipo de marketing quiere saber cuántas películas hay de cada género. Es un tipo de problema nuevo de agrupación. |

**Ejemplo en Scala**
```scala
val porGenero = peliculas.groupBy(p => p.genero)
val cantidadPorGenero = porGenero
  .map { case (genero, lista) => (genero, lista.size) }
  .toList
  .sortBy(_._1)
```

**Salida**
```text
List((Acción,1), (Animación,3), (Ciencia ficción,3), (Drama,2), (Romance,2), (Suspenso,1))
```

El `Map` que devuelve `groupBy` no garantiza el orden de sus claves. Por eso se pasa a lista y se ordena por nombre (con `sortBy`) para que la salida sea siempre la misma.

### 4.3 Ficha: `find`

| Campo | Descripción |
|---|---|
| **Qué hace** | Devuelve la primera película que cumple una condición. Como puede no haber ninguna, el resultado es `Some(elemento)` o `None`. |
| **Lambda que recibe** | Recibe un elemento y devuelve un `Boolean`, como `filter`. |
| **Problema que resuelve** | Se necesita encontrar la primera película de romance del catálogo para recomendarla. Se parece al tipo **Selección** (`filter`), con la diferencia de que devuelve solo el primer resultado y no una lista. |

**Ejemplo en Scala**
```scala
val primeraRomance = peliculas.find(p => p.genero == "Romance")
val sinResultado = peliculas.find(p => p.calificacion > 9.5)
```

**Salida**
```text
Some(Pelicula(Titanic,Romance,1997,195,7.9))
None
```

### 4.4 Ficha: `partition`

| Campo | Descripción |
|---|---|
| **Qué hace** | Divide la lista en dos: los elementos que cumplen la condición y los que no, en una sola pasada. |
| **Lambda que recibe** | Recibe un elemento y devuelve el elemento clasificado. El resultado es una tupla `(cumplen, noCumplen)`. |
| **Problema que resuelve** | Separar las películas largas (140 minutos o más) de las cortas para armar dos secciones. Se parece al tipo **Selección** (`filter`), pero conserva también los elementos que no cumplen. |

**Ejemplo en Scala**
```scala
val (largas, cortas) = peliculas.partition(p => p.duracion >= 140)
```

**Salida**
```text
largas: List(El Padrino, Interestelar, Gladiador, Titanic, Inception)
cortas: List(Parásitos, Toy Story, Matrix, Coco, Shrek, Joker, La La Land)
```

### 4.5 Combinar operaciones

**Pregunta:** ¿Qué géneros tienen 2 o más películas en el catálogo, ordenados de mayor a menor cantidad?

**Cadena de operaciones** (dos nuevas: `groupBy` y `sortBy`; una vista en clase: `filter`):

```scala
val generosPopulares = peliculas
  .groupBy(p => p.genero)                                    // nueva: agrupa por género
  .map { case (genero, lista) => (genero, lista.size) }      // cuenta cuántas hay en cada grupo
  .filter { case (_, cantidad) => cantidad >= 2 }            // vista en clase: se queda con 2 o más
  .toList
  .sortBy { case (genero, cantidad) => (-cantidad, genero) } // nueva: mayor a menor cantidad
```

**Explicación paso a paso**

| Paso | Operación | Qué hace |
|---|---|---|
| 1 | `groupBy` | Separa las 12 películas en 6 grupos, uno por género. |
| 2 | `map` | Reemplaza cada grupo por el par `(género, cantidad)`. |
| 3 | `filter` | Descarta los géneros con una sola película (Acción y Suspenso). |
| 4 | `toList` | Pasa el `Map` a lista, para poder ordenarla. |
| 5 | `sortBy` | Ordena por cantidad de mayor a menor; si empatan, por nombre del género. |

**Salida**
```text
List((Animación,3), (Ciencia ficción,3), (Drama,2), (Romance,2))
```
---

## Parte 5: Comparar y concluir

### 5.1 Scala, Java y Python frente a frente

| Criterio | Scala | Java | Python |
|---|---|---|---|
| **Sintaxis de la lambda** | Muy precisa usa flechas (x => x.precio > 10) o  (_.precio > 10). | Utiliza una flecha con sintaxis tipada (p -> p.getPrecio() > 10). | Emplea la palabra clave explícita (lambda x: x.precio > 10). |
| **Cómo se declara el tipo** | Mediante inferencia de tipos automática del compilador (ej. (x: Int) es opcional si el contexto lo deduce). | El compilador deduce el tipo según la interfaz funcional del contexto (Stream) | No se declaran tipos. Al ser de tipado dinámico, los parámetros de una lambda no llevan definición de tipo |
| **Operaciones con listas disponibles** | Nativas, amplias y muy completas directamente en las colecciones (map, filter, groupBy, etc.). | stream().filter(), collect(), etc.). | Disponibles mediante funciones integradas (map, filter) o la librería estándar (functools). |
| **Restricción del lenguaje** | Requiere tipado estricto, aunque es muy fácil de aprender. | Las lambdas están limitadas a interfaces funcionales de un solo método abstracto | Las funciones lambda están estrictamente limitadas a una sola expresión (no admiten bloques de código multilínea). |
| **Legibilidad (opinión)** | Mucho más fácil, limpia y expresiva gracias a su diseño funcional nativo y su sintaxis minimalista. | Moderada; aunque los Streams mejoran el código, sigue siendo más largo el programar por las reglas de Java. | Es fácil en casos simples, pero puede volverse compleja o menos limpia al anidar múltiples operaciones funcionales. |

**¿En qué lenguaje fue más natural resolver los problemas?**

Fue Scala. Las operaciones sobre listas y el uso de funciones anónimas fluyen de manera natural, con un código muy limpio y sin necesidad de escribir código repetitivo

**¿En qué tipo de problema encontraste más diferencias entre lenguajes y por qué?**

Las mayores diferencias se encontraron en los problemas de acumulación y reducción (foldLeft/reduce) y agrupación (groupBy).

Por qué, mientras que en Scala y Python estas operaciones se resuelven de forma directa y compacta con métodos nativos o funciones integradas, en Java se requiere utilizar la API de Streams junto con recolectores específicos (Collectors.groupingBy o acumuladores de reduce), lo que vuelve la sintaxis considerablemente más larga y estructurada, lo que la hace difícil de comprender

### 5.2 Conclusión

Las funciones anónimas constituyen una pieza fundamental en la programación moderna al permitir tratar el comportamiento y la lógica como un dato manipulable dentro de las operaciones con listas y estructuras de datos. Este enfoque cambia el paradigma de una programación imperativa hacia una declarativa, donde el foco se centra en qué transformar en lugar de cómo iterar manualmente cada elemento. Tal como se demuestra en el caso real de Netflix, su equipo CORE utiliza el ecosistema funcional de Python con librerías como pandas para automatizar la evaluación de miles de señales cuando sus sistemas de alerta detectan un fallo. En este tipo de escenarios, el uso de funciones anónimas y transformaciones declarativas permite procesar grandes volúmenes de datos de forma ágil y con un volumen mínimo de código, evitando la necesidad de construir herramientas complejas desde cero. En definitiva, la adopción de estas operaciones promueve la creación de sistemas más concisos, mantenibles y expresivos, reduciendo errores comunes de estado mutable y optimizando la resolución de problemas en entornos de producción a gran escala.

---


## Estructura del repositorio

```text
.
├── README.md        # Documento principal (partes 1 a 5)
├── scala/           # Soluciones de la Parte 3
├── java/            # Soluciones de la Parte 3
├── python/          # Soluciones de la Parte 3
├── operaciones/     # 4 operaciones nuevas y combinación (Parte 4)
└── img/             # Capturas de ejecución
```

---

## Referencias

1. Netflix Technology Blog, “Python at Netflix” (2019): https://medium.com/netflix-techblog/python-at-netflix-bba45dae649e
2. TechRepublic, “How Netflix uses Python”: https://www.techrepublic.com/article/how-netflix-uses-python-streaming-giant-reveals-its-programming-language-libraries-and-frameworks/
3. Oracle. Package java.util.stream (Java SE 8). https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html
4. O’Connor, J. J. y Robertson, E. F. Alonzo Church. MacTutor History of Mathematics Archive, Universidad de St Andrews. https://mathshistory.st-andrews.ac.uk/~history/Biographies/Church.html
5. Documentación oficial de Scala: https://docs.scala-lang.org
6. Programación funcional en Python: https://docs.python.org/3/howto/functional.html
7. Winitzki, S. *The Science of Functional Programming: A Tutorial, with Examples in Scala*. https://github.com/winitzki/sofp/releases/download/v2.2/sofp.pdf
8. Herramientas de IA utilizadas: Claude (Anthropic), apoyo en la estructura del README e investigación de casos, Gemini: para ayuda en la redacción
