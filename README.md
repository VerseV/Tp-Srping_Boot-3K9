# 🛒 API REST - Gestión de Productos (UTN Programación III)

API REST completa desarrollada con Spring Boot y Gradle para la gestión de productos de un sistema de e-commerce.

## 📋 Descripción del Proyecto

Este proyecto implementa una API RESTful que permite realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre productos, aplicando las mejores prácticas de desarrollo con Spring Boot, incluyendo:

* Arquitectura en capas (Controller, Service, Repository, Model, DTO)
* Validaciones con Bean Validation
* Manejo centralizado de excepciones
* Persistencia con Spring Data JPA y H2 Database
* Documentación interactiva con Swagger/OpenAPI

## ⚙️ Tecnologías Utilizadas

* **Java 17**
* **Spring Boot 3.5.7**
* **Spring Web** (Controladores REST)
* **Spring Data JPA** (Persistencia)
* **H2 Database** (Base de datos en memoria)
* **Lombok** (Para reducir código boilerplate)
* **Bean Validation** (Validaciones de DTOs)
* **Springdoc OpenAPI (Swagger)** (Documentación)
* **Gradle** (Gestión del proyecto y dependencias)

## 🚀 Instrucciones para Clonar y Ejecutar

### Prerrequisitos

* JDK 17 o superior.
* IDE (IntelliJ IDEA recomendado).

### Pasos para ejecutar

1.  **Clonar el repositorio**
    ```bash
    git clone [https://github.com/](https://github.com/)[TU-USUARIO]/[TU-REPOSITORIO].git
    cd [TU-REPOSITORIO]
    ```

2.  **Configuración de IntelliJ IDEA (¡Importante!)**
    Este proyecto está configurado para ejecutarse mejor con el *runner* nativo de IntelliJ. Si la aplicación no se mantiene corriendo (botón de Stop 🟥 gris), ve a:
    `File` > `Settings` > `Build, Execution, Deployment` > `Build Tools` > `Gradle`
    Y cambia la opción **"Build and run using:"** a **`IntelliJ IDEA`**.

3.  **Ejecutar la aplicación**
    Simplemente ejecuta la clase `ProductosApiApplication.java` desde tu IDE.

    O, si prefieres usar la terminal:
    ```bash
    # En Windows
    .\gradlew bootRun

    # En macOS/Linux
    ./gradlew bootRun
    ```

## 🔗 Acceso a Herramientas

Una vez que la aplicación esté corriendo, puedes acceder a:

### 1. Swagger UI (Documentación Interactiva)
Accede a la documentación para probar los endpoints:
`http://localhost:8080/swagger-ui/index.html`

### 2. Consola H2 (Base de Datos)
Para ver la base de datos en memoria:
`http://localhost:8080/h2-console`

* **JDBC URL:** `jdbc:h2:mem:productosdb`
* **Usuario:** `sa`
* **Contraseña:** (dejar vacío)

## 🗺️ Endpoints de la API

| Método | Ruta | Descripción |
| :--- | :--- | :--- |
| `GET` | `/api/productos` | Listar todos los productos |
| `GET` | `/api/productos/{id}` | Obtener un producto por ID |
| `GET` | `/api/productos/categoria/{categoria}` | Filtrar productos por categoría |
| `POST` | `/api/productos` | Crear un nuevo producto |
| `PUT` | `/api/productos/{id}` | Actualizar un producto completo |
| `PATCH`| `/api/productos/{id}/stock` | Actualizar solo el stock |
| `DELETE`| `/api/productos/{id}` | Eliminar un producto |

**Categorías disponibles:** `ELECTRONICA`, `ROPA`, `ALIMENTOS`, `HOGAR`, `DEPORTES`.

---

## 📸 Capturas de Pantalla de Pruebas

Capturas de las pruebas realizadas, como lo solicita el TP.

### 1. Swagger UI - Documentación Completa

![Swagger UI](https://github.com/user-attachments/assets/21168b15-dd43-4a0d-8a80-7a062b4f7c75)

### 2. POST - Crear Producto (201 Created)
(Prueba 1: Creación de un producto con código 201)

![Prueba 1](https://github.com/user-attachments/assets/31d8c0b7-9663-4147-98c1-856060f8b179)


### 3. GET - Listar Productos
(Prueba 3: Listado de los productos creados con código 200)

![Prueba 3](https://github.com/user-attachments/assets/1b6a4132-aef2-45b2-b416-b9fff238bab4)

### 4. Error 404 - Producto No Encontrado
(Prueba 6: Intento de buscar un producto con un ID inexistente, ej: 999)

![Prueba 6](https://github.com/user-attachments/assets/d5028236-a929-4320-90d7-11055866fc3a)

### 5. Error 400 - Validación
(Prueba 7 u 8: Intento de crear un producto con nombre vacío o precio negativo)

![Prueba 7](https://github.com/user-attachments/assets/e5dcbe95-00ba-4dcd-8a66-05394194a201)
![Prueba 8](https://github.com/user-attachments/assets/8e970431-fdbc-4576-a7c0-0dbb4e53ede6)

### 6. H2 Console - Datos Persistidos
(Prueba 12: Muestra de la tabla `PRODUCTO` después de realizar las operaciones)

![Prueba 12](https://github.com/user-attachments/assets/4af4ac96-bd35-4e60-9378-bd652e62426a)

---

## 💭 Conclusiones Personales

Este trabajo práctico fue una excelente consolidación de los conceptos de desarrollo backend vistos en la carrera. La implementación de una arquitectura en capas (controlador, servicio, repositorio) y el uso de DTOs para el desacoplamiento fueron puntos clave.

Sin embargo, el mayor desafío no estuvo en la lógica de Java, sino en la configuración del entorno de desarrollo. La depuración de la aplicación me enseñó lecciones fundamentales:

1.  **Configuración del IDE vs. Build Tool:** El problema más difícil de diagnosticar fue la configuración de ejecución de IntelliJ. Descubrir que la aplicación compilaba con Gradle pero no se ejecutaba (porque IntelliJ delegaba el *run* a Gradle y este terminaba la tarea) fue clave. Cambiar la ejecución a `IntelliJ IDEA` resolvió el problema base de que el servidor no se levantaba.
2.  **Conflictos de Dependencias y Startup:** El segundo gran desafío fue el *crash* silencioso de la aplicación. Identificar que `springdoc` (Swagger) fallaba al intentar analizar el `Enum Categoria` como `@PathVariable` me obligó a investigar cómo Spring maneja la conversión de tipos, implementando una solución robusta con un `Converter` personalizado en `WebConfig.java`.
3.  **Diagnóstico del Entorno:** Finalmente, el error `Port 8080 was already in use` fue un recordatorio práctico de la importancia de gestionar los procesos y puertos en el entorno de desarrollo.

Este TP fue valioso porque demostró que el trabajo de un ingeniero de sistemas no es solo escribir código que funcione, sino también entender, configurar y depurar la compleja cadena de herramientas, dependencias y configuraciones del entorno que lo hacen posible.

## 👤 Autor

**Adriel Leonel Espejo Benitez**
**Legajo: 47664**
*Tecnicatura Universitaria en Programación - UTN (2025)*
