erDiagram

    CLIENTE {
        int id PK
        varchar nombre
        varchar rfc
        varchar telefono
        varchar email
        int direccion_id FK
        int estado_cuenta_id FK
        datetime fecha_registro
    }

    DIRECCION {
        int id PK
        varchar calle
        varchar numero
        varchar colonia
        varchar ciudad
        varchar estado
        varchar codigo_postal
    }

    ESTADO_CUENTA {
        int id PK
        date fecha_corte
        varchar semana
        int año
        decimal saldo_pendiente
        varchar estatus
        int ultimo_pago_id FK
    }

    ORDEN {
        int id PK
        int cliente_id FK
        varchar folio
        date fecha_venta
        date fecha_instalacion
        varchar estatus
        int promotor_id FK
        int paquete_id FK
        int estrategia_id FK
        decimal importe_total
    }

    PAGO {
        int id PK
        int orden_id FK
        date fecha_pago
        decimal monto
        varchar metodo_pago
        varchar referencia
        varchar estatus
        varchar observaciones
    }

    PAQUETE {
        int id PK
        varchar nombre
        varchar tipo_linea
        varchar descripcion
        decimal costo_mensual
    }

    PROMOTOR {
        int id PK
        varchar nombre
        varchar telefono
        varchar email
        int supervisor_id FK
    }

    ESTRATEGIA_VENTA {
        int id PK
        varchar nombre
        varchar proyecto
        date fecha_inicio
        date fecha_fin
        varchar estatus
    }

    INVENTARIO {
        int id PK
        varchar tipo_equipo
        varchar modelo
        varchar serie
        varchar estatus
        int orden_id FK
    }

    HISTORIAL_COBRANZA {
        int id PK
        int cliente_id FK
        date fecha_contacto
        varchar medio_contacto
        varchar resultado
        varchar observaciones
        int agente_id FK
    }

    %% Relaciones mejoradas
    CLIENTE ||--o{ ORDEN : "realiza"
    CLIENTE ||--|{ DIRECCION : "tiene"
    CLIENTE ||--|| ESTADO_CUENTA : "tiene"
    ORDEN ||--|{ PAGO : "genera"
    ORDEN }|--|| PAQUETE : "contiene"
    ORDEN }|--|| PROMOTOR : "asignado_a"
    ORDEN }|--|| ESTRATEGIA_VENTA : "asociado_a"
    ORDEN ||--o{ INVENTARIO : "utiliza"
    CLIENTE ||--o{ HISTORIAL_COBRANZA : "registra"
    PROMOTOR }|--|| PROMOTOR : "supervisado_por"
