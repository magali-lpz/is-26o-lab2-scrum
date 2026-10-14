
# Especificación Funcional - US-03

## 1. Información general

- **Módulo:** Catálogo y Búsqueda (Célula 2).
- **Historias asociadas al módulo:** US-03 y US-04.
- **Historia desarrollada en este documento:** US-03 - Búsqueda de libros por ISBN y título.
- **Integrantes redactores:**
  - Luis Uriel Mondragón Ramírez.
  - Martinez Perez Gabriel.
  - Leonardo D Maldonado Garduño.
  - Valeria Danaí Millán Acosta.

## 2. Flujo de interacción del usuario

1. El alumno ingresa al portal de la biblioteca y selecciona la opción de búsqueda de libros.
2. El sistema muestra un campo de búsqueda donde el alumno puede introducir el título o ISBN del libro que desea consultar.
3. El alumno ingresa el nombre del libro, una parte del título o su código ISBN.
4. El sistema verifica que los datos ingresados cumplan con las validaciones establecidas.
5. Si la búsqueda es por título, el sistema muestra los libros que coincidan parcial o totalmente con las palabras ingresadas.
6. Si la búsqueda es por ISBN, el sistema muestra únicamente el libro cuyo código coincida exactamente con el registrado.
7. Si se encuentran coincidencias, el sistema presenta los resultados junto con el número de ejemplares disponibles en sala y para préstamo a domicilio.
8. El alumno puede seleccionar el libro de su interés para consultar su información y disponibilidad.
9. Si no se encuentran coincidencias, el sistema muestra un mensaje indicando que no existen resultados para la búsqueda realizada.

## 3. Reglas del sistema (Criterios de aceptación)

**Validación y normalización de ISBN:**

- Se deben eliminar automáticamente los guiones y espacios del ISBN antes de realizar la consulta en la base de datos.
- Si el formato del ISBN ingresado es inválido por tener un número incorrecto de dígitos, el sistema muestra un mensaje de advertencia sin ejecutar la búsqueda.
- La búsqueda por ISBN debe ser exacta, mostrando únicamente el libro cuyo código coincida con el ingresado.

**Búsqueda flexible por título:**

- **Insensibilidad al formato:** La búsqueda debe ignorar diferencias entre mayúsculas, minúsculas, tildes y acentos diacríticos.
- **Coincidencia parcial:** Se deben permitir búsquedas mediante palabras clave o títulos incompletos.
- **Longitud mínima:** El alumno debe ingresar al menos 3 caracteres para realizar una búsqueda por título.

**Validación de entradas vacías:**

- El botón de búsqueda permanece deshabilitado cuando el campo está vacío o contiene únicamente espacios en blanco.
- El sistema evita ejecutar consultas sin un criterio de búsqueda válido.

**Disponibilidad de ejemplares:**

- Cada libro encontrado debe mostrar el número de ejemplares disponibles para consulta en sala.
- El sistema debe indicar la cantidad de ejemplares disponibles para préstamo a domicilio.
- Si no existen ejemplares disponibles en alguna modalidad, se debe mostrar la cantidad cero.

**Resultados de búsqueda:**

- Si existen coincidencias, el sistema muestra los libros encontrados con su título, ISBN y disponibilidad.
- Si no existen coincidencias, el sistema muestra el mensaje: "No se encontraron libros que coincidan con la búsqueda".

## 4. Ejemplo de datos (Estructura esperada)

```json
{
  "isbn": "9780307474728",
  "titulo": "Cien años de soledad",
  "ejemplares_sala": 3,
  "ejemplares_domicilio": 2,
  "estatus": "DISPONIBLE"
}
```
