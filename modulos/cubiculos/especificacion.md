# Especificación funcional: Cancelación y liberación anticipada de cubículo

## 1. Información general

- **Módulo:** Cubículos de estudio
- **Historia Asociada:** US-10 - Cancelación y liberación anticipada de cubículo
- **Integrante redactor:** Yadira Camila Ramírez Jiménez

---

## 2. Flujo de interacción del usuario

### Cancelación anticipada de reserva de cubículo

1. El alumno ingresa al portal de biblioteca y consulta sus reservas de cubículos.
2. Selecciona la reserva que desea cancelar.
3. El sistema verifica el tiempo restante antes del inicio de la reserva.
4. Si faltan al menos **30 minutos**, el sistema permite cancelar la reserva sin penalización.
5. El sistema registra la cancelación y libera el cubículo para que pueda ser utilizado por otros alumnos.

### Liberación anticipada del cubículo

1. El alumno consulta la sesión de cubículo que se encuentra activa.
2. Selecciona la opción **"Finalizar sesión"** antes de la hora programada.
3. El sistema solicita confirmación para finalizar anticipadamente la sesión.
4. Al confirmar, el sistema registra la hora de salida.
5. El cubículo cambia inmediatamente su estado a **"Disponible"**.

---

## 3. Reglas del sistema (Criterios de aceptación)

- **Cancelación sin penalización:** Se permite cancelar una reserva sin penalización cuando se realiza con al menos **30 minutos de anticipación**.
- **Validación de tiempo:** El sistema debe verificar la hora de inicio de la reserva antes de procesar la cancelación.
- **Usuario autorizado:** Solo el alumno asociado a la reserva puede cancelarla o finalizar anticipadamente la sesión.
- **Liberación inmediata:** Al finalizar una sesión anticipadamente, el estado del cubículo debe cambiar inmediatamente a **"Disponible"**.
- **Registro de la operación:** El sistema debe guardar la fecha y hora en que se realizó la cancelación o liberación anticipada.

---

## 4. Ejemplo de datos

La estructura de datos utilizada para esta historia se encuentra en el archivo:

**`ejemplo-datos.json`**
