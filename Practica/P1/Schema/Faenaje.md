# Faenaje
- [x]  Faena
    - [x]  🔏 Un barco (matrícula)
    - [x]  🔏 En un caladero (nombre)
    - [x]  🔏 Una especie (código)
    - [x]  los kilos obtenidos de cada especie
    - [x]  en un intervalo de tiempo
        - [x]  una fecha (_timemark_) de inicio
        - [x]  y otra de fin.

```mermaid
flowchart LR   
  classDef atributo stroke:#088,stroke-width:2px;
  classDef derivado stroke-width:3px, stroke-dasharray:3 3;

  classDef pk stroke:#800,stroke-width:4px;
  classDef fk stroke:#080,stroke-width:4px;
  classDef pkfk stroke:#880,stroke-width:4px;
  classDef entidad stroke:#404,stroke-width:4px;

  %% Atributos FAENAJE
  subgraph Faenajes
    Faena[FAENA]:::entidad
    Faena --- kg_especie([kg_especie]):::atributo 
    Faena ---|PK FK| nombre([nombre_caladero]):::pkfk 
    Faena ---|PK FK| matricula([matricula_barco]):::pkfk 
    Faena ---|PK FK| cod_especie([cod_especie]):::pkfk
    Faena --- periodo((periodo)):::atributo
    periodo:::derivado
    periodo ---|PK| fecha_inicio([fecha_inicio]):::pk 
    periodo --- fecha_fin([fecha_fin]):::atributo

    end
  nombre ---> Caladero
  matricula ---> Barco
  cod_especie ---> Especie

  Caladero[CALADERO]:::entidad
  Barco[BARCO]:::entidad
  Especie[ESPECIE]:::entidad
```
```sql
CREATE TABLE FAENA (
    matricula_barco CHAR(10)   REFERENCES BARCO,
    nombre_caladero VARCHAR(40) REFERENCES CALADERO,
    cod_especie     VARCHAR(5) REFERENCES ESPECIE,
    kg_especie 		NUMBER(8,2),
    fecha_inicio    DATE,
    fecha_fin       DATE,
    PRIMARY KEY (matricula_barco, nombre_caladero, cod_especie, fecha_inicio)
    );
```


> Idea Alternativa:
> En lugar de relacionar Barco Especie y Caladero a tres
> Relacionar Lotes y Caladeros. Razones:
> - Lotes ya tiene el barco y la cantidad 
> 
