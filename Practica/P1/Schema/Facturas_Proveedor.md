# Factura Proveedor
Las facturas emitidas por los barcos:
- Datos básicos:
  - Número de factura.
  - Fecha de emisión.
  - Importe total.
- El CIF del barco (desde matrícula).
- Los códigos de lote facturados.

Las facturas emitidas por los barcos,
- [x] Datos básicos
	- [x] Número de factura
	- [x] Fecha de emisión
	- [x] Importe total.
- [x] el CIF del barco (desde matricula)
- [x] Los códigos de lote facturados


```mermaid
flowchart LR

classDef entidad stroke:#404,stroke-width:4px;
classDef relacion stroke:#840,stroke-width:2px;
classDef atributo stroke:#088,stroke-width:2px;

Barco[BARCO]:::entidad
FacturaB[FACTURA_PROVEEDOR]:::entidad
Lote[LOTE]:::entidad
Provision{{PROVISION}}:::relacion

FacturaB --- num_fact_b([num_factura]):::atributo  
FacturaB --- fecha_emision_b([fecha_emision]):::atributo 
FacturaB --- importe_total_b([importe_total]):::atributo  
FacturaB --- pagada_b([pagada]):::atributo  

Barco ---|"(1,N)"| FacturaB
FacturaB ---|"(1,N)"| Provision
Provision ---|"(1,1)"| Lote

```
```sql
CREATE TABLE FACTURA_PROVEEDOR (
    num_factura  		CHAR(10) PRIMARY KEY,
    matricula          	CHAR(10) NOT NULL REFERENCES BARCO,
    fecha_emision      	DATE NOT NULL,
    importe_total      	NUMBER(10,2),
    pagada             	NUMBER(1,0) DEFAULT 1
    -- 1 = pendiente, 0 = pagada
	);

CREATE TABLE PROVISION (
    num_factura  			CHAR(10) REFERENCES FACTURA_PROVEEDOR,
    cod_lote           		CHAR(5)  REFERENCES LOTE UNIQUE,
    PRIMARY KEY (num_factura, cod_lote)
	);

CREATE TABLE PAGO_BARCO (
    cod_pago      CHAR(5) PRIMARY KEY,
    num_factura   CHAR(10) REFERENCES FACTURA_PROVEEDOR,
    fecha         DATE,
    importe       NUMBER(10,2)
);
```
Aunque el enunciado dice que en la factura se almacena el CIF del barco, optamos por guardar el CIF como atributo del BARCO y referenciar el barco desde FACTURA_PROVEEDOR usando su clave actual. 

Así evitamos redundancia; el CIF es accesible mediante una consulta.
Otra alternativa sería cambiar la clave principal o hacer una compuesta. Al ser requisitos bastante separados, es posible que sea una confusión del cliente, ya que el campo cif no estaba requerido en la información del barco. Por tanto, técnicamente no está relacionando una entidad con otra añadir el cif a la factura. 

Considero que esta opción es la más sencilla, y que la interfaz puede presentar está información como el cliente prefiera. Antes de implementar esta decisión de diseño consultaría con el cliente.


