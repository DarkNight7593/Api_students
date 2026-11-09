# API de Gestión de Estudiantes 📚

**Proyecto académico de Backend** desarrollado con **Python, Flask y SQLite**.

Esta aplicación expone una API HTTP para consultar, registrar, actualizar y eliminar estudiantes. Es parte de mi portafolio de programación y me permite practicar el desarrollo de servicios web, rutas HTTP y persistencia de datos.

## Tecnologías utilizadas

- **Python** — lógica de la aplicación.
- **Flask** — rutas y manejo de solicitudes HTTP.
- **SQLite** — almacenamiento local de estudiantes.
- **Docker** — ejecución alternativa en un contenedor.

## Funcionalidades

- Obtener el listado de estudiantes.
- Consultar un estudiante por su ID.
- Registrar un estudiante.
- Actualizar los datos de un estudiante.
- Eliminar un estudiante.

## Estructura del repositorio

```text
Api_students/
├── app.py       # Endpoints y lógica de la API
├── db.py        # Creación inicial de la tabla students
├── Dockerfile   # Imagen para ejecutar la aplicación
└── README.md    # Documentación del proyecto
```

El archivo `students.sqlite` se genera localmente al inicializar la base de datos.

## Cómo ejecutarlo localmente

Necesitas **Python 3** y `pip`.

1. Clona el repositorio:

   ```bash
   git clone https://github.com/DarkNight7593/Api_students.git
   cd Api_students
   ```

2. Crea y activa un entorno virtual:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```

   En Windows (PowerShell), la activación es `.venv\\Scripts\\Activate.ps1`.

3. Instala Flask:

   ```bash
   pip install flask
   ```

4. **Solo la primera vez**, crea la tabla de estudiantes:

   ```bash
   python db.py
   ```

   > El script actual crea la tabla sin comprobar si ya existe. Si lo ejecutas por segunda vez sobre la misma base de datos, SQLite devolverá un error de tabla existente.

5. Inicia el servidor:

   ```bash
   python app.py
   ```

La API quedará disponible en **http://localhost:8000**.

## Endpoints

| Método | Ruta | Descripción |
| --- | --- | --- |
| `GET` | `/students` | Listar estudiantes |
| `POST` | `/students` | Registrar estudiante |
| `GET` | `/student/{id}` | Obtener estudiante por ID |
| `PUT` | `/student/{id}` | Actualizar estudiante |
| `DELETE` | `/student/{id}` | Eliminar estudiante |

### Ejemplos con cURL

Listar estudiantes:

```bash
curl http://localhost:8000/students
```

Registrar un estudiante:

```bash
curl -X POST http://localhost:8000/students \
  --data-urlencode "firstname=Ana" \
  --data-urlencode "lastname=Perez" \
  --data-urlencode "gender=F" \
  --data-urlencode "age=21"
```

Consultar un estudiante (por ejemplo, ID 1):

```bash
curl http://localhost:8000/student/1
```

Actualizarlo:

```bash
curl -X PUT http://localhost:8000/student/1 \
  --data-urlencode "firstname=Ana" \
  --data-urlencode "lastname=Perez" \
  --data-urlencode "gender=F" \
  --data-urlencode "age=22"
```

Eliminarlo:

```bash
curl -X DELETE http://localhost:8000/student/1
```

**Importante:** las operaciones `POST` y `PUT` de esta versión leen los datos como **formulario** (`request.form`), no como JSON.

## Ejecutar con Docker

Si tienes Docker instalado:

```bash
docker build -t api-students .
docker run --rm -p 8000:8000 api-students
```

Abre **http://localhost:8000/students** para probar el listado. La base de datos de este ejemplo queda dentro del contenedor; sin un volumen persistente, los cambios pueden perderse al eliminarlo.

## Mejoras pendientes

Este proyecto es **educativo** y todavía no está preparado para un entorno de producción. Algunas mejoras previstas son:

- Validación de campos y respuestas de error más consistentes.
- Soporte para cuerpos JSON en `POST` y `PUT`.
- Cierre correcto de conexiones y manejo de excepciones.
- Inicialización idempotente de la base de datos.
- Pruebas automatizadas con `pytest`.
- Documentación OpenAPI y autenticación si el caso de uso lo requiere.

## Autor

**Juan Rodolfo Inca Acuña**  
Estudiante de Ciencias de la Computación (8.º ciclo), interesado en el desarrollo Full Stack y Backend.

- [GitHub](https://github.com/DarkNight7593)
- [LinkedIn](https://www.linkedin.com/in/juan-rodolfo-inca-acu%C3%B1a-634376356/)
