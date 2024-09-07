
<h1 align="center">
  <br>
  
  Desarrollo de una Lista de Tareas (To-Do List)
  <br>
</h1>

<h4 align="center">Un proyecto de gestión de tareas desarrollado utilizando MySQL, por un equipo de apasionados desarrolladores.</h4>

<p align="center">
  <a href="#características-principales">Características Principales</a> •
  <a href="#cómo-utilizar">Cómo Utilizar</a> •
  <a href="#modelo-entidad-relación">Modelo Entidad-Relación</a> •
  <a href="#creación-de-la-base-de-datos">Creación de la Base de Datos</a> •
  <a href="#operaciones-sql">Operaciones SQL</a> •
  <a href="#licencia">Licencia</a>
</p>


## Características Principales

* **Gestión de Usuarios**: Crea, lee, actualiza y elimina usuarios.
* **Gestión de Tareas**: Añade, visualiza, edita y elimina tareas.
* **Relaciones**: Un usuario puede tener múltiples tareas, pero cada tarea pertenece a un único usuario.
* **MySQL**: Base de datos robusta y escalable para gestionar los datos de la aplicación.
* **Interfaz Intuitiva**: Fácil de usar para la gestión de tareas diarias.
* **Escalabilidad**: Diseñado con un enfoque en la escalabilidad y el rendimiento de lectura.

## Cómo Utilizar

Para clonar y ejecutar esta aplicación, necesitarás [Git](https://git-scm.com) y [MySQL](https://www.mysql.com/downloads/) instalados en tu computadora. Desde tu línea de comandos:

```bash
# Clona este repositorio
$ git clone https://github.com/tuusuario/todolist

# Entra en el repositorio
$ cd todolist

# Configura la base de datos en MySQL
$ mysql -u tu_usuario -p < database/todolist.sql

# Ejecuta la aplicación (puedes usar cualquier framework o servidor web)
$ npm start
```

> **Nota**
> Asegúrate de configurar correctamente tu servidor MySQL y de importar las tablas utilizando los scripts SQL proporcionados.

## Modelo Entidad-Relación

El modelo entidad-relación (ER) para esta aplicación es sencillo pero efectivo, y está diseñado para gestionar usuarios y sus respectivas tareas. Las entidades principales son `Usuario` y `Tarea`. Un usuario puede tener múltiples tareas, y cada tarea está asociada a un solo usuario.

**Entidades y Atributos**:
- **Usuario**: 
  - `ID` (Primary Key)
  - `Nombre`
  - `Correo Electrónico`
  - `Contraseña` (almacenada de forma segura, idealmente como hash)
  
- **Tarea**: 
  - `ID` (Primary Key)
  - `Descripción`
  - `Estado` (por ejemplo: Pendiente, Completada)
  - `Fecha de Creación`
  - `Fecha de Vencimiento` (opcional)
  - `ID_Usuario` (Foreign Key): Relacionado con el Usuario que creó la tarea

El diagrama ER puede visualizarse en [Lucidchart](https://lucid.app/lucidchart/41e467aa-48c2-4697-8ca1-1e9bf6f8c79c/edit?viewport_loc=-419%2C-305%2C2846%2C1334%2C0_0&invitationId=inv_98fa727e-15d9-445d-9047-463e5995d7bb).

## Creación de la Base de Datos

### 1. Creación de la Base de Datos
```sql
CREATE DATABASE ToDoListDB;
USE ToDoListDB;
```

### 2. Creación de las Tablas

#### 2.1 Crear la tabla de Usuario:
```sql
CREATE TABLE Usuario (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Nombre VARCHAR(100) NOT NULL,
    Correo_Electronico VARCHAR(100) NOT NULL UNIQUE,
    Contraseña VARCHAR(255) NOT NULL -- Asegúrate de usar un hash seguro para las contraseñas
);
```

#### 2.2 Crear la tabla de Tarea:
```sql
CREATE TABLE Tarea (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Descripcion TEXT NOT NULL,
    Estado ENUM('Pendiente', 'Completada') DEFAULT 'Pendiente',
    Fecha_Creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    Fecha_Vencimiento DATE,
    ID_Usuario INT,
    FOREIGN KEY (ID_Usuario) REFERENCES Usuario(ID)
);
```

## Operaciones SQL

### 3.1 Crear un nuevo usuario:
```sql
INSERT INTO Usuario (Nombre, Correo_Electronico, Contraseña)
VALUES ('Juan Pérez', 'juan@example.com', 'hashed_password');
```

### 3.2 Listar todos los usuarios:
```sql
SELECT * FROM Usuario;
```

### 3.3 Modificar un usuario (por ejemplo, cambiar el nombre):
```sql
UPDATE Usuario
SET Nombre = 'Juanito Pérez'
WHERE ID = 1;
```

### 3.4 Eliminar un usuario:
```sql
DELETE FROM Usuario
WHERE ID = 1;
```

### 3.5 Crear una nueva tarea:
```sql
INSERT INTO Tarea (Descripcion, Estado, Fecha_Vencimiento, ID_Usuario)
VALUES ('Comprar leche', 'Pendiente', '2024-09-15', 1);
```

### 3.6 Listar todas las tareas de un usuario:
```sql
SELECT * FROM Tarea
WHERE ID_Usuario = 1;
```

### 3.7 Modificar una tarea (por ejemplo, marcar como completada):
```sql
UPDATE Tarea
SET Estado = 'Completada'
WHERE ID = 1;
```

### 3.8 Eliminar una tarea:
```sql
DELETE FROM Tarea
WHERE ID = 1;
```

---

### Desarrollado por:  COLOCAR USUARIO DE CADA UNO
> **Carlos Ventura** • [GitHub](https://github.com/Lion447)  
> **Daniela Bravo** • [GitHub](https://github.com/danielabravo)  
> **Roxana Marchetto** • [GitHub](https://github.com/roxymarchetto)  
> **Yesica Sofra** • [GitHub](https://github.com/Yesica1983)


### Explicación Adicional:
1. **Modelo Entidad-Relación**: Se detalla el modelo ER incluyendo los atributos y la relación entre entidades.
2. **Creación de la Base de Datos**: Se explican los comandos para crear la base de datos y las tablas necesarias en MySQL.
3. **Operaciones SQL**: Se incluyen ejemplos específicos de cómo realizar las operaciones CRUD (Crear, Leer, Actualizar, Eliminar) para usuarios y tareas.
4. **Enlaces**: Se agregan los enlaces a los perfiles de GitHub de cada integrante del equipo.

Este README ofrece una descripción completa del proyecto, cubriendo todos los aspectos esenciales desde la configuración hasta las operaciones básicas en la base de datos.
