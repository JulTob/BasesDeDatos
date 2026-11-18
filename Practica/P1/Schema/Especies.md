# Especies
  - [x]  🔐 __Código__ (no repetible)
  - [x]  Nombre
  - [x]  Tipo (por ejemplo, moluscos, pescado blanco, etc.).
```mermaid
flowchart LR   
  classDef atributo stroke:#088,stroke-width:2px;
  classDef pk stroke:#800,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;

  %% Atributos ESPECIE
  subgraph Especies
    Especie[ESPECIE]:::entidad
    Especie ---|PK| cod_especie(["<b><u>cod_especie</u></b>"]):::pk
    Especie ---nombre_especie([nombre]):::atributo 
    Especie ---tipo_especie([tipo]):::atributo 
    end


```
```sql
CREATE TABLE ESPECIE (
    cod_especie   VARCHAR(5) PRIMARY KEY,
    nombre        VARCHAR(30) NOT NULL,
    tipo          VARCHAR(20) NOT NULL
    );
```

