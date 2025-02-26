#MONARCH ODO RELATIONAL MODEL

```mermaid
erDiagram
    Tecnicos {
        INT id PK
        VARCHAR(255) nombre
        VARCHAR(255) contacto
        INT zona_id FK
    }

    Tarifas {
        INT id PK
        VARCHAR(255) tipo_servicio
        INT rango_distancia_min
        INT rango_distancia_max
        DECIMAL(10,2) costo
    }

    Almacen {
        INT id PK
        VARCHAR(255) nombre_material
        TEXT descripcion
        VARCHAR(50) unidad_medida
        INT cantidad
        INT proveedor_id FK
    }

    Clientes {
        INT id PK
        VARCHAR(255) nombre
        VARCHAR(255) direccion
        VARCHAR(255) contacto
        INT distrito_id FK
    }

    Zonas {
        INT id PK
        VARCHAR(255) nombre
        VARCHAR(255) distrito
        VARCHAR(255) ciudad
        VARCHAR(255) estado
        VARCHAR(255) pais
    }

    Instalaciones {
        INT id PK
        INT cliente_id FK
        INT tecnico_id FK
        INT tarifa_id FK
        DATE fecha
        VARCHAR(50) estado
        ENUM('Cobre', 'Fibra') tecnologia
        VARCHAR(255) terminal
        VARCHAR(255) puerto
        INT ont_id FK
        INT distancia_mts
        VARCHAR(255) tipo_construccion
    }

    UsoMateriales {
        INT id PK
        INT instalacion_id FK
        INT material_id FK
        INT cantidad_usada
    }

    ONT {
        INT id PK
        VARCHAR(255) modelo
        VARCHAR(255) marca
        VARCHAR(255) serie
        TEXT foto_ont
    }

    Proveedores {
        INT id PK
        VARCHAR(255) nombre
        VARCHAR(255) contacto
        VARCHAR(255) direccion
    }

    FormulariosCaptura {
        INT id PK
        DATE fecha
        VARCHAR(255) correo_electronico
        INT coordinador_id FK
        VARCHAR(255) expediente_tecnico
        VARCHAR(255) folio_pisa
        TEXT foto_orden
        INT ont_id FK
        INT bajante_total
        TEXT foto_ont
        INT unifibra
        INT bajante_zte
        VARCHAR(255) num_modem_ont
        INT orden_servicio_id FK
    }

    Tecnicos }|--|| Zonas : zona_id
    Clientes }|--|| Zonas : distrito_id
    Almacen }|--|| Proveedores : proveedor_id
    Instalaciones }|--|| Clientes : cliente_id
    Instalaciones }|--|| Tecnicos : tecnico_id
    Instalaciones }|--|| Tarifas : tarifa_id
    Instalaciones }|--|| ONT : ont_id
    UsoMateriales }|--|| Instalaciones : instalacion_id
    UsoMateriales }|--|| Almacen : material_id
    FormulariosCaptura }|--|| Tecnicos : coordinador_id
    FormulariosCaptura }|--|| ONT : ont_id
    FormulariosCaptura }|--|| Instalaciones : orden_servicio_id
