# SpendFlux - C4 Level 1 (Context)

```mermaid
C4Context
    title SpendFlux - C4 Model Level 1 (System Context)

    Person(user, "User", "A person who uses SpendFlux to manage personal finances")
    System(spendflux, "SpendFlux", "Personal finance management system")

    System_Ext(emailService, "Email Service", "External service for sending notifications")
    SystemDb_Ext(postgres, "PostgreSQL", "Relational database with separated schemas per module")

    Rel(user, spendflux, "Uses")
    Rel(spendflux, emailService, "Sends notifications via")
    Rel(spendflux, postgres, "Stores data in")
