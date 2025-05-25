[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/oLntvctd)

# Sistema de Gestión Académica — GitHub Classroom Assignment

Este proyecto es una API REST creada con **Kotlin**, **Spring Boot**, **Gradle** y **H2** como base de datos en memoria. Está pensada como punto de partida para una tarea de laboratorio donde los estudiantes deben aplicar relaciones entre entidades y manejo de excepciones.

---

## 📚 Instrucciones para el estudiante

Tu objetivo es completar una API REST que permita:

1. Registrar profesores y estudiantes.
2. Crear asignaturas que estén asignadas a un profesor.
3. Inscribir estudiantes en asignaturas.
4. Implementar validaciones como:
  - No permitir inscripciones duplicadas.
  - Lanzar excepciones cuando no se encuentre un profesor o estudiante.
5. Manejar los errores usando `@ControllerAdvice` y excepciones personalizadas.

### 🎯 Entregable esperado

Una API funcional que permita:

- Crear y listar profesores, estudiantes y asignaturas.
- Inscribir estudiantes mediante endpoint específico.
- Consultar la información mediante cURL o Postman.
- Pasar los tests definidos en el proyecto (`src/test/...`).

---

## 🚀 Requisitos

- Java 21
- Gradle
- IntelliJ IDEA (opcional)
- Postman o cURL para pruebas

---

## 🛠️ Cómo ejecutar

1. Clona el repositorio
2. Abre el proyecto en IntelliJ o tu IDE favorito
3. Ejecuta la clase `Application.kt`
4. La API estará disponible en `http://localhost:8080`

---

## ⚙️ Autograding (evaluación automática)

Este repositorio incluye un workflow de GitHub Actions para autograding. Cada vez que hagas push, se ejecutarán pruebas automáticas.

> **Importante:** no borres ni modifiques el archivo `.github/workflows/classroom.yml`.

---

## 🔧 Endpoints disponibles

### Profesores
- `POST /api/professors` → crear profesor
- `GET /api/professors` → listar todos

### Estudiantes
- `POST /api/students` → crear estudiante
- `GET /api/students` → listar todos

### Asignaturas
- `POST /api/subjects` → crear asignatura (`professorId` requerido)
- `GET /api/subjects` → listar todas
- `POST /api/subjects/{subjectId}/enroll/{studentId}` → inscribir estudiante

---

## 🗃️ Consultas SQL útiles

Puedes usarlas en la consola H2: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

```sql
SELECT * FROM PROFESSORS;
SELECT * FROM STUDENTS;
SELECT * FROM SUBJECTS;
SELECT * FROM SUBJECT_STUDENTS;

SELECT 
    sj.name AS subject_name,
    pr.name AS professor_name,
    st.name AS student_name,
    st.email AS student_email
FROM SUBJECTS sj
INNER JOIN PROFESSORS pr ON sj.professor_id = pr.id
INNER JOIN SUBJECT_STUDENTS ss ON sj.id = ss.subject_id
INNER JOIN STUDENTS st ON ss.student_id = st.id
WHERE sj.id = 1;

SELECT 
    sj.name AS subject_name,
    pr.name AS professor_name,
    st.name AS student_name,
    st.email AS student_email
FROM SUBJECTS sj
INNER JOIN PROFESSORS pr ON sj.professor_id = pr.id
INNER JOIN SUBJECT_STUDENTS ss ON sj.id = ss.subject_id
INNER JOIN STUDENTS st ON ss.student_id = st.id
WHERE sj.id = 2;
```

---

## 🧠 Notas

- El proyecto utiliza `@ControllerAdvice` para manejo centralizado de errores.
- Se implementaron `Mapper` y `DTOs` para separar entidades de persistencia de las respuestas.
- El archivo `README.md` y los tests servirán como referencia para completar tu entrega.

---

## 📎 Licencia

Uso académico para PUCE TEC.
