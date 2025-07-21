
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

## 5. Ejemplo: Tabla Clientes y Pedidos

###  SQL para Crear Tablas

```sql
-- Tabla de Clientes
CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    correo VARCHAR(100)
);

-- Tabla de Pedidos
CREATE TABLE pedidos (
    id_pedido INT PRIMARY KEY,
    id_cliente INT,
    fecha_pedido DATE,
    estado VARCHAR(20),
    FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);
```
