# MONARCH MODELO 1
```mermaid
erDiagram
    Tecnicos {
        INT id PK
        VARCHAR nombre
        VARCHAR contacto
        INT zona_id FK
    }

    Tarifas {
        INT id PK
        VARCHAR tipo_servicio
        INT rango_distancia_min
        INT rango_distancia_max
        DECIMAL costo
    }

    Almacen {
        INT id PK
        VARCHAR nombre_material
        TEXT descripcion
        VARCHAR unidad_medida
        INT cantidad
        INT proveedor_id FK
    }

    Clientes {
        INT id PK
        VARCHAR nombre
        VARCHAR direccion
        VARCHAR contacto
        INT distrito_id FK
    }

    Zonas {
        INT id PK
        VARCHAR nombre
        VARCHAR distrito
        VARCHAR ciudad
        VARCHAR estado
        VARCHAR pais
    }

    Instalaciones {
        INT id PK
        INT cliente_id FK
        INT tecnico_id FK
        INT tarifa_id FK
        DATE fecha
        VARCHAR estado
        ENUM tecnologia
        VARCHAR terminal
        VARCHAR puerto
        INT ont_id FK
        INT distancia_mts
        VARCHAR tipo_construccion
    }

    UsoMateriales {
        INT id PK
        INT instalacion_id FK
        INT material_id FK
        INT cantidad_usada
    }

    ONT {
        INT id PK
        VARCHAR modelo
        VARCHAR marca
        VARCHAR serie
        TEXT foto_ont
    }

    Proveedores {
        INT id PK
        VARCHAR nombre
        VARCHAR contacto
        VARCHAR direccion
    }

    FormulariosCaptura {
        INT id PK
        DATE fecha
        VARCHAR correo_electronico
        INT coordinador_id FK
        VARCHAR expediente_tecnico
        VARCHAR folio_pisa
        TEXT foto_orden
        INT ont_id FK
        INT bajante_total
        TEXT foto_ont
        INT unifibra
        INT bajante_zte
        VARCHAR num_modem_ont
        INT orden_servicio_id FK
    }

    Tecnicos }|--|| Zonas : "zona_id"
    Clientes }|--|| Zonas : "distrito_id"
    Almacen }|--|| Proveedores : "proveedor_id"
    Instalaciones }|--|| Clientes : "cliente_id"
    Instalaciones }|--|| Tecnicos : "tecnico_id"
    Instalaciones }|--|| Tarifas : "tarifa_id"
    Instalaciones }|--|| ONT : "ont_id"
    UsoMateriales }|--|| Instalaciones : "instalacion_id"
    UsoMateriales }|--|| Almacen : "material_id"
    FormulariosCaptura }|--|| Tecnicos : "coordinador_id"
    FormulariosCaptura }|--|| ONT : "ont_id"
    FormulariosCaptura }|--|| Instalaciones : "orden_servicio_id"
