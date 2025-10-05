# SpendFlux - C4 Level 1 (Context)

```mermaid

C4Component
title Transaction Module - C4 Model Level 3 (Components)

    Container_Boundary(transaction, "Transaction Module") {
        
        Component(domain, "Domain Layer", "Entities + Events", "Contains Transaction entity and TransactionCreatedEvent")
        Component(application, "Application Layer", "Use Cases + Ports", "Defines use cases and ports for repository and event publishing")
        Component(infrastructure, "Infrastructure Layer", "Adapters", "Implements REST controllers, JPA repositories, and event publishers")
    }

    Rel(domain, application, "Business rules invoked by")
    Rel(application, infrastructure, "Uses adapters implemented in")
    Rel(infrastructure, application, "Implements ports defined in")
