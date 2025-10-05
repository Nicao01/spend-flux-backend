# SpendFlux - C4 Level 1 (Context)

```mermaid

C4Container
    title SpendFlux - C4 Model Level 2 (Containers)

    Person(user, "User", "A person who interacts with SpendFlux")

    System_Boundary(spendflux, "SpendFlux") {
        Container(api, "REST API (Spring Boot)", "Java + Spring Boot", "Exposes REST endpoints for all modules")
        
        Container_Boundary(modules, "Internal Modules") {
            Container(auth, "Auth Module", "Spring Security + JWT", "Handles authentication and authorization")
            Container(userModule, "User Module", "Java + JPA", "Manages user accounts")
            Container(category, "Category Module", "Java + JPA", "Manages categories")
            Container(transaction, "Transaction Module", "Java + JPA", "Handles transactions and publishes domain events")
            Container(notification, "Notification Module", "Java", "Listens to events and sends notifications")
        }

        ContainerDb(db, "PostgreSQL", "Relational Database", "Schemas separated by module")
    }

    System_Ext(emailService, "Email Service", "External service for sending notifications")

    Rel(user, api, "Interacts via HTTP/JSON")
    Rel(api, auth, "Delegates authentication")
    Rel(api, userModule, "CRUD operations on users")
    Rel(api, category, "CRUD operations on categories")
    Rel(api, transaction, "CRUD operations on transactions")
    Rel(transaction, notification, "Publishes events to")
    Rel(notification, emailService, "Sends notifications via")
    Rel(auth, db, "Stores data in")
    Rel(userModule, db, "Stores data in")
    Rel(category, db, "Stores data in")
    Rel(transaction, db, "Stores data in")
    Rel(notification, db, "Stores logs in")