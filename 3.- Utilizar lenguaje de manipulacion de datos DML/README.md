
## 🟢 INSERT - Insertar datos

### 1. Insertar un nuevo sexo

```sql
INSERT INTO Sexo (descripcion)
VALUES ('Masculino');
```

### 2. Insertar una especialidad médica

```sql
INSERT INTO Especialidades (nombre_especialidad)
VALUES ('Medicina General');
```

### 3. Insertar un nuevo paciente

```sql
INSERT INTO Pacientes (
    rut, nombre, apellido, fecha_nacimiento, id_sexo, direccion, telefono, correo
)
VALUES (
    '11.222.333-4', 'Juan', 'Pérez', '1990-06-15', 1, 'Av. Central 123', '987654321', 'juanperez@example.com'
);
```

### 4. Insertar un médico

```sql
INSERT INTO Medicos (
    nombre, apellido, id_especialidad, numero_colegiado, correo, telefono
)
VALUES (
    'Ana', 'González', 1, 'MG12345', 'ana.gonzalez@clinica.cl', '912345678'
);
```

### 5. Insertar una ficha médica para un paciente

```sql
INSERT INTO Fichas_Medicas (
    id_paciente, fecha_creacion, motivo_consulta, antecedentes
)
VALUES (
    1, CURDATE(), 'Dolor abdominal', 'Sin antecedentes relevantes'
);
```

---

##  UPDATE - Modificar datos

### 6. Actualizar dirección y teléfono de un paciente

```sql
UPDATE Pacientes
SET direccion = 'Nueva Dirección 456', telefono = '912000111'
WHERE rut = '11.222.333-4';
```

### 7. Cambiar la especialidad de un médico

```sql
UPDATE Medicos
SET id_especialidad = 2
WHERE numero_colegiado = 'MG12345';
```

### 8. Corregir el diagnóstico de una atención médica

```sql
UPDATE Atenciones
SET diagnostico = 'Apendicitis aguda'
WHERE id_atencion = 5;
```

---

## DELETE - Eliminar datos

### 9. Eliminar una receta asociada a una atención cancelada

```sql
DELETE FROM Recetas
WHERE id_atencion = 5;
```

### 10. Eliminar un paciente sin fichas médicas

```sql
DELETE FROM Pacientes
WHERE id_paciente = 10
  AND id_paciente NOT IN (
      SELECT id_paciente FROM Fichas_Medicas
  );
```
