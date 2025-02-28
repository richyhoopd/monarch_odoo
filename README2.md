```mermaid
flowchart TD
    A[Inicio] --> A1[Técnico completa instalación]
    A1 --> A2[Se toma la foto de ONT]
    A2 --> A3[Se llena hoja en físico]
    A3 --> B[Captura de datos en formulario de captura]
    B --> C[Vaciar información en BD]
    C --> D{Bajante es ZTE?}
    D -- Sí --> E[Poner bajante ZTE = 1]
    D -- No --> F[Poner bajante ZTE = 0]
    E --> G{Todos los campos son correctos?}
    F --> G
    G -- Sí --> H{Bajante es fibra óptica?}
    G -- No --> G1[Esperar corrección de campos]
    G1 --> G
    H -- Sí --> I[Mostrar opciones de 25m en 25m hasta 250m]
    H -- No --> J[Pedir ingreso manual de metraje cobre]
    I --> K{Metraje excede 300m?}
    J --> K
    K -- Sí --> L[Solicitar tarifa extra por metro]
    L --> L1[Añadir pago extra al técnico por instalación grande]
    L1 --> M[Generar registro en tabla de emulaciones]
    K -- No --> M[Generar registro en tabla de emulaciones]
    M --> N[Enviar emulación por correo en formato Excel plano]
    N --> O[Esperar respuesta]
    O --> P{Monto a pagar coincide?}
    P -- Sí --> Q[Mandar emulación al histórico]
    P -- No --> R[Notificar a área de facturación]
    Q --> S[Fin]
    R --> S[Fin]
