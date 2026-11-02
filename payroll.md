mermaid'''
erDiagram
    COMPANIES ||--o{ EMPLOYEES : employs
    COMPANIES ||--o{ PAYROLL_RUNS : processes

    EMPLOYEES ||--o{ COMPENSATION : has
    EMPLOYEES ||--o{ TIME_ENTRIES : records
    EMPLOYEES ||--o{ PAYROLL_ITEMS : receives

    PAYROLL_RUNS ||--o{ PAYROLL_ITEMS : contains
    PAYROLL_ITEMS ||--o{ TAX_CALCULATIONS : includes
    PAYROLL_ITEMS ||--o{ PAYMENTS : generates

    LEDGER_TRANSACTIONS ||--|{ LEDGER_ENTRIES : contains
    PAYMENTS o|--o{ LEDGER_TRANSACTIONS : records

    COMPANIES {
        uuid company_id PK
        string name
        string status
    }

    EMPLOYEES {
        uuid employee_id PK
        uuid company_id FK
        string employment_status
    }

    COMPENSATION {
        uuid compensation_id PK
        uuid employee_id FK
        decimal pay_rate
        date effective_from
    }

    TIME_ENTRIES {
        uuid time_entry_id PK
        uuid employee_id FK
        decimal hours
        string approval_status
    }

    PAYROLL_RUNS {
        uuid run_id PK
        uuid company_id FK
        string period_id
        string state
        int version
    }

    PAYROLL_ITEMS {
        uuid item_id PK
        uuid run_id FK
        uuid employee_id FK
        decimal gross
        decimal taxes
        decimal net
    }

    TAX_CALCULATIONS {
        uuid tax_calculation_id PK
        uuid item_id FK
        string jurisdiction
        decimal amount
        string rule_version
    }

    PAYMENTS {
        uuid payment_id PK
        uuid item_id FK
        decimal amount
        string state
        string idempotency_key
    }

    LEDGER_TRANSACTIONS {
        uuid transaction_id PK
        uuid payment_id FK
        string transaction_type
        string status
    }

    LEDGER_ENTRIES {
        uuid entry_id PK
        uuid transaction_id FK
        uuid account_id FK
        decimal debit
        decimal credit
    }
    '''
