# Especificación funcional: Módulo de Inicio de Sesión

## 1. Información general

* **Módulo:** Autenticación y Acceso
* **Historia Asociada:** US-01 - Inicio de sesión con matrícula
* **Integrantes redactores:** Erik Lopez Ibarra - Edrick Yamil Garduño Toscuento

## 2. Flujo de interacción del usuario

1. El alumno ingresa al portal de la biblioteca y selecciona la opción "Iniciar sesión".
2. El sistema muestra un formulario solicitando la matrícula institucional.
3. El alumno ingresa su matrícula y presiona el botón de acceder.
4. El sistema valida que la matrícula tenga el formato correcto.
5. El sistema consulta la base de datos para verificar si el alumno tiene alguna sanción activa.
6. Si las validaciones son correctas, el sistema otorga el acceso y redirige al alumno a su panel de servicios de biblioteca.

## 3. Reglas del sistema (Criterios de aceptación)

* **Formato de matrícula:** El sistema debe validar estrictamente que la matrícula institucional ingresada esté compuesta por exactamente 10 dígitos numéricos.
* **Estado del usuario (Sanciones):** El sistema debe denegar el acceso e impedir el inicio de sesión si el alumno tiene una sanción activa en el sistema, mostrando un mensaje informativo sobre la restricción.
