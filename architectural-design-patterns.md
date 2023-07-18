# Architectural Design Patterns

Speaker: Daniel Hinojosa

[Workshop Repository](https://github.com/dhinojosa/architectural-design-patterns/)

- [Architectural Design Patterns](#architectural-design-patterns)
  - [Hexagonal Architecture](#hexagonal-architecture)
  - [Domain Driven Design](#domain-driven-design)
  - [Bounded Context Interaction](#bounded-context-interaction)
    - [Partnership](#partnership)
    - [Shared Kernel](#shared-kernel)
    - [Customer-Supplier](#customer-supplier)
    - [Conformist](#conformist)
    - [Anti-Corruption Layer](#anti-corruption-layer)
    - [Open-Host Service](#open-host-service)
  - [Design Patterns](#design-patterns)
    - [Circuit Breaker](#circuit-breaker)
    - [Retry](#retry)
    - [Bulkhead](#bulkhead)
    - [Ambassador](#ambassador)
    - [Event Sourcing](#event-sourcing)
    - [Competing Consumers](#competing-consumers)
    - [Claim Check](#claim-check)
    - [Materialized View](#materialized-view)
    - [CQRS](#cqrs)
    - [Strangler Fig](#strangler-fig)
    - [Gatekeeper](#gatekeeper)
    - [Valet Key](#valet-key)
    - [Data Mesh](#data-mesh)
    - [Saga](#saga)
  - [Other Resources](#other-resources)
    - [References](#references)
    - [Libraries](#libraries)

## Hexagonal Architecture

- aka Ports and Adapters
- Decouple business logic from infrastructure
- Separation of concerns, domain is encapsulated
- Adapters are concrete implementations in the infrastructure layer
- Ports are interfaces to the outside world, accepting interaction from the adapters

## Domain Driven Design

- Focused on the importance of the domain
- Build a *ubiquitous language* for domain
  - Define the terms of your domain
  - Language of your business
  - Precise and  consistent
- Classifies objects into:
  - Entities
    - Explicit identification required
  - Aggregates
    - Manages a collection of domain object
    - Transactions should not cross aggregate boundaries
  - Value Objects
    - Immutable
  - Domain Events
  - Service Objects
    - Stateless objects that implement the business logic
    - Domain services act on domain objects across boundaries
    - Application services make use of repositories and route to the UI
- Notion of bounded context and subdomains

## Bounded Context Interaction

Each context can interact with each other via interfaces within the same application or using a port/adapter pattern

### Partnership

- One team notifies anothers about API changes and the second team will adapt
- Two way coordination between contexts
- Bad fit for geographically distributed teams
- Good CI/CD is needed

### Shared Kernel

- Cases when the same model of a subdoamin will be implemented in multiple bounded contexts
- Shared model needs to be consistent across all contexts

### Customer-Supplier

- Supplier provides services to the customer
- Both can succeed independently
- Imbalance of power, either the supplier dictates the terms or the customer does

### Conformist

- The upstream system doesn't care about the customer's needs
- Upstream may be an industry standard, well-established model, or legacy

### Anti-Corruption Layer

- Similar to conformist, but acts as a layer in-between the supplier and consumer to handle changes
- Translates interactions between the suppliers and customer

### Open-Host Service

- Customer is in control
- Supplier must provide multiple public interfaces customized for the customer
- Done by decoupling the implementation from the public interfaces

## Design Patterns

### Circuit Breaker

- Problem: When a service synchronously requests from a remote call there is a big possibility of failure
- Solution: Client invokes the remote service by proxy
  - When the number of consecutive failures crosses a threshold, the circuit trips
  - Block all further requests (Open State)
  - After a set timeout, let in limited requests to test the service health (Half-Open state)
  - If service is healthy, let all requests through again (Closed state)
- You must handle the exceptions thrown by the circuit breaker and log all requests for health monitoring
- Shouldn't be used for private resources that you control (e.g. in-memory dbs)

### Retry

- Problem: There can be transient faults when it comes to networking application (e.g. network issues, extrernal system failure, rate limits)
- Solution: Retry the request
  - Cancel and log the request
  - Retry the request immediately
  - Retry after a delay and repeat as necessary or up to a maximum number of attempts
- You should log all requests and retries for health monitoring

### Bulkhead

- Problem: Tasks of a threaded application exhaust all of the resources available, starving out other tasks
- Solution: Partition service instances into groups based on consumer load and availability requirements
  - Isolate resources between tasks, so greedy tasks can starve others out
  - Protects from cascading failures
  - Perfect for isolating critical consumers from standard consumers
- Adds complexity to the system

### Ambassador

- Problem: Applications require a multitude of services like Circuit Breaker, Metering, etc.
- Solution: Use a proxy for your application to external services
  - Monitors performance such as latency and resource usage
  - You can make updates to the ambassador without affecting the legacy application
  - Can be done as a sidecar to the application
- Solution is better of integrated into the application itself, but that isn't always possible
- Expect some minor latency overhead

### Event Sourcing

- Problem: In typical CRUD databases you can only see a snapshot in time, as opposed to all the transactions that occurred
- Solution: Events are recorded in an append only store
  - Events are described discretely in past tense (e.g. AddedItemToCart, ClearedCart)
  - Can be used to prepare the data for the purposes of being efficiently read by a UI or business analytics for consumption
- Eventually consistent, immediately real-time consistency is not available
- If you do not require audit trails, history, and rollbacks, it might be overkill
- If you do not expect a lot of conflicts, it might be overkill

### Competing Consumers

- Problem: You require constant processing of a number of requests and using a single instance can be problematic
- Solution: Use a message queue or pub/sub to send message over to the consumer
  - Each consumer can process the message that does not interfere with other consumers
  - Consumers become fault tolerant
- It may not be easy to separate the application workload into discrete tasks
- May be problematic if tasks must be performed synchronously or in a particular sequence

### Claim Check

- Problem: Many messaging applications can't accept really large payloads (i.e. entire records)
- Solution: Store the message payload in external storage and send a reference to it instead
  - Consumer retrieves the payload from storage using the reference

### Materialized View

- Problem: Entities can have too much information to be usable and much of the design revolves around how it is stored, not how it is read
- Solution: Create a different perspective for the data you need
- If immediate consistency is required, then query directly

### CQRS

- aka Command and Query Responsiblity Segregation
- Problem: There is often a mismatch between the read and write representations of data
- Solution: Separate reads and updates for a database
  - Use commands to update data, and queries to read data
  - Commands should be task-based and can be processed asynchronously
  - Queries never modify the database
  - Improves performance, scalability, and security
  - Better evolution over time
  - Prevents merge conflics

### Strangler Fig

- Problem: You have a legacy application that you'd like to replace
- Solution: Create a façade called the Strangler Facade which will intercept requests
  - The façade routes the requests to the new services if implemented, otherwise falls back to the legacy app
  - Existing features can be migrated to the new system gradually and consumers use the same interface
  - Can easily rollback to legacy because it was not modified directly
  - Another flavor of a Canary Deployment
- Need to ensure the façade doesn't become a bottleneck

### Gatekeeper

- Problem: Services may have potentially sensitive information that could be useful to hackers
- Solution: Create a façade that will be entry point of all requests
  - Accepts requests
  - Sanitizes the requests
  - Validates the requests
  - Mutates the requests

### Valet Key

- Problem: Needing a middleman for securely interacting with storage accounts
- Solution: Provide a key or secret that can be used by the service to securely interact with the storage account directly

### Data Mesh

- Problem: Data can be siloed into database per service or consumer
- Solution: Create a data lake or shared database
  - Domain-oriented decentralized data ownership and architecture
  - Data as a product
  - Self-serve data infrastructure as a platform
  - Federated computational governance
- The accountability of data quality shifts upstream as close to the source of the data as possible

### Saga

- Problem: We require distributed transactions across services through events
- Solution: Choreography or Orchestration
  - Choreography-based patterns require that each service understands it's part and how to handle success and failure
  - Orchestration-based patterns use a separate service to manage the state of the transaction, handles errors, and coordinates the other services
- No perfect solution for this
- Hard to achieve fully

## Other Resources

### References

- [Refactoring to Testable Code](https://moretestable.com/)
- [Catalog of Design Patterns](https://learn.microsoft.com/en-us/azure/architecture/patterns/#catalog-of-patterns)

### Libraries

- [ArchUnit: Unit test your Java architecture](https://www.archunit.org/)
- [Squants: The Scala API for Quantities, Units of Measure and Dimensional Analysis](https://github.com/typelevel/squants)
- [Resilience4j: a lightweight fault tolerance library designed for functional programming](https://resilience4j.readme.io/docs)
- [Open Policy Agent: Policy-based control for cloud native environments](https://www.openpolicyagent.org/)
