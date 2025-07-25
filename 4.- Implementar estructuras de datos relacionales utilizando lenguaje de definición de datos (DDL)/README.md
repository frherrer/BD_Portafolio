## 1. Crear tablas relacionadas

```sql
-- Tabla: Laboratorios clínicos
CREATE TABLE Laboratorios (
    id_laboratorio INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    direccion VARCHAR(150),
    telefono VARCHAR(20)
);

-- Tabla: Resultados de exámenes de pacientes
CREATE TABLE Resultados_Examenes (
    id_resultado INT AUTO_INCREMENT PRIMARY KEY,
    id_laboratorio INT NOT NULL,
    id_paciente INT NOT NULL,
    tipo_examen VARCHAR(100),
    resultado TEXT,
    fecha_examen DATE,
    FOREIGN KEY (id_laboratorio) REFERENCES Laboratorios(id_laboratorio)
);
```

## 2. Modificar tablas (ALTER TABLE)

```sql
-- Cambiar el tipo de dato del campo 'telefono' para permitir valores más largos
ALTER TABLE Laboratorios
MODIFY telefono VARCHAR(30);

-- Agregar una columna para el correo electrónico del laboratorio
ALTER TABLE Laboratorios
ADD correo VARCHAR(100);

-- Cambiar el nombre de la columna 'tipo_examen' por 'nombre_examen'
ALTER TABLE Resultados_Examenes
CHANGE tipo_examen nombre_examen VARCHAR(120);

-- Agregar restricción para que la fecha del examen no sea nula
ALTER TABLE Resultados_Examenes
MODIFY fecha_examen DATE NOT NULL;
```