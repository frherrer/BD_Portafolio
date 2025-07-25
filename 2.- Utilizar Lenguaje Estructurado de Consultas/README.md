## Consultas SQL - Extracción de Información

### 1. Listado de pacientes con su sexo

```sql
SELECT p.nombre, p.apellido, s.descripcion AS sexo
FROM Pacientes p
JOIN Sexo s ON p.id_sexo = s.id_sexo;
```

### 2. Fichas médicas de un paciente por RUT

```sql
SELECT f.id_ficha, f.fecha_creacion, f.motivo_consulta
FROM Fichas_Medicas f
JOIN Pacientes p ON f.id_paciente = p.id_paciente
WHERE p.rut = '12.345.678-9';
```

### 3. Última atención realizada por paciente

```sql
SELECT p.nombre, p.apellido, a.fecha_atencion, a.diagnostico
FROM Atenciones a
JOIN Fichas_Medicas f ON a.id_ficha = f.id_ficha
JOIN Pacientes p ON f.id_paciente = p.id_paciente
WHERE a.fecha_atencion = (
    SELECT MAX(a2.fecha_atencion)
    FROM Atenciones a2
    WHERE a2.id_ficha = f.id_ficha
);
```

### 4. Cantidad de atenciones por médico

```sql
SELECT m.nombre, m.apellido, e.nombre_especialidad, COUNT(*) AS total_atenciones
FROM Atenciones a
JOIN Medicos m ON a.id_medico = m.id_medico
JOIN Especialidades e ON m.id_especialidad = e.id_especialidad
GROUP BY m.id_medico;
```

### 5. Medicamentos recetados en una atención

```sql
SELECT medicamento, dosis, frecuencia, duracion
FROM Recetas
WHERE id_atencion = 101;
```

### 6. Pacientes atendidos por especialidad

```sql
SELECT DISTINCT p.nombre, p.apellido, e.nombre_especialidad
FROM Atenciones a
JOIN Fichas_Medicas f ON a.id_ficha = f.id_ficha
JOIN Pacientes p ON f.id_paciente = p.id_paciente
JOIN Medicos m ON a.id_medico = m.id_medico
JOIN Especialidades e ON m.id_especialidad = e.id_especialidad
WHERE e.nombre_especialidad = 'Pediatría';
```

### 7. Total de recetas emitidas por médico

```sql
SELECT m.nombre, m.apellido, COUNT(r.id_receta) AS total_recetas
FROM Recetas r
JOIN Atenciones a ON r.id_atencion = a.id_atencion
JOIN Medicos m ON a.id_medico = m.id_medico
GROUP BY m.id_medico;
```

### 8. Pacientes sin fichas médicas

```sql
SELECT p.nombre, p.apellido
FROM Pacientes p
LEFT JOIN Fichas_Medicas f ON p.id_paciente = f.id_paciente
WHERE f.id_ficha IS NULL;
```

### 9. Atenciones entre fechas

```sql
SELECT p.nombre AS paciente, m.nombre AS medico, a.fecha_atencion, a.diagnostico
FROM Atenciones a
JOIN Fichas_Medicas f ON a.id_ficha = f.id_ficha
JOIN Pacientes p ON f.id_paciente = p.id_paciente
JOIN Medicos m ON a.id_medico = m.id_medico
WHERE a.fecha_atencion BETWEEN '2025-01-01' AND '2025-12-31';
```

### 10. Cantidad de pacientes por sexo

```sql
SELECT s.descripcion AS sexo, COUNT(*) AS total
FROM Pacientes p
JOIN Sexo s ON p.id_sexo = s.id_sexo
GROUP BY s.descripcion;
```