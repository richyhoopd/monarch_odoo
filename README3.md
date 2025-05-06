```mermaid
erDiagram

    CLIENTE {
        int id PK
        varchar primer_nombre
        varchar segundo_nombre
        varchar apellido_paterno
        varchar apellido_materno
        varchar curp
        varchar rfc
        varchar telefono_principal
        varchar telefono_alterno
        varchar email
        varchar calle_principal
        varchar calle_secundaria
        varchar numero_exterior
        varchar numero_interior
        varchar colonia
        varchar municipio
        varchar estado
        varchar codigo_postal
        varchar identificacion_anverso
        varchar identificacion_reverso
        varchar comprobante_domicilio
        varchar nip
        varchar tipo_cliente
        int estado_cuenta_id FK
        datetime fecha_registro
    }

    ESTADO_CUENTA {
        int id PK
        date fecha_corte
        varchar semana
        int año
        varchar master
        varchar folio
        decimal saldo_pendiente
        varchar estatus
        int ultimo_pago_id FK
        decimal mora_acumulada
        int dias_vencidos
    }

    ORDEN {
        int id PK
        int cliente_id FK
        varchar folio_siac
        date fecha_venta
        date fecha_instalacion
        varchar estatus
        int promotor_id FK
        int paquete_id FK
        int estrategia_id FK
        decimal importe_total
        boolean portabilidad
        varchar telefono_portar
        varchar observaciones_tecnicas
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
        varchar canal_pago
        varchar autorizacion
    }

    PAQUETE {
        int id PK
        varchar nombre
        varchar codigo
        varchar descripcion
        int tarifa_id FK
        varchar tipo_servicio
        boolean activo
    }

    PERSONAL {
        int id PK
        varchar codigo
        varchar nombre_completo
        varchar telefono
        varchar email
        varchar tipo "PROMOTOR|COORDINADOR"
        varchar division
        varchar distrito
        int coordinador_id FK "Null si es coordinador"
        varchar estatus
        datetime fecha_registro
    }

    ESTRATEGIA_VENTA {
        int id PK
        varchar nombre
        varchar codigo
        varchar proyecto_empresa
        varchar proyecto_estrategia
        date fecha_inicio
        date fecha_fin
        varchar estatus
        decimal meta_ventas
    }

    HISTORIAL_COBRANZA {
        int id PK
        int cliente_id FK
        date fecha_contacto
        varchar medio_contacto
        varchar resultado
        varchar observaciones
        int agente_id FK
        varchar accion_siguiente
        date fecha_proximo_contacto
        varchar nivel_riesgo
    }

    TARIFA {
        int id PK
        varchar codigo
        varchar denominacion
        decimal precio
        varchar estatus
        varchar canales_venta
        int actualizado_por FK
        datetime ultima_actualizacion
        varchar notas
    }

    PRODUCTO {
        int id PK
        varchar nombre
        varchar referencia_interna
        varchar codigo
        int responsable_id FK
        decimal precio_base
        varchar estatus
        varchar especificaciones_tecnicas
    }

    TARIFA_PRODUCTO {
        int tarifa_id FK
        int producto_id FK
        int cantidad
        varchar notas
    }


    CLIENTE ||--o{ ORDEN : "realiza"
    CLIENTE ||--|| ESTADO_CUENTA : "tiene"
    ORDEN ||--|{ PAGO : "genera"
    ORDEN }|--|| PAQUETE : "contiene"
    ORDEN }|--|| PERSONAL : "asignado_a"
    ORDEN }|--|| ESTRATEGIA_VENTA : "asociado_a"
    CLIENTE ||--o{ HISTORIAL_COBRANZA : "registra"
    PERSONAL }|--o{ PERSONAL : "supervisa"
    PAQUETE }|--|| TARIFA : "usa"
    TARIFA ||--|{ TARIFA_PRODUCTO : "incluye"
    PRODUCTO ||--o{ TARIFA_PRODUCTO : "aparece_en"
