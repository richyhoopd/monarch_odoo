# MONARCH MODELO 1
```mermaid
erDiagram
    Coordinators {
        INT id PK
        VARCHAR name
        VARCHAR phone
        VARCHAR monarch_id
        VARCHAR telmex_id
        VARCHAR email
    }

    Technicians {
        INT id PK
        VARCHAR name
        VARCHAR contact
        INT zone_id FK
        VARCHAR NSS
        VARCHAR mobile
        VARCHAR car_brand
        VARCHAR license_plate
        INT monarch_coordinator_id FK
        INT telmex_coordinator_id FK
    }

    Rates {
        INT id PK
        VARCHAR service_type
        INT min_distance_range
        INT max_distance_range
        DECIMAL cost
    }

    Customers {
        INT id PK
        VARCHAR name
        VARCHAR address
        VARCHAR contact
        INT district_id FK
    }

    Zones {
        INT id PK
        VARCHAR area
        VARCHAR district
        VARCHAR city
        VARCHAR state
        VARCHAR country
        VARCHAR postal_code
    }

    Installations {
        INT id PK
        INT customer_id FK
        INT technician_id FK
        INT rate_id FK
        DATE date
        VARCHAR status
        ENUM technology
        VARCHAR terminal
        VARCHAR port
        INT ont_id FK
        INT distance_mts
        VARCHAR construction_type
        INT drop_type_id FK
    }

    ONT {
        INT id PK
        VARCHAR model
        VARCHAR brand
        VARCHAR serial
        INT available_quantity
    }

    DropTypes {
        INT id PK
        VARCHAR concept
        DECIMAL price
    }

    CaptureForms {
        INT id PK
        DATE date
        VARCHAR email
        INT coordinator_id FK
        VARCHAR technical_file
        VARCHAR folio_pisa
        TEXT order_photo
        INT ont_id FK
        INT total_drop
        TEXT ont_photo
        INT unifiber
        INT zte_drop
        VARCHAR modem_ont_number
        INT service_order_id FK
    }

    Emulation {
        INT id PK
        INT installation_id FK
        BOOL chargeable
        DECIMAL unit_price
        INT area_id FK
        INT drop_type_id FK
    }

    Technicians }|--|| Zones : "zone_id"
    Customers }|--|| Zones : "district_id"
    Installations }|--|| Customers : "customer_id"
    Installations }|--|| Technicians : "technician_id"
    Installations }|--|| Rates : "rate_id"
    Installations }|--|| ONT : "ont_id"
    Installations }|--|| DropTypes : "drop_type_id"
    CaptureForms }|--|| Technicians : "coordinator_id"
    CaptureForms }|--|| ONT : "ont_id"
    CaptureForms }|--|| Installations : "service_order_id"
    Technicians }|--|| Coordinators : "monarch_coordinator_id"
    Technicians }|--|| Coordinators : "telmex_coordinator_id"
    Emulation }|--|| Installations : "installation_id"
    Emulation }|--|| Zones : "area_id"
    Emulation }|--|| DropTypes : "drop_type_id"
