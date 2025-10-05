erDiagram
AUTH_SCHEMA.USERS_CREDENTIALS {
UUID id PK
VARCHAR username
VARCHAR password_hash
VARCHAR role
}

    USER_SCHEMA.USERS {
        UUID id PK
        VARCHAR name
        VARCHAR email
        TIMESTAMP created_at
    }

    CATEGORY_SCHEMA.CATEGORIES {
        UUID id PK
        VARCHAR name
        VARCHAR description
    }

    TRANSACTION_SCHEMA.TRANSACTIONS {
        UUID id PK
        UUID user_id FK
        UUID category_id FK
        DECIMAL amount
        TIMESTAMP created_at
        VARCHAR description
    }

    NOTIFICATION_SCHEMA.NOTIFICATIONS_LOG {
        UUID id PK
        UUID user_id FK
        VARCHAR message
        TIMESTAMP sent_at
    }

    %% Relationships
    USER_SCHEMA.USERS ||--o{ TRANSACTION_SCHEMA.TRANSACTIONS : "creates"
    CATEGORY_SCHEMA.CATEGORIES ||--o{ TRANSACTION_SCHEMA.TRANSACTIONS : "categorizes"
    USER_SCHEMA.USERS ||--o{ NOTIFICATION_SCHEMA.NOTIFICATIONS_LOG : "receives"
    AUTH_SCHEMA.USERS_CREDENTIALS ||--|| USER_SCHEMA.USERS : "authenticates"
