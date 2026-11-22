# Práctica 3: Bases de Datos Orientadas a Grafos en Neo4j

**Asignatura:** Bases de Datos 2  
**Programa:** Ingeniería Informática — Facultad de Ingeniería y Ciencias Básicas  
**Universidad Autónoma de Occidente (UAO)**

---

## Descripción del Proyecto

Implementación en **Neo4j** y **Cypher** de una base de datos orientada a grafos que modela la estructura y el comportamiento de una plataforma de cursos en línea (estilo Coursera o edX)[cite: 1, 2]. El modelo permite explorar, cursar, valorar y recomendar contenidos educativos, analizando hábitos de estudio, cobertura geográfica y recomendaciones personalizadas mediante filtrado colaborativo y afinidad temática[cite: 2, 3, 4].

---

## Modelo del Grafo

El nodo central del modelo es **`Curso`**, el cual se organiza jerárquicamente en **`Modulo`** y **`Leccion`**, conectándose además con **`Categoria`**, **`Idioma`**, **`Pais`** y **`Usuario`**[cite: 1, 2].

### Nodos (7)
* **`Usuario`**: `usuarioId`, `nombre`, `edad`, `sexo` (`"M"`, `"F"`, `"Otro"` - opcional), `email`, `fechaNacimiento`[cite: 2, 5].
* **`Curso`**: `cursoId`, `titulo`, `descripcion`, `nivel` (`"Básico"`, `"Intermedio"`, `"Avanzado"`), `anioPublicacion`, `calificacionPromedio`[cite: 2, 5].
* **`Modulo`**: `moduloId`, `titulo`, `numero` (orden dentro del curso)[cite: 2, 5].
* **`Leccion`**: `leccionId`, `titulo`, `descripcion`, `duracionMin`, `numero` (orden dentro del módulo)[cite: 2, 5].
* **`Categoria`**: `codigo`, `nombre`, `descripcion`[cite: 2, 5].
* **`Idioma`**: `codigo`, `nombre`[cite: 2, 5].
* **`Pais`**: `codigo`, `nombre`[cite: 2, 5].

### Relaciones (9)
* `(:Usuario)-[:VIO {fecha, minutosReproducidos, finalizado}]->(:Leccion)`[cite: 2, 5]
* `(:Usuario)-[:LE_GUSTA {valoracion, fecha}]->(:Curso)`[cite: 2, 5]
* `(:Usuario)-[:INSCRITO_EN {fechaInicio, fechaFin, progreso, estado}]->(:Curso)`[cite: 2, 5]
* `(:Usuario)-[:RESIDE_EN]->(:Pais)`[cite: 1, 5]
* `(:Curso)-[:ESTA_COMPUESTO {orden}]->(:Modulo)`[cite: 2, 5]
* `(:Modulo)-[:CONTIENE {orden}]->(:Leccion)`[cite: 2, 5]
* `(:Curso)-[:EN_IDIOMA]->(:Idioma)`[cite: 1, 5]
* `(:Curso)-[:PERTENECE_A]->(:Categoria)`[cite: 1, 5]
* `(:Curso)-[:DISPONIBLE_EN {fechaInicio, fechaFin}]->(:Pais)`[cite: 2, 5]

---

## Estructura del Repositorio

```text
Practica-Final/
├── CargaDatos.txt          # Script Cypher completo (constraints, carga de nodos y relaciones)
├── Consultas.txt           # Solución y explicación detallada de las 7 consultas Cypher
├── Práctica Final Neo4j.pdf # Enunciado oficial de la práctica
│
├── usuarios.csv            # Datos de nodos Usuario
├── cursos.csv              # Datos de nodos Curso
├── modulos.csv             # Datos de nodos Modulo
├── lecciones.csv           # Datos de nodos Leccion
├── categorias.csv          # Datos de nodos Categoria
├── idiomas.csv             # Datos de nodos Idioma
├── paises.csv              # Datos de nodos Pais
│
├── VIO.csv                 # Relación Usuario -> Leccion
├── LE_GUSTA.csv            # Relación Usuario -> Curso
├── INSCRITO_EN.csv         # Relación Usuario -> Curso
├── RESIDE_EN.csv           # Relación Usuario -> Pais
├── ESTA_COMPUESTO.csv      # Relación Curso -> Modulo
├── CONTIENE.csv            # Relación Modulo -> Leccion
├── EN_IDIOMA.csv           # Relación Curso -> Idioma
├── PERTENECE_A.csv         # Relación Curso -> Categoria
└── DISPONIBLE_EN.csv       # Relación Curso -> Pais
```
---
## Autores

* **Juan Esteban Bermúdez Montenegro** — [@juanbermudezm-UAO](https://github.com/juanbermudezm-UAO)
* **Miguel Ángel Benavides Valencia** — [@BenavidesMA](https://github.com/BenavidesMA)
