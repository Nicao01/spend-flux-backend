sequenceDiagram
participant U as User
participant C as TransactionController
participant S as CreateTransactionService
participant R as TransactionRepository (Port)
participant DB as PostgreSQL
participant E as EventPublisher
participant N as NotificationModule

    U->>C: POST /transactions
    C->>S: createTransaction(request)
    S->>R: save(transaction)
    R->>DB: INSERT transaction
    DB-->>R: success
    R-->>S: transaction saved
    S->>E: publish(TransactionCreatedEvent)
    E->>N: onTransactionCreated(event)
    N->>U: Send notification (email/sms)
