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
  classDef pk stroke:#800,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;

  %% Atributos CALADERO
  subgraph Caladeros
    Caladero[CALADERO]:::entidad
    Caladero ---|PK| nombre([nombre]):::pk 
    Caladero --- ubicacion((ubicacion)):::atributo 
    Caladero --- extension([extension]):::atributo 
      ubicacion:::derivado
      ubicacion  --- latitud([latitud]):::atributo
	  ubicacion  --- longitud([longitud]):::atributo 

    end
```
```sql
CREATE TABLE CALADERO (
    nombre        VARCHAR(40) PRIMARY KEY,
    extension     NUMBER(10,2),
    latitud       NUMBER(8,5),
    longitud      NUMBER(8,5)
    );
```
