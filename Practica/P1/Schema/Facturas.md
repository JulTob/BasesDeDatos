

# FACTURAS (Lonja)


- [x] Facturas de Pagos (de los compradores por los lotes).
  - [x] Cada factura corresponde a un comprador.
  - [x] Una factura puede incluir uno o varios lotes.
  - [x] Número de factura
  - [x] Fecha de emisión
  - [x] Importe total.
  - [x] Estado (pendiente o pagada).
  - [x] Cada lote en exactamente una factura.
  - [x] Un comprador puede tener muchas facturas.
     


```mermaid
flowchart LR
  classDef atributo stroke:#088,stroke-width:2px;
  classDef derivado stroke-width:3px, stroke-dasharray:3 3;
  classDef pk stroke:#800,stroke-width:4px;
  classDef fk stroke:#080,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;
  classDef multientidad stroke:#808,stroke-width:8px;
  classDef pkfk stroke:#880,stroke-width:4px;
  classDef relacion stroke:#840,stroke-width:4px;


  Comprador[COMPRADOR]:::entidad
  Factura[FACTURA_CLIENTE]:::entidad
  Lote[LOTE]:::entidad
  Incluye{{INCLUYE}}:::relacion

  Factura ---|PK| num_fact([num_factura]):::pk 
  Factura --- fecha_emision([fecha_emision]):::atributo  
  Factura --- importe_total([importe_total]):::atributo 
  Factura --- pendiente([pendiente]):::atributo 

  Factura ---|"(1,N)"| Incluye
  Incluye ---|"(1,1)"| Lote

  Comprador ---|"(1,N)"| Factura

```

```sql
CREATE TABLE FACTURA_CLIENTE (
    num_factura      	CHAR(10) PRIMARY KEY,
    cod_comprador    	CHAR(5) NOT NULL REFERENCES COMPRADOR,
    fecha_emision    	DATE NOT NULL,
    importe_total    	NUMBER(10,2),
    pendiente         NUMBER(1,0) DEFAULT 0
			-- 1 = pendiente, 0 = pagada
);

CREATE TABLE INCLUYE (
    num_factura   CHAR(10) REFERENCES FACTURA_CLIENTE,
    cod_lote      CHAR(5)  REFERENCES LOTE UNIQUE,
    PRIMARY KEY (num_factura, cod_lote)
);

```
- INCLUYE es la relación N:M.
- PRIMARY KEY (num_factura, cod_lote) impide repetir un lote en la misma factura.

Estado Pagada: 
- 1 = pendiente (TRUE)
- 0 = pagada (FALSE)
- `DEFAULT 0` asegura que todas las facturas nuevas comiencen como pagadas, ya que es el default de las .
- Este campo actúa como booleano.
- Guardamos el estado para todas las facturas, aunque solo sea relevante para compradores al contado. Para el grupo que no es de interés se ponen como pagadas automaticamente.
  
Cada comprador puede emitir varias facturas; cada factura agrupa varios lotes.

Cada lote pertenece a una única factura (por post-adjudicación).


