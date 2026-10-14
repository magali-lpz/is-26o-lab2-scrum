**
# Especificación Funcional - US-04

## 1. Información general

- **Módulo:** Catálogo y Búsqueda (Célula 2).
- **Historias asociadas al módulo:** US-03 y US-04.
- **Historia desarrollada en este documento:** US-04 - Alta de nuevos ejemplares en catálogo.
- **Integrantes redactores:**
  - Luis Uriel Mondragón Ramírez.
  - Martinez Perez Gabriel.
  - Leonardo D Maldonado Garduño.
  - Valeria Danaí Millán Acosta.

## 2. Flujo de interacción del usuario

1. El bibliotecario ingresa al portal de la biblioteca y selecciona la opción "Registrar libro".
2. El sistema muestra un formulario para ingresar la información del libro.
3. El bibliotecario introduce el título, autor, editorial, año de publicación e ISBN.
4. El bibliotecario indica la cantidad de ejemplares físicos que desea registrar.
5. El sistema verifica que los campos obligatorios estén completos y que los datos tengan un formato válido.
6. El sistema consulta si el ISBN ya se encuentra registrado en el catálogo.
7. Si el libro ya existe, el sistema permite agregar nuevos ejemplares al registro existente.
8. Si el libro no existe, el sistema crea un nuevo registro con la información proporcionada.
9. El sistema genera automáticamente un identificador único para cada ejemplar físico registrado.
10. El sistema guarda la información y muestra un mensaje de confirmación con los ejemplares registrados.

## 3. Reglas del sistema (Criterios de aceptación)

**Registro de información del libro:**

- **Campos obligatorios:** El sistema debe solicitar título, autor, editorial, año de publicación e ISBN.
- **Validación de datos:** No se permite guardar registros con campos obligatorios vacíos.
- **Año de publicación:** Debe ingresarse como un valor numérico válido.
- **ISBN:** El sistema debe comprobar que el código tenga un formato válido antes de registrar el libro.

**Registro de ejemplares físicos:**

- **Identificador único:** Cada copia física debe recibir un identificador individual que no se repita dentro del sistema.
- **Múltiples ejemplares:** Si se registran varias copias de un mismo libro, cada una debe contar con su propio identificador.
- **Registro existente:** Si el ISBN ya está registrado, el sistema debe permitir agregar ejemplares sin duplicar la información bibliográfica del libro.
- **Cantidad de ejemplares:** El número de copias a registrar debe ser un número entero mayor que cero.

**Confirmación del registro:**

- El sistema debe guardar la información bibliográfica y los identificadores de los ejemplares registrados.
- Al finalizar correctamente, se muestra un mensaje de confirmación.
- Si ocurre un error durante el registro, el sistema informa al bibliotecario y evita guardar información incompleta.

## 4. Ejemplo de datos (Estructura esperada)

```json
{
  "isbn": "9780307474728",
  "titulo": "Cien años de soledad",
  "autor": "Gabriel García Márquez",
  "editorial": "Vintage Español",
  "anio_publicacion": 2009,
  "ejemplares": [
    {
      "id_ejemplar": "EJ-001",
      "estatus": "DISPONIBLE"
    },
    {
      "id_ejemplar": "EJ-002",
      "estatus": "DISPONIBLE"
    },
    {
      "id_ejemplar": "EJ-003",
      "estatus": "DISPONIBLE"
    }
  ]
}
```
**
