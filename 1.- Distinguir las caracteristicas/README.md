
# Introducción a Bases de Datos Relacionales

## 1. ¿Qué es una Base de Datos Relacional?

Una **base de datos relacional** es un sistema que organiza la información en **tablas** relacionadas entre sí, facilitando el **almacenamiento, consulta y gestión** de datos. 

---

##  2. Características, Rol y Elementos Fundamentales

### Características:
- Estructurada en tablas con filas y columnas.
- Usa relaciones lógicas entre tablas mediante claves.
- Garantiza integridad y consistencia de los datos.
- Permite el uso de SQL para manipular los datos.

###  Rol en la organización:
- Centraliza datos de diferentes áreas (ventas, clientes, productos).
- Mejora la toma de decisiones basada en datos.
- Automatiza procesos (ej. facturación, inventario).
- Aumenta la seguridad, trazabilidad y eficiencia en la gestión de la información.

---

##  3. Componentes Básicos de una Base de Datos Relacional

| Componente          | Descripción                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **Tabla**           | Estructura principal donde se almacenan los datos (como una hoja de Excel). |
| **Registro**        | Cada fila de la tabla representa una entrada o conjunto de datos.            |
| **Campo**           | Cada columna representa un atributo o característica de los datos.           |
| **Clave primaria**  | Campo único que identifica de forma exclusiva a cada registro.               |
| **Clave foránea**   | Campo que se relaciona con la clave primaria de otra tabla.                 |

---

## 4. Gestión y Relación de Tablas

- Cada tabla almacena información específica (clientes, productos, pedidos).
- Se dividen los datos en diferentes tablas y se relacionan mediante claves.
- Esto permite consultas complejas uniendo datos relevantes de diferentes tablas.

---

## 5. Ejemplo: Tablas para creacion de una ficha medica

###  SQL para Crear Tablas

```sql
-- Tabla Especialidades
CREATE TABLE Especialidades (
    id_especialidad INT AUTO_INCREMENT PRIMARY KEY,
    nombre_especialidad VARCHAR(50) NOT NULL UNIQUE
);

-- Tabla Sexo
CREATE TABLE Sexo (
    id_sexo INT AUTO_INCREMENT PRIMARY KEY,
    descripcion VARCHAR(10) NOT NULL UNIQUE
);

-- Tabla Pacientes

CREATE TABLE Pacientes (
    id_paciente INT AUTO_INCREMENT PRIMARY KEY,
    rut VARCHAR(15) NOT NULL UNIQUE,
    nombre VARCHAR(50) NOT NULL,
    apellido VARCHAR(50) NOT NULL,
    fecha_nacimiento DATE NOT NULL,
    id_sexo INT NOT NULL,
    direccion VARCHAR(100),
    telefono VARCHAR(20),
    correo VARCHAR(100),
    FOREIGN KEY (id_sexo) REFERENCES Sexo(id_sexo)
);

-- Tabla Medicos

CREATE TABLE Medicos (
    id_medico INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL,
    apellido VARCHAR(50) NOT NULL,
    id_especialidad INT NOT NULL,
    numero_colegiado VARCHAR(30) UNIQUE,
    correo VARCHAR(100),
    telefono VARCHAR(20),
    FOREIGN KEY (id_especialidad) REFERENCES Especialidades(id_especialidad)
);

-- Tabla Ficha Medica

CREATE TABLE Fichas_Medicas (
    id_ficha INT AUTO_INCREMENT PRIMARY KEY,
    id_paciente INT NOT NULL,
    fecha_creacion DATE NOT NULL,
    motivo_consulta TEXT,
    antecedentes TEXT,
    FOREIGN KEY (id_paciente) REFERENCES Pacientes(id_paciente)
);

-- Tabla Atenciones

CREATE TABLE Atenciones (
    id_atencion INT AUTO_INCREMENT PRIMARY KEY,
    id_ficha INT NOT NULL,
    id_medico INT NOT NULL,
    fecha_atencion DATETIME NOT NULL,
    diagnostico TEXT,
    tratamiento TEXT,
    observaciones TEXT,
    FOREIGN KEY (id_ficha) REFERENCES Fichas_Medicas(id_ficha),
    FOREIGN KEY (id_medico) REFERENCES Medicos(id_medico)
);

-- Tabla Recetas

CREATE TABLE Recetas (
    id_receta INT AUTO_INCREMENT PRIMARY KEY,
    id_atencion INT NOT NULL,
    medicamento TEXT NOT NULL,
    dosis TEXT,
    frecuencia TEXT,
    duracion TEXT,
    FOREIGN KEY (id_atencion) REFERENCES Atenciones(id_atencion)
);


```
