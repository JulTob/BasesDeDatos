
# Tema 1


### Ejemplo: Modelo Entidad Relación Extendido (ERE)

Obtener el esquema conceptual correspondiente a las salas de un hospital:
a. En una clínica se lleva un registro de pacientes, un registro de personal y uno de
salas con el personal que trabajan en esas salas y con los pacientes internados en
dichas salas.
b. Del personal nos interesa el número de empleado, el nombre, la dirección y el
teléfono. Sabemos que dos empleados no tienen el mismo numero.
c. De los pacientes nos interesa el número de registro (que les es asignado cuando
ingresan, diferente para cada uno de ellos) y el nombre, mientras que de las salas
nos interesa el nombre y la cantidad de camas que tiene. Nos indican que dos
salas no tienen el mismo nombre.
d. También se sabe que un empleado trabaja en una única sala, pero en una sala
pueden trabajar varios empleados.
e. Con los pacientes ocurre igual, es decir un paciente está en una única sala, pero en
una sala pueden estar ingresados varios pacientes.



```mermaid
---
config:
  theme: 'base'
  themeVariables:
    background: '#fff'
---
graph LR
  subgraph Hospital
    direction TB
    subgraph Personal
      direction TB
      tP(telefono) & dP(Dirección) & nP(Número) & nmP(Nombre)
      end
    subgraph paciente
      direction TB
      nPc(N Registro) & nmPc(Nombre)
      end    
    sala[Sala]
    trabaja{Trabaja En}
    internado{Internado En}
    end

    Personal --> trabaja --> sala
    paciente --> internado --> sala
    Software <--> data



    paciente:::rojo
    Personal:::azul
    sala:::verde
    trabaja:::amarillo
    internado:::cian

    classDef rojo color:#800, stroke:#f00, stroke-width:4px, fill:#FAA
    classDef azul color:#008, stroke:#00f, stroke-width:4px, fill:#AAF
    classDef verde color:#080, stroke:#0f0, stroke-width:4px, fill:#AFA
    classDef amarillo color:#880, stroke:#ff0, stroke-width:4px, fill:#FFA
    classDef cian color:#088, stroke:#0ff, stroke-width:4px, fill:#AFF
```




