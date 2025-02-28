# MONARCH MODELO 1
```mermaid
erDiagram
    Coordinadores {
        INT id PK
        VARCHAR nombre
        VARCHAR telefono
        VARCHAR id_monarch
        VARCHAR id_telmex
        VARCHAR correo
    }

    Tecnicos {
        INT id PK
        VARCHAR nombre
        VARCHAR contacto
        INT zona_id FK
        VARCHAR NSS
        VARCHAR celular
        VARCHAR marca_auto
        VARCHAR placas
        INT coordinador_id_monarch FK
        INT coord_id_telmex FK
    }

    Tarifas {
        INT id PK
        VARCHAR tipo_servicio
        INT rango_distancia_min
        INT rango_distancia_max
        DECIMAL costo
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
        VARCHAR area
        VARCHAR distrito
        VARCHAR ciudad
        VARCHAR estado
        VARCHAR pais
        VARCHAR codigo_postal
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
        INT id_tipo_bajante FK
    }

    ONT {
        INT id PK
        VARCHAR modelo
        VARCHAR marca
        VARCHAR serie
        INT cantidad_disponible
    }

    TiposBajante {
        INT id PK
        VARCHAR concepto
        DECIMAL precio
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

    Emulacion {
        INT id PK
        INT instalacion_id FK
        BOOL cobrable
        DECIMAL PU
        INT area_id FK
        INT id_tipo_bajante FK
    }

    Tecnicos }|--|| Zonas : "zona_id"
    Clientes }|--|| Zonas : "distrito_id"
    Instalaciones }|--|| Clientes : "cliente_id"
    Instalaciones }|--|| Tecnicos : "tecnico_id"
    Instalaciones }|--|| Tarifas : "tarifa_id"
    Instalaciones }|--|| ONT : "ont_id"
    Instalaciones }|--|| TiposBajante : "id_tipo_bajante"
    FormulariosCaptura }|--|| Tecnicos : "coordinador_id"
    FormulariosCaptura }|--|| ONT : "ont_id"
    FormulariosCaptura }|--|| Instalaciones : "orden_servicio_id"
    Tecnicos }|--|| Coordinadores : "coordinador_id_monarch"
    Tecnicos }|--|| Coordinadores : "coord_id_telmex"
    Emulacion }|--|| Instalaciones : "instalacion_id"
    Emulacion }|--|| Zonas : "area_id"
    Emulacion }|--|| TiposBajante : "id_tipo_bajante"
