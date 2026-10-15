# Especificación funcional: Emisión de constancia de No Adeudo

## 1. Información general

* **Módulo:** Constancia de No Adeudo (Célula 4) 
* **Historia Principal:** [US-08] Emisión de constancia de No Adeudo
* **Historia Asociada:** [US-07] Cálculo automático de multas por mora
* **Integrante redactores:** Braulio Eduardo Sánchez Morales

## 2. Flujo de interacción del usuario

1. El alumno egresado ingresa al portal del sistema bibliotecario y selecciona la opción "Constancia de No Adeudo".
2. El sistema identifica la sesión activa o solicita ingresar la matrícula del alumno.
3. El sistema consulta la base de datos para verificar el historial de préstamos y el estado de cuenta del alumno.
4. Al comprobar que no hay libros pendientes ni multas económicas (saldo de $0), el sistema procesa la solicitud.
5. Se genera y emite un comprobante digital en formato PDF con su respectivo folio único y sello de validación escolar, el cual se muestra en pantalla listo para descargar.

## 3. Reglas del sistema (Criterios de aceptación)

* **Validación estricta de adeudos:** El sistema debe bloquear la emisión de la constancia si detecta $1 o más pesos de saldo en multas por mora (derivado de la US-07) o 1 o más libros no devueltos.
* **Identificación única:** Cada constancia digital generada debe tener asignado un folio alfanumérico único para evitar duplicidades y permitir su rastreo en control escolar.
* **Autenticidad del documento:** El comprobante generado tiene que incrustar obligatoriamente el sello de validación escolar (firma digital, marca de agua o código verificador) válido para trámites de titulación.
* **Mensaje de rechazo:** Si el alumno tiene adeudos, el sistema no generará el documento y deberá mostrar un mensaje indicando el motivo exacto (ej. "No es posible emitir la constancia. Tienes un adeudo pendiente").

## 4. Ejemplo de datos (Estructura esperada)

```json
{
  "idAlumno": "ALU-001",
  "prestamosPendientes": 0,
  "montoMultas": 0,
  "constancia": {
    "folio": "NA-2026-0001",
    "fechaEmision": "2026-10-13",
    "estado": "EMITIDA",
    "selloValidacion": "SELLO-INSTITUCIONAL"
  }
}
```
