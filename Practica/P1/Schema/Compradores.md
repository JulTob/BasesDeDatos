# Compradores

- [x]  🔐 __Código__ (no repetible),
- [x]  Nombre,
- [x]  Dirección,
- [x]  DNI o CIF,
- [x]  Cuota anual que deben pagar a la lonja.

## Creditores y Contadores
Existen compradores de dos tipos
---
1. ### A Credito (Creditores)
   Que tienen crédito, realizando los pagos al final de cada mes:
  - [] Número de cuenta bancaria (IBAN).
  - [] Importe acumulado hasta el momento.
  - [] Fecha de vencimiento del pago.
  ---
2. ### Al contado (Contadores)
  - [] No se requiere información adicional
  ---

> Un comprador no puede ser de ambos tipos a la vez.




```mermaid
flowchart LR
  classDef atributo stroke:#088,stroke-width:2px;
  classDef derivado stroke-width:3px, stroke-dasharray:3 3;
  classDef pk stroke:#800,stroke-width:4px;
  classDef fk stroke:#080,stroke-width:4px;
  classDef pkfk stroke:#880,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;
  classDef pseudoentidad stroke:#323,stroke-width:4px;

  %% Atributos COMPRADOR
  subgraph Compradores
    Comprador[COMPRADOR]:::entidad
    Comprador ---|PK| cod_comprador([cod_comprador]):::pk
    Comprador --- nombre([nombre]):::atributo 
    Comprador --- direccion([direccion]):::atributo 
    Comprador --- dni_cif([dni_cif]):::atributo 
    Comprador --- cuota_anual([cuota_anual]):::atributo 
    end

  Comprador --> es{d} -->|1:0..1| Creditor[CREDITOR]:::entidad
				es{d} --x|pseudoentidad| contador[CONTADOR]:::pseudoentidad

```
