# Práctica 1 · Lonja de Santa Pola

**Julio Toboso · Fundamentos de Bases de Datos · Curso 2026–2027**

El modelo sigue un lote desde su llegada hasta la subasta, la facturación y el movimiento de dinero. La lonja puede registrar la llegada antes de conocer al comprador. Después puede identificar por separado qué ha cobrado del comprador y qué ha pagado al barco que entregó la pesca. [Enunciado de la práctica](Enunciado-Lonja-Santa-Pola.md) · [Modelo conceptual y participación](ERE.md)

## Del negocio a las tablas

| Operación | Qué queda identificado | Fichas del relacional |
|---|---|---|
| Recibir un lote | Su código, las cajas, los kilos, la fecha de llegada, los precios de salida por kilo y total, el barco y la especie. | [Lote](Schema/Lotes.md) · [Contenido del lote](Schema/Lote-Contiene-Especie.md) |
| Registrar la pesca | El barco, el caladero y la especie de cada captura durante un período, con sus kilos. | [Barco](Schema/Barcos.md) · [Caladero](Schema/Caladeros.md) · [Especie](Schema/Especies.md) · [Faena](Schema/Faenaje.md) |
| Dar de alta un comprador | Sus datos comunes y su modalidad. En crédito se conservan los datos de la mensualidad en curso. En contado se conoce la forma habitual de pago. | [Comprador, crédito y contado](Schema/Compradores.md) |
| Resolver la subasta | Si hay ganador, su código, el lote y los precios de adjudicación por kilo y total. | [Adjudicación](Schema/Adjudicación.md) |
| Facturar al comprador y cobrarle | La factura emitida por la lonja, sus lotes adjudicados y los cobros de esa factura. | [FACTURAS_EMITIDAS, INCLUYE y VENTA](Schema/Facturas.md) |
| Recibir la factura del barco y pagarla | El barco emisor, el número de su factura, sus lotes y los pagos de la lonja. | [FACTURAS_RECIBIDAS, PROVISION y PAGO_BARCO](Schema/Facturas_Proveedor.md) |

## Decisiones del diseño

**Identidad del barco.** La matrícula es la clave primaria y el CIF es una clave alternativa obligatoria. La factura recibida remite al barco por su matrícula. Así se recupera el CIF que pide el enunciado. Se conserva el criterio de admitir identificadores fiscales de longitud variable, hasta 15 caracteres, tanto para el barco como para el comprador. [Barcos](Schema/Barcos.md) · [Compradores](Schema/Compradores.md)

**Faena y procedencia.** Una misma embarcación puede capturar la misma especie en el mismo caladero en dos períodos diferentes. Por eso la fecha de inicio completa la clave formada por los tres participantes. Se supone que la misma terna tiene a lo sumo una faena con la misma fecha de inicio. El lote identifica su barco y especie. Si ambos coinciden en varias faenas, estos datos no permiten atribuir el lote a un único período o caladero. [Vista de captura](Diagramas/01-captura.png) · [Faenaje](Schema/Faenaje.md)

**Subasta.** Se conserva la decisión del proyecto de registrar el resultado. La adjudicación es opcional y el código del lote identifica un único resultado. Las pujas perdedoras y su secuencia quedan fuera del registro. La selección de la mejor puja corresponde a la subasta y no puede reconstruirse a partir de la adjudicación. [Vista de subasta](Diagramas/03-subasta.png) · [Adjudicación](Schema/Adjudicación.md)

**Modalidades del comprador.** Se consideran exhaustivas las dos modalidades descritas y se respeta su exclusividad. Cada comprador tendrá exactamente una ficha de crédito o de contado. El número de cuenta se trata como texto para conservar las letras y los ceros iniciales. La modalidad de contado conserva la forma habitual de pago, efectivo o tarjeta. [Compradores](Schema/Compradores.md)

**Numeración y titularidad de las facturas.** La lonja numera sus propias facturas emitidas. En las recibidas, el número tiene alcance por barco. Dos barcos distintos pueden presentar su factura 17. Cada lote puede figurar como máximo una vez en cada circuito. La factura emitida y la adjudicación deben identificar al mismo comprador. La factura recibida y el lote deben identificar al mismo barco. Las fichas muestran las claves ajenas compuestas que preservan estas coincidencias. [Facturas emitidas](Schema/Facturas.md) · [Facturas recibidas](Schema/Facturas_Proveedor.md)

**Cobros y pagos parciales.** Cada movimiento tiene código, fecha, importe y una factura obligatoria. Una factura puede tener cero, uno o varios movimientos. Si un comprador realiza un abono mensual que cubre varias facturas, se anota por separado el importe aplicado a cada una. Para contado, la consulta `ESTADO_CONTADO` calcula el saldo como el importe de la factura menos los cobros registrados. Un saldo positivo indica «pendiente» y un saldo de cero indica «pagada». Una factura de 100 € con un primer cobro de 40 € sigue pendiente de 60 €. [Cobros de compradores](Schema/Facturas.md) · [Pagos a barcos](Schema/Facturas_Proveedor.md)

## Controles al registrar operaciones

La existencia de claves ajenas permite verificar la titularidad de los lotes. Otras reglas afectan a varias filas y requieren comprobar la operación completa.

- Al dar de alta al comprador, verificar que queda en una sola modalidad y que tiene todos los datos de esa modalidad.
- Al emitir o registrar una factura, guardar su cabecera y al menos un lote del titular en la misma operación. Impedir que una modificación deje una factura sin lotes.
- Al registrar o modificar un cobro o pago, comprobar que su importe es positivo y que los movimientos acumulados caben en el importe de la factura. Calcular el estado de contado a partir del saldo resultante.

Los dominios de las tablas, las claves y las dependencias se detallan en las [fichas del modelo relacional](Schema/). El enunciado especifica por separado el contenido de la memoria, del dibujo relacional IDEF1X y de la base de datos de Access. [Formato de la entrega](Enunciado-Lonja-Santa-Pola.md)
