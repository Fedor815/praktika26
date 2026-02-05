# Entity Relationship Diagram (ERD) базы данных

```mermaid
erDiagram
    USERS ||--o{ APPOINTMENTS : "имеет"
    DOCTORS ||--o{ APPOINTMENTS : "принимает"
    DOCTORS ||--o{ SPECIALIZATIONS : "имеет"
    DOCTORS ||--o{ SCHEDULES : "имеет"
    CLINICS ||--o{ DOCTORS : "работает в"
    
    USERS {
        int id PK
        string email UK
        string password_hash
        string full_name
        string role "patient|doctor|admin"
        timestamp created_at
    }
    
    DOCTORS {
        int id PK
        int user_id FK
        int clinic_id FK
        string specialization
        int experience_years
        decimal rating
        string bio
    }
    
    APPOINTMENTS {
        int id PK
        int patient_id FK
        int doctor_id FK
        datetime appointment_date
        string status "scheduled|completed|cancelled"
        string notes
        timestamp created_at
    }
    
    CLINICS {
        int id PK
        string name
        string address
        string phone
        string email
    }
    
    SPECIALIZATIONS {
        int id PK
        string name
        string description
    }
    
    SCHEDULES {
        int id PK
        int doctor_id FK
        date work_date
        time start_time
        time end_time
        boolean is_available
    }