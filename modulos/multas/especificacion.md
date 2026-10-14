US-07: Cálculo automático de multas por mora

Historia de usuario

Como usuario del sistema de préstamos de biblioteca, quiero que el sistema calcule automáticamente las multas por días de retraso en la devolución de materiales, para registrar los adeudos correspondientes y aplicar las sanciones establecidas.

2.1 Criterios de aceptación

- El sistema debe identificar la fecha límite de devolución del material prestado.
- El sistema debe calcular los días naturales de retraso cuando la devolución se realice después de la fecha límite.
- El sistema debe calcular automáticamente la multa multiplicando los días de retraso por la tarifa diaria configurada.
- El sistema debe registrar el importe de la multa como un adeudo del alumno.
- El sistema debe suspender temporalmente el derecho a solicitar nuevos préstamos mientras exista un adeudo pendiente.
- El sistema debe permitir retirar la suspensión cuando el adeudo haya sido liquidado y no existan otros adeudos pendientes.

2.2 Flujo de interacción

1. El sistema consulta la fecha límite de devolución registrada para el préstamo.
2. El sistema obtiene la fecha efectiva de devolución o, si el material aún no se devuelve, utiliza la fecha actual para determinar el retraso.
3. Si la fecha de devolución es posterior a la fecha límite, el sistema calcula los días naturales transcurridos.
4. El sistema multiplica los días de retraso por la tarifa fija diaria configurada.
5. El sistema registra o actualiza la multa correspondiente en la cuenta del alumno.
6. Si existe un adeudo pendiente, el sistema suspende temporalmente el derecho a solicitar nuevos préstamos.
7. Cuando el alumno liquida el adeudo, el sistema actualiza su estado y retira la suspensión si no existen otros adeudos pendientes.

2.3 Reglas de negocio y validaciones

- La multa se calcula únicamente cuando existe retraso respecto a la fecha límite de devolución.
- Cada día natural de retraso genera un recargo conforme a la tarifa diaria configurada.
- La tarifa diaria debe ser definida o confirmada por el Product Owner, ya que el requerimiento no especifica una cantidad monetaria.
- Si el material se devuelve en la fecha límite o antes, no se genera una multa por mora.
- El sistema debe registrar el importe total de la multa y su estado de pago.
- Mientras exista un adeudo pendiente, el alumno no podrá solicitar nuevos préstamos.
- La suspensión solo se retira cuando todos los adeudos pendientes del alumno han sido liquidados.
- El sistema debe evitar generar multas duplicadas por el mismo préstamo y periodo de retraso.
- Las reglas de redondeo, las posibles exenciones y el tratamiento de devoluciones parciales deberán confirmarse con el Product Owner antes de implementarse.

2.4 Ejemplo de datos (JSON)

{
  "id_prestamo": 105,
  "id_alumno": 2026,
  "fecha_limite": "2026-10-10",
  "fecha_devolucion": "2026-10-13",
  "dias_retraso": 3,
  "tarifa_diaria": 5.00,
  "multa_total": 15.00,
  "estado_adeudo": "pendiente",
  "prestamos_suspendidos": true
}

Nota: El ejemplo utiliza una tarifa hipotética de $5.00 por día únicamente para ilustrar el cálculo. La tarifa real debe confirmarse con el Product Owner.
