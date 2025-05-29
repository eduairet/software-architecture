# Advance Architecture Topics

## Microservices Architecture

An Architecture in which various functionalities are implemented separately as independent services, which communicate with each other over a network.

- Each service runs in its own process and does not impact other services.
- Each service can be updated separately.
- Each service can be implemented using different technologies.
- Each service can be optimized separately.

## Event Sourcing

Event Sourcing is a pattern where the state of an application is determined by a sequence of events. Instead of storing the current state, all changes to the state are stored as a sequence of events.

- Each event represents a change in the state of the application.
- The current state can be reconstructed by replaying the events.
- Event Sourcing is often used in conjunction with CQRS (Command Query Responsibility Segregation) to separate the read and write operations.

| Pros                                                                      | Cons                         |
| ------------------------------------------------------------------------- | ---------------------------- |
| Tracing: Easy to trace the history of changes.                            | No unified view of the data. |
| Simple Data Model: No need to maintain complex entities or relationships. | It uses a lot of storage.    |
| Performance: All you need to do is append events to the database.         |                              |
| Reporting: Te history is already available in the data                    |                              |

## CQRS (Command Query Responsibility Segregation)

CQRS stands for Command Query Responsibility Segregation. It is a pattern that separates the read and write operations of an application.

- Commands are used to change the state of the application.
- Queries are used to read the state of the application.
- Commands and Queries are handled by different models.
- I needs two different data stores: one for data storage and one for data retrieval interconnected with a synchronization service.
- The ideal use case for this pattern is with high frequency updates that require near real-time data retrieval like telemetry systems (e.g. IoT systems or stock trading systems).
