# Especificación funcional: Módulo de registro de préstamo a domicilio

## 1. Información general

- **Módulo:** Préstamos (Célula 3)
- **Historia asociada:** US-06 - Registro de préstamo a domicilio
- **Integrantes redactores:** Ricardo Palomino Bravo, Diego Peralta Huerta, Jorge Iván Ramírez Segundo, Claudia Rodríguez Hernández

## 2. Flujo de interacción del usuario

1. El alumno llega al mostrador de la biblioteca y solicita el préstamo de un libro a casa.
2. El bibliotecario ingresa la matrícula del alumno en el sistema.
3. El sistema valida que la matrícula sea válida.
4. El sistema consulta y muestra cuántos libros tiene prestados el alumno.
5. Si el alumno cumple con el límite establecido (3 préstamos simultáneos), el bibliotecario registra el préstamo del libro.
6. El sistema calcula la fecha de devolución (7 días hábiles) y la guarda en el registro.
7. Se emite un comprobante con los ejemplares prestados y la fecha límite de devolución.
8. El sistema actualiza la información de la matrícula asociada.

## 3. Reglas del sistema (Criterios de aceptación)

- **Asociación del ejemplar:** El sistema debe asociar el identificador único de los ejemplares con la matrícula del alumno que solicita el préstamo. No se puede registrar un préstamo sin ambos datos.
- **Historial del alumno:** El alumno no debe estar penalizado en el sistema asociado con su matrícula.
- **Hora de entrega:** El sistema registra automáticamente la hora exacta en que se entrega el ejemplar.
- **Fecha límite:** El tiempo máximo de préstamo es de 7 días hábiles. Pasado ese límite, el préstamo se marca como vencido.
- **Disponibilidad:** Un ejemplar ya prestado no puede asignarse a otro alumno hasta que se registre su devolución.
- **Límite de préstamos:** Un alumno no puede tener más de 3 libros a domicilio al mismo tiempo. Si el préstamo nuevo haría que rebase ese número, el sistema lo rechaza e indica cuántos libros más puede llevarse.

## 4. Ejemplo de datos (Estructura esperada)

```json
{
  "id_matricula": "2213067888",
  "id_prestamo": "PRE-01-l",
  "id_ejemplar": "EJ-0001",
  "fecha_prestamo": "2026-10-15",
  "fecha_entrega": "2026-10-18",
  "libros_prestados": ["nombre1", "nombre2"],
  "estado": "Indispuestos_Temporalmente"
}
```
