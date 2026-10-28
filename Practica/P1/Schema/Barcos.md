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
  Barco ---cif([cif]):::atributo 
  end
```

```sql
CREATE TABLE BARCO (
    matricula     CHAR(10) PRIMARY KEY,
    nombre        VARCHAR(30),
    clase         VARCHAR(20),
    capitan       VARCHAR(30),
    armador       VARCHAR(30),
    cif       	  VARCHAR(15) UNIQUE
    );
```
