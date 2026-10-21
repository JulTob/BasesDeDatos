# Práctica 1 — Lonja de Santa Pola

## Modelo Conceptual (ERE) y Relacional

> Nota de transcripción: el PDF facilitado contiene requisitos mezclados con una resolución. Se recogen aquí los fragmentos del enunciado presentes en ese documento, sin el SQL, los diagramas ni los comentarios de diseño. Se conserva la numeración disponible: no aparece el apartado 3.1. El documento no especifica una fecha de entrega.

## 1. Objetivos

- Access 2016/2019/2021/2024.
  - Modelización ERE y su correspondiente Relacional.
  - Creación de tablas con sus campos así como la definición de los dominios de los campos y establecimiento de las relaciones.

## 2. Enunciado de la práctica

La lonja de pescado de Santa Pola desea agilizar la gestión de su negocio a tal efecto, nos solicita proveerlos de una solución de bases de datos.

Cada día, los barcos llevan la pesca a la lonja, siendo que allí, se subasta la captura. Normalmente los compradores son pescaderías de la zona. Tras múltiples entrevistas con los usuarios y labores de análisis previo, hemos obtenido las siguientes especificaciones iniciales:

### Lotes

La captura del día se distribuye en lotes.

- Código único.
- Número de cajas.
- Una determinada especie.
- Número de kilos total.
- Fecha de llegada.
- Precio por kilo de salida.
- Precio total de salida del lote.
- Qué barco capturó cada lote.

### Especies

- Código (no repetible).
- Nombre.
- Tipo (por ejemplo, moluscos, pescado blanco, etc.).

### Barcos

- Matrícula.
- Nombre.
- Clase.
- Nombre del capitán.
- Nombre del armador.
- CIF.

### Caladeros

- Nombre (único).
- Extensión.
- Ubicación [GPS]:
  - Latitud.
  - Longitud.

### Faenaje

- Faena:
  - Un barco (matrícula).
  - En un caladero (nombre).
  - Una especie (código).
  - Los kilos obtenidos de cada especie.
  - En un intervalo de tiempo:
    - Una fecha de inicio.
    - Y otra de fin.

### Compradores

- Código (no repetible).
- Nombre.
- Dirección.
- DNI o CIF.
- Cuota anual que deben pagar a la lonja.

### Compradores: Creditores y Contadores

- Existen compradores que tienen crédito (creditores), realizando los pagos al final de cada mes:
  - Se guarda un número de cuenta bancaria.
  - El último importe acumulado hasta el momento.
  - Y la fecha de vencimiento del pago.
- Existen los compradores que realizan los pagos al contado (contadores) sobre los que no se necesita guardar información adicional.
- Un comprador no puede ser de ambos tipos a la vez.

### Adjudicación

Los lotes se subastan. Cada lote será adquirido por el comprador que realice la mejor puja.

- Precio de compra por kilo.
- Precio total de adjudicación del lote.
- Cada lote será adquirido por un comprador.
- Un comprador puede adquirir varios lotes.

### Facturas

Facturas de Pagos (de los compradores por los lotes).

- Cada factura corresponde a un comprador.
- Una factura puede incluir uno o varios lotes.
- Número de factura.
- Fecha de emisión.
- Importe total.
- Estado (pendiente o pagada).
- Cada lote en exactamente una factura.
- Un comprador puede tener muchas facturas.

### Factura Proveedor

Las facturas emitidas por los barcos:

- Datos básicos:
  - Número de factura.
  - Fecha de emisión.
  - Importe total.
- El CIF del barco (desde matrícula).
- Los códigos de lote facturados.

## 3.2. Modelo Relacional

Basándose en el esquema conceptual (Modelo ERE) desarrollado en el anterior apartado se deberá crear el Modelo Relacional, el cual reflejará lo más fielmente posible una solución al problema que se nos plantea. Éste se ha de documentar utilizando la herramienta Microsoft Visio usando la plantilla para Bases de Datos relacionales con notaciones IDEF1X haciendo constar, los siguientes elementos:

- Tablas con sus atributos o campos y sus dominios.
- Claves Primarias y Alternativas.
- Claves Ajenas indicando su dependencia.
- Los posibles o no nulos.
- Valores por defecto.
- Cardinalidades.
- Acción para la preservación de la Integridad Referencial.
- … en definitiva, todos los elementos explicados para los esquemas relacionales que sean necesarios para plasmar el enunciado.

Solo se podrán usar los siguientes tipos de datos:

- `VARCHAR`.
- `CHAR`.
- `NUMBER`.
- `DATE`.

Recordad que es importante que el tipo de dato, y en general el dominio de cada atributo, esté desarrollado conforme al concepto que representa.

La forma de transformar una relación ternaria del tipo Muchos, Muchos, Muchos (N:N:N) es, una vez creadas las tablas correspondientes a las entidades partícipes, crear una nueva tabla que representará dicha relación ternaria y que debe incluir como claves foráneas las claves principales de cada una de las tres entidades partícipes. El conjunto formado por estas claves foráneas será la clave principal de la nueva tabla. En dicha nueva tabla se debe incluir también los atributos de la relación siguiendo los mismos criterios que se siguen en los atributos de una relación binaria de tipo N:N.

## 3.3. Creación de la base de datos

En consonancia con lo desarrollado en el anterior apartado, construid el definitivo esquema de base de datos relacional en Access.

## 4. Formato y fecha de entrega

Se entregará un fichero comprimido en formato `.zip` o `.rar` cuyo contenido ha de ser:

a) Un documento de Word o PDF con la siguiente información:

1. DNI, Nombre y Apellidos del Alumno.
2. Diseño Conceptual incluyendo los supuestos semánticos y la semántica perdida.
   1. El fichero Microsoft Visio con el diseño del modelo relacional.
   2. Las base de datos de Access que se construya a partir del modelo relacional.

> La anidación de los dos últimos elementos reproduce la disposición del PDF facilitado.
