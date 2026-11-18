# Barcos
  - [x]  🔐 Matrícula
  - [x]  Nombre
  - [x]  Clase
  - [x]  Nombre del capitán
  - [x]  Nombre del armador
  - [x]  CIF
```mermaid
flowchart LR   
  classDef atributo stroke:#088,stroke-width:2px;
  classDef pk stroke:#800,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;

  %% Atributos BARCO
  subgraph Barcos
  Barco[BARCO]:::entidad
  Barco ---|PK| matricula([matricula]):::pk  
  Barco ---nombre([nombre]):::atributo  
  Barco ---clase([clase]):::atributo  
  Barco ---capitan([capitan]):::atributo 
  Barco ---armador([armador]):::atributo 
  Barco ---|AK| cif([cif]):::atributo
  end
```

```sql
CREATE TABLE BARCO (
    matricula     CHAR(10) PRIMARY KEY,
    nombre        VARCHAR(30) NOT NULL,
    clase         VARCHAR(20) NOT NULL,
    capitan       VARCHAR(30) NOT NULL,
    armador       VARCHAR(30) NOT NULL,
    cif       	  VARCHAR(15) NOT NULL UNIQUE
    );
```

La matrícula identifica al barco y el CIF constituye una clave alternativa obligatoria. Se conserva como texto para admitir letras y ceros iniciales.
