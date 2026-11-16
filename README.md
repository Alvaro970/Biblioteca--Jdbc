[README.md](https://github.com/user-attachments/files/34929006/README.md)
# Biblioteca JDBC

Aplicación web para gestionar una biblioteca: un CRUD de **libros** y **autores** con filtros de búsqueda. El acceso a datos se hace directamente con **JDBC** (sin JPA/Hibernate), y la interfaz se renderiza en el servidor con Thymeleaf.

## Qué hace

- **Libros**: listar, crear, editar y borrar (se identifican por ISBN).
- **Autores**: listar, crear, editar y borrar. Al borrar un autor se borran también sus libros (`ON DELETE CASCADE`).
- **Filtros** en el listado de libros: por autor y por rango de años de publicación (todos opcionales).
- **Validación** de formularios: ISBN de 13 dígitos, título obligatorio (máx. 150), autor obligatorio y fecha de publicación no futura. Si el ISBN ya existe, se avisa junto al campo sin perder los datos.
- **Gestión de errores centralizada**: páginas de error propias para recursos no encontrados (404) y fallos de base de datos.
- Datos de ejemplo precargados (autores y libros de literatura en español).

## Tecnologías

Java 21 · Spring Boot · Spring JDBC · Thymeleaf · Bean Validation · H2 (en memoria) · Bootstrap · Lombok · Maven

## Estructura

```
src/main/java/es/daw/bibliotecajdbc
├── controller   # LibroController, AutorController (MVC)
├── service      # lógica de negocio
├── repository   # interfaces + implementaciones JDBC
├── model        # entidades (Libro, Autor)
├── dto          # datos entre vista y controlador (+ filtros)
├── mapper       # conversión modelo <-> DTO
├── exception    # excepciones propias y GlobalExceptionHandler
└── config       # configuración web
src/main/resources
├── schema.sql / data.sql   # tablas y datos de ejemplo
├── templates               # vistas Thymeleaf
└── static                  # CSS y Bootstrap
```

## Cómo ejecutarlo

Requisitos: JDK 21.

```bash
git clone https://github.com/Alvaro970/Biblioteca--Jdbc.git
cd Biblioteca--Jdbc
./mvnw spring-boot:run        # en Windows: mvnw.cmd spring-boot:run
```

Después abre <http://localhost:8080>.

La base de datos H2 es en memoria: se crea con `schema.sql` y `data.sql` al arrancar y se reinicia cada vez. Puedes consultarla en <http://localhost:8080/h2-console> con la URL `jdbc:h2:mem:bibliotecadb`, usuario `sa` y contraseña vacía.

## Autor

Álvaro Escribano Gómez · [GitHub](https://github.com/Alvaro970)
