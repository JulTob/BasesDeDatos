# Lotes

La captura del día se distribuye en **Lotes**:
- [x] Código único
- [x] Número de cajas
- [x] Una determinada especie
- [x] Número de kilos total
- [x] Fecha de llegada
- [x] Precio por kilo de salida
- [x] Precio total de salida del lote
- [x] **Qué barco capturó cada lote**

      
```mermaid
flowchart LR
  classDef atributo stroke:#088,stroke-width:2px;
  classDef pk stroke:#800,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;
  classDef relacion stroke:#840,stroke-width:2px;
  classDef fk stroke:#080,stroke-width:4px;

  %% Atributos LOTE
  subgraph Lotes
    Lote[LOTE]:::entidad
    Lote ---|PK| cod_lote([cod_lote]):::pk   
    Lote --- num_cajas([num_cajas]):::atributo  
    Lote --- kilos_total([kilos_total]):::atributo  
    Lote --- fecha_llegada([fecha_llegada]):::atributo  
    Lote --- precio_kg_salida([precio_kg_salida]):::atributo  
    Lote --- precio_total_salida([precio_total_salida]):::atributo  
    Lote ---|FK| matricula_barco([matricula_barco]):::fk  
    Lote ---|FK| cod_especie([cod_especie]):::fk  

    end 

matricula_barco ---> Barco
Barco[BARCO]:::entidad

cod_especie ---> Especie
Especie[ESPECIE]:::entidad

```
```sql
CREATE TABLE LOTE (
    cod_lote            CHAR(5) PRIMARY KEY,
    num_cajas           NUMBER(6,0) NOT NULL CHECK (num_cajas > 0),
    kilos_total         NUMBER(8,2) NOT NULL CHECK (kilos_total > 0),
    fecha_llegada       DATE NOT NULL,
    precio_kg_salida    NUMBER(8,2) NOT NULL CHECK (precio_kg_salida >= 0),
    precio_total_salida NUMBER(8,2) NOT NULL CHECK (precio_total_salida >= 0),
    cod_especie         VARCHAR(5) NOT NULL REFERENCES ESPECIE (cod_especie),
    matricula_barco     CHAR(10) NOT NULL REFERENCES BARCO (matricula),
    UNIQUE (cod_lote, matricula_barco)
    );
```

La pareja de lote y matrícula permite comprobar que el emisor de una factura recibida es el barco que capturó ese lote. El código del lote sigue siendo por sí solo su identificador.
