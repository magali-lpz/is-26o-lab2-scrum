# Especificación funcional: Módulo de préstamo de libros en sala

## 1. Información general

- **Módulo:** Préstamos en Sala (Célula 3)
- **Historia asociada:** US-05 - Registro de préstamo de libro en sala
- **Integrantes redactores:** Ricardo Palomino Bravo, Diego Peralta Huerta, Jorge Iván Ramírez Segundo, Claudia Rodríguez Hernández

## 2. Flujo de interacción del usuario

1. El alumno llega al mostrador de la biblioteca y solicita un libro para consulta en sala.
2. El bibliotecario ingresa la matrícula del alumno en el sistema.
3. El sistema valida que la matrícula sea válida.
4. El bibliotecario ingresa el identificador del libro a prestar.
5. El sistema guarda la información de la matrícula asociada y el libro prestado.
6. El sistema calcula la hora límite de consulta (3 horas después de la entrega) y emite un comprobante de préstamo.
7. El bibliotecario le entrega al alumno el libro.

## 3. Reglas del sistema (Criterios de aceptación)

- **Asociación del ejemplar:** El sistema debe asociar el identificador único del ejemplar con la matrícula del alumno que solicita la consulta. No se puede registrar un préstamo sin ambos datos.
- **Hora de entrega:** El sistema registra automáticamente la hora exacta en que se entrega el ejemplar.
- **Tiempo límite:** El tiempo máximo de consulta es de 3 horas. Pasado ese límite, el préstamo se marca como vencido.
- **Disponibilidad:** Un ejemplar ya prestado en sala no puede asignarse a otro alumno hasta que se registre su devolución.

## 4. Ejemplo de datos (Estructura esperada)

```json
{
  "id_matricula": "2213067888",
  "id_prestamo": "PRE-01-l",
  "id_ejemplar": "EJ-0001",
  "fecha": "2026-10-15",
  "hora_entrega": "14:00",
  "hora_limite": "17:00",
  "estado": "EN_CONSULTA"
}
```
