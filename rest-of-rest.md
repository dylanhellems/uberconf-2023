# A Developer's Guide to the Rest of Rest

Speaker: Michael Carducci

- [A Developer's Guide to the Rest of Rest](#a-developers-guide-to-the-rest-of-rest)
  - [What is REST?](#what-is-rest)
    - [Categories of Educational Content](#categories-of-educational-content)
    - [REST is *an* architecture](#rest-is-an-architecture)
    - [Architecture as a set of constraints](#architecture-as-a-set-of-constraints)
    - [Richardson Maturity Model](#richardson-maturity-model)
    - [Concepts](#concepts)
  - [Pattern-Driven API Evolution](#pattern-driven-api-evolution)
    - [Level Zero API Example](#level-zero-api-example)
    - [URIs](#uris)
    - [Level One/Two API Example](#level-onetwo-api-example)
    - [Serialization and Syntax/Shape](#serialization-and-syntaxshape)
    - [Child and Related Resources](#child-and-related-resources)
    - [Other Useful Identifier Patterns](#other-useful-identifier-patterns)
    - [Level Three API](#level-three-api)
  - [Other Resources](#other-resources)
    - [References](#references)

## What is REST?

The meaning has evolved over time from its original definition due to innovation, misunderstanding, and misuse

### Categories of Educational Content

- Beginners summarizing a concept they've just learned
- Experts producing a synthesis of deep ideas they've explored
- Biased engineers publishing content to validate their biases

### REST is *an* architecture

>"Architecture is the important stuff... whatever that is" - Martin Fowler

- REST is the architecture of the World-Wide Web
- Functional requirements are your ante (what gets you into the game), but the architecture is everything else (e.g. -ilities)
- There are no "Silver Bullet" solutions
- There are no good or bad architectures, just tradeoffs

### Architecture as a set of constraints

> “The REST interface is designed to be efficient for large-grain hypermedia data transfer, optimizing for the common case of the Web, but resulting in an interface that is not optimal for other forms of architectural interaction.” - Dr. Roy Fielding

- SOLID Principles
  - Single Responsibility
  - Open/Closed
  - Liskov Substitution
  - Interface Segregation
  - Dependency Inversion
- REST
  - Start with "Null Architecture" and add constraints
    - Client-server
    - Stateless
    - Cache
    - Uniform Interface
      - Resource abstraction
      - Stable identification of resources
      - Manipulation of resources via representations
      - Self-describing messages
      - Semantically constrained actions
      - HATEOS
    - Layered System
    - Code-on-demand

### Richardson Maturity Model

- Level 0: POX Swamp
  - Plain old XML
- Level 1: URI
  - Multiple URI-based resources and single verbs
- Level 2: HTTP
  - Interactions with URI resources using different HTTP verbs
- Level 3: Hypermedia or REST
  - HATEOS

### Concepts

- Resource
  - The atomic building-blocks of information. Physical virtual, or conceptual entities important enough to be named and potentially connected
- Identity
  - A globally scoped, unique, stable identifier for a resource; a URI
- Representation
  - The syntax, serialization, shape, and/or format of a resource that is most useful to the client
- Semantics
  - The meaning and behavior of the resource, the data describing the resource, and the request/operation semantics
- Behavior
  - The functional capabilities of the server software
- Implementation
  - The specific software, platform, framework, OS, etc. of the server

## Pattern-Driven API Evolution

### Level Zero API Example

`GET http://example.com/api/v1/json/getPersonById.php?id=1234`

- Representation bleeding into URI (`/json/`)
- RPC endpoint, not resource identifier (`getPersonById`)
- Implementation details bleeding into URI (`.php`)

### URIs

- Identity Scheme Properties
  - Identity
  - Disambiguation
  - Scope
  - Resolvability
- Literal Keys Pattern
  - Create URIs from existing non-global identifiers (e.g. db keys)
- Pattern URIs
  - Create URIs using a common pattern so it can be easily remembered and algorithmically constructed
- Hierarchical URIs
  - Create URIs using the natural hierarchy of resources
- Be consistent

### Level One/Two API Example

`GET http://example.com/person/id/1234`

- Hierarchical pattern (`/person/id/`)
- Natural key (`1234`)

### Serialization and Syntax/Shape

- Content Negotiation Pattern
  - Allows the user agent to decide which representation of any given resource is best suited for them
  - Decouples resource representation, syntax, serialization, behavior, and implementation
  - Stable abstraction
  - Versioning
  - Language support
  - Client-specific optimizations

### Child and Related Resources

- XHIBIT Antipattern
  - `GET http://example.com/job-history/person/http://example.com/person/id/1234`
  - Level 0 API disguised as Level 1

- RESTful related resource
  - `GET http://example.com/job-history/person/http://example.com/person/id/1234`

### Other Useful Identifier Patterns

- URI Slugs
- Proxy URIs
  - Treat third-party resources like your own data
- Rebased Identifier

### Level Three API

To be truly RESTful, an API must be self-describing and not need documentation to understand or use

## Other Resources

### References

- [Architectural Styles and the Design of Network-based Software Architectures](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
