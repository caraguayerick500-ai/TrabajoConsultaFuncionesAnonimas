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
###  FALTAA
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

```scala
case class Producto(nombre: String, categoria: String, precio: Double, stock: Int)

val productos = List(
  Producto("...", "...", 0.0, 0)
  // completa con 10 a 15 elementos
)
```

> Los equivalentes en Java y Python están en las carpetas [`java/`](java/) y [`python/`](python/).

### 3.1 Catálogo de tipos de problemas

Se documentan [4 a 7] de los siguientes tipos:

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

#### 3.1.1 Selección (`filter`)

**Situación real:** [Ejemplo concreto]

**Scala**
```scala
// Código
```

**Java**
```java
// Código con Streams
```

**Python**
```python
# Código con lambda
```

**Salida de cada versión**

| Scala | Java | Python |
|---|---|---|
| ![Scala](img/seleccion_scala.png) | ![Java](img/seleccion_java.png) | ![Python](img/seleccion_python.png) |

---

#### 3.1.2 Transformación (`map`)

**Situación real:** [...]

**Scala**
```scala
```

**Java**
```java
```

**Python**
```python
```

**Salida de cada versión**

| Scala | Java | Python |
|---|---|---|
| ![Scala](img/transformacion_scala.png) | ![Java](img/transformacion_java.png) | ![Python](img/transformacion_python.png) |

---

#### 3.1.3 Validación (`exists`, `forall`)

**Situación real:** [...]

**Scala**
```scala
```

**Java**
```java
```

**Python**
```python
```

**Salida de cada versión**

| Scala | Java | Python |
|---|---|---|
| ![Scala](img/validacion_scala.png) | ![Java](img/validacion_java.png) | ![Python](img/validacion_python.png) |

---

#### 3.1.4 Conteo (`count`)

**Situación real:** [...]

**Scala**
```scala
```

**Java**
```java
```

**Python**
```python
```

**Salida de cada versión**

| Scala | Java | Python |
|---|---|---|
| ![Scala](img/conteo_scala.png) | ![Java](img/conteo_java.png) | ![Python](img/conteo_python.png) |

---

<!-- Copia el mismo formato para Extremos (3.1.5), Aplanamiento (3.1.6) y Acumulación (3.1.7) si los documentas. Si no, elimina este comentario. -->

---

## Parte 4 - Ampliar: Cuatro operaciones nuevas.

Las operaciones elegidas son: **[operación 1]**, **[operación 2]**, **[operación 3]** y **[operación 4]**.
Código completo en [`operaciones/`](operaciones/).

### 4.1 Ficha: `[operación 1]`

| Campo | Descripción |
|---|---|
| **Qué hace** | [Una o dos líneas con tus palabras] |
| **Lambda que recibe** | [Qué recibe y qué debe devolver. Si no recibe lambda, indica con qué operación se encadena] |
| **Problema que resuelve** | [Situación real y tipo de problema de la sección 3.1, o si es un tipo nuevo] |

**Ejemplo en Scala**
```scala
// Usa la misma lista de productos de la Parte 3
```

**Salida**
```text
[Pega aquí la salida]
```

### 4.2 Ficha: `[operación 2]`

| Campo | Descripción |
|---|---|
| **Qué hace** | [...] |
| **Lambda que recibe** | [...] |
| **Problema que resuelve** | [...] |

**Ejemplo en Scala**
```scala
```

**Salida**
```text
```

### 4.3 Ficha: `[operación 3]`

| Campo | Descripción |
|---|---|
| **Qué hace** | [...] |
| **Lambda que recibe** | [...] |
| **Problema que resuelve** | [...] |

**Ejemplo en Scala**
```scala
```

**Salida**
```text
```

### 4.4 Ficha: `[operación 4]`

| Campo | Descripción |
|---|---|
| **Qué hace** | [...] |
| **Lambda que recibe** | [...] |
| **Problema que resuelve** | [...] |

**Ejemplo en Scala**
```scala
```

**Salida**
```text
```

### 4.5 Combinar operaciones

**Pregunta:** [Pregunta sobre la lista que requiera varios pasos]

**Cadena de operaciones** (dos operaciones nuevas y una vista en clase):

```scala
productos
  .operacion1(...)   // paso 1
  .operacion2(...)   // paso 2
  .operacion3(...)   // paso 3
```

**Explicación paso a paso**

| Paso | Operación | Qué hace |
|---|---|---|
| 1 | `[...]` | [...] |
| 2 | `[...]` | [...] |
| 3 | `[...]` | [...] |

**Salida**
```text
[Pega aquí la salida]
```

---

## Parte 5: Comparar y concluir

### 5.1 Scala, Java y Python frente a frente

| Criterio | Scala | Java | Python |
|---|---|---|---|
| **Sintaxis de la lambda** | [...] | [...] | [...] |
| **Cómo se declara el tipo** | [...] | [...] | [...] |
| **Operaciones con listas disponibles** | [...] | [...] | [...] |
| **Restricción del lenguaje** | [...] | [...] | [...] |
| **Legibilidad (opinión)** | [...] | [...] | [...] |

**¿En qué lenguaje fue más natural resolver los problemas?**

[Respuesta]

**¿En qué tipo de problema encontraste más diferencias entre lenguajes y por qué?**

[Respuesta con evidencia de tu propio código; enlaza la sección de la Parte 3 que corresponda]

### 5.2 Conclusión

[Uno o dos párrafos: qué importancia tienen las funciones anónimas en la solución de problemas con listas, relacionándolo con al menos uno de los casos reales de la [Parte 1](#parte-1-explorar).]

---

## Cómo ejecutar el código

### Scala
```bash
cd scala
scala NombreDelArchivo.scala
```

### Java
```bash
cd java
javac NombreDelArchivo.java
java NombreDelArchivo
```

### Python
```bash
cd python
python nombre_del_archivo.py
```

> Requisitos: [Scala x.x, JDK 17+, Python 3.x]. Ajusta los comandos según tu entorno.

---

## Estructura del repositorio

```text
.
├── README.md        # Documento principal (partes 1 a 5)
├── scala/           # Soluciones de la Parte 3
├── java/            # Soluciones de la Parte 3
├── python/          # Soluciones de la Parte 3
├── operaciones/     # 4 operaciones nuevas y combinación (Parte 4)
└── img/             # Capturas de ejecución y tablas
```

---

## Referencias

1. Netflix Technology Blog, “Python at Netflix” (2019): https://medium.com/netflix-techblog/python-at-netflix-bba45dae649e
2. TechRepublic, “How Netflix uses Python”: https://www.techrepublic.com/article/how-netflix-uses-python-streaming-giant-reveals-its-programming-language-libraries-and-frameworks/

3. Oracle. Package java.util.stream (Java SE 8). https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html
4. 

5. Documentación oficial de Scala: https://docs.scala-lang.org
6. Expresiones lambda en Java: https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html
7. Programación funcional en Python: https://docs.python.org/3/howto/functional.html
8. Winitzki, S. *The Science of Functional Programming: A Tutorial, with Examples in Scala*. https://github.com/winitzki/sofp/releases/download/v2.2/sofp.pdf
9. Herramientas de IA utilizadas: Claude (Anthropic), apoyo en la estructura del README e investigación de casos
