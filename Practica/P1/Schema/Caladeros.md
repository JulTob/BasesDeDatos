# Caladeros
  - [x]  🔐 __Nombre__ (único),
  - [x]  Extensión
  - [x]  Ubicación [GPS]
      - [x]  latitud 
      - [x]  longitud.

```mermaid
flowchart LR   
  classDef atributo stroke:#088,stroke-width:2px;
  classDef derivado stroke-width:3px, stroke-dasharray:3 3;
  classDef compuesto stroke-width:6px, stroke-dasharray:1 1;
  classDef pk stroke:#800,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;

  %% Atributos CALADERO
  subgraph Caladeros
    Caladero[CALADERO]:::entidad
    Caladero ---|PK| nombre([nombre]):::pk 
    Caladero --- ubicacion([ubicacion]):::atributo 
    Caladero --- extension([extension]):::atributo 
      ubicacion:::compuesto
      ubicacion  --- latitud([latitud]):::atributo
	  ubicacion  --- longitud([longitud]):::atributo 

    end
```
```sql
CREATE TABLE CALADERO (
    nombre        VARCHAR(40) PRIMARY KEY,
    extension     NUMBER(10,2) NOT NULL CHECK (extension > 0),
    latitud       NUMBER(8,5) NOT NULL CHECK (latitud BETWEEN -90 AND 90),
    longitud      NUMBER(8,5) NOT NULL CHECK (longitud BETWEEN -180 AND 180)
    );
```

La ubicación es un atributo compuesto por latitud y longitud en grados decimales. Se supone que la extensión se mide en km².
