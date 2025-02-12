# REST (Representational State Transfer)

- Communication: layered architecture
- A protocol, often used and described with HTTP
- Use links between endpoints to navigate a web API
- Use URL endpoints to provide resources and manipulate resources
- Goal: modifiable and reusable of shared web resources and services, support scalability and availability
- Elements:
  - Web resources identified by URLs (most common URI), always a noun, never verb
    ![URL](assets/url.png)
  - RESTful web services: access to textual representations of web resources with a predefined set of operations
  - Client: invokes a RESTful web service
- Stateless request/response connector: body encoded in xml, json etc (no state info between two requests)
- Requirements
  - Client server (CS)
  - Stateless (CSS) (Each request must contain all info to understand the request, server does not keep a history of old requests)
  - Cacheable (C$SS)
  - Uniform interface (U) (between components: resources are usable across API)
  - Layered system (LS)
  - Code on demand (COD)
- CRUD (methods on resources)
  - Create: POST (Create new resource)
  - Read: GET (Retrieve existing resources) idempotent, safe
  - Update: PUT (Update an existing resource with an identifier) idempotent
  - Delete: DELETE (Delete existing resources) idempotent

## RESTful API: HTTP

- Endpoints: identified by an **URI path** and HTTP method
- Serialization:
  - Object <--> String
  - JSON: JavaScript object notation (human readable, language independent)
    ![status-code](assets/status-code.png)
