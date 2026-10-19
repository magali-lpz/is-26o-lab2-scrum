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
- 

---

## 4. Ejemplo de datos

La estructura de datos utilizada para esta historia se encuentra en el archivo:

**`ejemplo-datos.json`**

---

# Especificación funcional: Consulta de disponibilidad de cubículos en tiempo real

## 1. Información general

- **Módulo:** Cubículos de estudio.
- **Historia asociada:** US-11 - Consulta de disponibilidad de cubículos en tiempo real.
- **Issue relacionado:** #22.
- **Integrante redactora:** Wendy Jolet Rodríguez Jiménez.

### Historia de usuario

Como alumna quiero consultar el calendario y estatus en tiempo real de los cubículos de estudio para identificar horarios libres antes de programar una reserva.

---

## 2. Flujo de interacción del usuario

1. El alumno ingresa al portal de la biblioteca.
2. Selecciona la opción **"Consultar disponibilidad de cubículos"**.
3. El sistema muestra una cuadrícula o listado con el identificador, la capacidad y el estado actual de cada cubículo: **Disponible, Ocupada, Reservada o En mantenimiento**.
4. El alumno selecciona la fecha, la hora de inicio y la hora de fin que desea consultar.
5. Opcionalmente, selecciona el tamaño del cubículo:
   - **Chica:** de 3 a 4 personas.
   - **Grande:** de 5 a 6 personas.
6. El alumno presiona el botón **"Consultar"**.
7. El sistema valida la fecha y el rango de horas.
8. El sistema muestra los cubículos que cumplen con la capacidad seleccionada e indica si están disponibles durante todo el intervalo solicitado.
9. Si no existen coincidencias, el sistema muestra: **"No hay cubículos que coincidan con los filtros seleccionados"**.
10. Cuando se registra un cambio de ocupación, reserva o mantenimiento, el sistema actualiza automáticamente la información y conserva los filtros seleccionados.

---

## 3. Reglas del sistema y validaciones

### Visualización de estados

Cada cubículo debe mostrar su identificador, capacidad y una etiqueta de texto con su estado:

- **Disponible:** está habilitado y libre en el momento consultado.
- **Ocupada:** tiene una sesión de uso activa.
- **Reservada:** tiene una reserva vigente para el momento consultado, sin una sesión de uso activa.
- **En mantenimiento:** se encuentra fuera de servicio.

El sistema debe distinguir entre el **estado actual** y la **disponibilidad para el intervalo seleccionado**. Un cubículo disponible ahora puede tener una reserva para un horario posterior.

### Filtro por capacidad

- La opción **Chica** muestra cubículos con capacidad para 3 o 4 personas.
- La opción **Grande** muestra cubículos con capacidad para 5 o 6 personas.
- Si no se selecciona tamaño, se consideran ambos tipos.
- El filtro de capacidad y el rango de horas se aplican conjuntamente.

### Filtro por fecha y rango de horas

- La fecha y las horas deben ser válidas.
- La hora de inicio debe ser anterior a la hora de fin.
- El intervalo solicitado debe encontrarse dentro del horario de servicio configurado por la biblioteca.
- Un cubículo solo se considera disponible para todo el intervalo si no existen reservas, ocupaciones o mantenimientos que se superpongan con este.

Existe superposición cuando se cumplen ambas condiciones:

- El inicio del bloqueo existente es anterior al fin solicitado.
- El fin del bloqueo existente es posterior al inicio solicitado.

Por ejemplo, una reserva de **10:30 a 11:30** impide considerar disponible el cubículo para una consulta de **10:00 a 11:00**.

Una reserva que termina exactamente a las **10:00** no genera conflicto con una consulta que comienza a las **10:00**.

### Actualización en tiempo real

