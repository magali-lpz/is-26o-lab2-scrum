# Especificación funcional: Consulta del perfil escolar del alumno

## 1. Información general

- **Módulo:** Biblioteca / Gestión de alumnos
- **Historia asociada:** US-XX – Consulta de perfil escolar
- **Actor principal:** Bibliotecario

## 2. Flujo de interacción del usuario

1. El bibliotecario ingresa al sistema de biblioteca.
2. Busca al alumno por matrícula o nombre.
3. El sistema muestra el perfil escolar del alumno seleccionado.
4. Se visualizan el nombre, la carrera y el correo institucional.
5. El sistema indica si el alumno tiene libros en préstamo actualmente.

## 3. Reglas del sistema (Criterios de aceptación)

- **Datos visibles:** Se debe mostrar el nombre completo, la carrera y el correo institucional del alumno.
- **Préstamos activos:** Se debe indicar claramente si el alumno tiene libros en préstamo.
- **Información actualizada:** El estado de los préstamos debe corresponder a los registros vigentes de la biblioteca.
```