- Los cambios de reservas, ocupación y mantenimiento deben reflejarse automáticamente en la consulta.
- Cuando se registra una cancelación o liberación anticipada mediante US-10, el sistema debe recalcular la disponibilidad.
- La actualización debe conservar la fecha, capacidad y horario seleccionados.
- El sistema debe mostrar la fecha y hora de la última actualización.
- Si no puede actualizar la información, debe mostrar un aviso e identificar los datos anteriores como pendientes de actualización.

### Mensajes de validación

| Situación | Mensaje del sistema |
| --- | --- |
| Fecha u hora inválida | Ingresa una fecha y un horario válidos. |
| Hora de inicio igual o posterior a la hora de fin | La hora de inicio debe ser anterior a la hora de fin. |
| Intervalo fuera del horario de servicio | Selecciona un intervalo dentro del horario de servicio. |
| Sin resultados para los filtros | No hay cubículos que coincidan con los filtros seleccionados. |
| Error al actualizar la información | No fue posible actualizar la disponibilidad. Intenta nuevamente. |

---

## 4. Ejemplo de datos

El siguiente JSON contiene datos ficticios de una consulta de cubículos chicos para el 19 de octubre de 2026, de 10:00 a 11:00, hora de Ciudad de México.

```json
{
  "historia": "US-11",
  "consulta": {
    "inicio": "2026-10-19T10:00:00-06:00",
    "fin": "2026-10-19T11:00:00-06:00",
    "tipo": "chica"
  },
  "ultima_actualizacion": "2026-10-19T09:55:00-06:00",
  "cubiculos": [
    {
      "id": "C01",
      "capacidad": 4,
      "tipo": "chica",
      "estado_actual": "Disponible",
      "disponible_en_intervalo": true,
      "bloqueos": []
    },
    {
      "id": "C02",
      "capacidad": 3,
      "tipo": "chica",
      "estado_actual": "Disponible",
      "disponible_en_intervalo": false,
      "bloqueos": [
        {
          "tipo": "Reservada",
          "inicio": "2026-10-19T10:30:00-06:00",
          "fin": "2026-10-19T11:30:00-06:00"
        }
      ]
    }
  ]
}
```

El cubículo **C01** está disponible durante todo el intervalo solicitado.

El cubículo **C02** está disponible en el momento de la actualización, pero no durante todo el intervalo consultado, porque tiene una reserva que comienza a las 10:30.

---

## 5. Casos de prueba de aceptación propuestos

Estos casos describen cómo verificar el comportamiento especificado; no representan pruebas ejecutadas de una aplicación.

| Caso | Acción o condición | Resultado esperado |
| --- | --- | --- |
| CP-01 | Abrir la consulta de cubículos | Mostrar identificador, capacidad y estado actual de cada cubículo. |
| CP-02 | Consultar cubículos con distintos estados | Mostrar las etiquetas Disponible, Ocupada, Reservada y En mantenimiento, según corresponda. |
| CP-03 | Seleccionar el filtro Chica | Mostrar únicamente cubículos con capacidad para 3 o 4 personas. |
| CP-04 | Seleccionar el filtro Grande | Mostrar únicamente cubículos con capacidad para 5 o 6 personas. |
| CP-05 | Consultar un intervalo sin bloqueos | Indicar que el cubículo está disponible durante todo el intervalo. |
| CP-06 | Consultar un intervalo con una reserva superpuesta | Indicar que el cubículo no está disponible durante todo el intervalo. |
| CP-07 | Consultar desde la hora exacta en que termina otra reserva | No considerar esa reserva como un conflicto. |
| CP-08 | Introducir una hora de inicio igual o posterior a la de fin | Mostrar el mensaje de validación y no ejecutar la consulta. |
| CP-09 | Registrar una cancelación o liberación anticipada | Recalcular y actualizar automáticamente la disponibilidad conservando los filtros. |
| CP-10 | Aplicar filtros sin coincidencias | Mostrar el mensaje de ausencia de resultados. |
| CP-11 | Perder la conexión durante la consulta | Mostrar el aviso de actualización fallida e identificar los datos como pendientes de actualización. |
