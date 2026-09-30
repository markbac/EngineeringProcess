# Interface Specification Template

Use this template to define software, message, hardware, or network interfaces across components, products, or external systems.

```yaml
---
id: INT-0000
name: Interface Name
owner: Team or Role
version: 1.0.0
status: proposed # Options: proposed | active | deprecated | retired
type: rest-openapi # Options: rest-openapi | asyncapi | grpc-protobuf | graphql | ipc-idl | custom
providers: [Service A, Component X]
consumers: [Service B, Mobile App, Edge Gateway]
last-reviewed: YYYY-MM-DD
---
```

## 1. Overview & Purpose

- **Description:** High-level summary of what this interface does and the business/technical capabilities it exposes.
- **Scope & Boundaries:** What is included and excluded.
- **Provider(s):** Systems or components that implement and host this interface.
- **Consumer(s):** Systems or components that invoke or subscribe to this interface.

---

## 2. Interface Approach & Technology Selection

Select the specification format appropriate for the architectural pattern:

| Pattern / Style | Recommended Specification Standard | Primary Artifact Location |
|---|---|---|
| **RESTful HTTP / Web API** | **OpenAPI (OAS 3.0 / 3.1)** | `api/openapi.yaml` |
| **Event-Driven / Messaging** | **AsyncAPI (v2 / v3)** | `api/asyncapi.yaml` |
| **High-Performance RPC / Streaming** | **gRPC / Protocol Buffers (v3)** | `api/proto/*.proto` |
| **Queryable Graph API** | **GraphQL Schema Definition (SDL)** | `api/schema.graphql` |
| **Low-Level IPC / OS / Embedded** | **DBus IDL / FIDL / C Headers** | `api/idl/*` |

---

## 3. Detailed Specification Subsections

### 3.1 RESTful HTTP Interface (OpenAPI)

*For HTTP/REST APIs, link to or embed the OpenAPI 3.x specification file (`openapi.yaml`).*

- **Base URL / Environment:** `https://api.example.com/v1`
- **Authentication & Security:** OAuth2, JWT Bearer, API Keys, mTLS.
- **Endpoints & Operations Summary:**
  - `GET /v1/resources` – List resources (Query params: `limit`, `offset`).
  - `POST /v1/resources` – Create resource (Request Body: JSON Schema).
  - `GET /v1/resources/{id}` – Retrieve single resource.
  - `DELETE /v1/resources/{id}` – Remove resource.
- **Response Codes & Standard Error Format:**
  - `200 OK`, `201 Created`, `400 Bad Request`, `401 Unauthorized`, `404 Not Found`, `500 Internal Error`.
  - RFC 7807 Problem Details for HTTP APIs schema.

```yaml
# Example OpenAPI snippet reference
openapi: 3.1.0
info:
  title: Example Resource API
  version: 1.0.0
paths:
  /v1/resources:
    get:
      summary: Retrieve resource list
      responses:
        '200':
          description: Successful response
```

---

### 3.2 Event-Driven & Messaging Interface (AsyncAPI)

*For asynchronous, message-bus, WebSocket, MQTT, Kafka, or AMQP interfaces, link to or embed the AsyncAPI specification (`asyncapi.yaml`).*

- **Protocol & Transport:** MQTT v5, Apache Kafka, AMQP 0-9-1, WebSockets, NATS.
- **Broker / Endpoint:** `mqtts://telemetry.example.com:8883` or `kafka.internal:9092`
- **Channels & Topics:**
  - `telemetry/v1/devices/{deviceId}/status` – Device telemetry events.
  - `commands/v1/devices/{deviceId}/control` – Inbound device control commands.
- **Message Semantics:**
  - **Publish Operations:** Messages emitted by providers.
  - **Subscribe Operations:** Messages listened to by consumers.
- **Message Headers & Payload Schemas:** CloudEvents v1.0, JSON Schema, or Avro.

```yaml
# Example AsyncAPI snippet reference
asyncapi: 3.0.0
info:
  title: Device Telemetry Event Stream
  version: 1.0.0
channels:
  deviceStatus:
    address: 'telemetry/v1/devices/{deviceId}/status'
    messages:
      statusEvent:
        payload:
          type: object
          properties:
            temperature: { type: number }
            batteryLevel: { type: integer }
```

---

### 3.3 Remote Procedure Call & Binary Interfaces (gRPC / Protobuf)

*For microservices RPCs, high-throughput streaming, or cross-language binary interfaces.*

- **Transport:** HTTP/2 or HTTP/3.
- **Service & Method Definitions:**

```protobuf
syntax = "proto3";

package telemetry.v1;

service DeviceService {
  rpc GetStatus (StatusRequest) returns (StatusResponse);
  rpc StreamTelemetry (TelemetryRequest) returns (stream TelemetryData);
}
```

---

### 3.4 GraphQL & Flexible Query Interfaces

*For client-driven data fetching and composite graph APIs.*

- **Schema Definition (SDL):**

```graphql
type Device {
  id: ID!
  name: String!
  status: DeviceStatus!
}

type Query {
  device(id: ID!): Device
}
```

---

### 3.5 Inter-Process & Low-Level Hardware Interfaces (IPC / IDL)

*For embedded OS IPC (DBus, Binder, FIDL), shared memory ring buffers, or register-level contracts.*

- **Mechanism:** DBus / Shared Memory / Unix Domain Sockets / SPI / I2C / CAN bus.
- **Message Structure / Struct Alignment:** Packing rules (e.g. `#pragma pack(1)`), byte order (Little-Endian / Big-Endian).
- **IDL Definition / Header File:** Link to `interface.xml` or `interface.h`.

---

## 4. Data & Encoding Standards

- **Serialization Format:** JSON / Protocol Buffers / CBOR / Avro / Raw Binary.
- **Encoding & Character Sets:** UTF-8.
- **Endianness & Field Alignment:** Explicitly state if binary (e.g., Network Byte Order / Big-Endian).

---

## 5. Timing, Performance & Quality of Service (QoS)

- **Latency Target:** e.g., 99th percentile < 50ms.
- **Throughput / Rate Limits:** e.g., Max 100 requests/sec per client.
- **Delivery Guarantees (Messaging):** At-most-once (QoS 0) / At-least-once (QoS 1) / Exactly-once (QoS 2).

---

## 6. Errors, Fault Handling & Recovery

- **Error Codes:** Standardized numeric or string error codes.
- **Retry & Backoff Policy:** Exponential backoff with jitter rules.
- **Circuit Breaking & Fallbacks:** Behavior when provider is unreachable.

---

## 7. Versioning & Backward Compatibility

- **Versioning Strategy:** Semantic Versioning (`MAJOR.MINOR.PATCH`).
- **Breaking Change Rules:** `MAJOR` version bump required for field deletions or type changes.
- **Deprecation Grace Period:** Minimum 6 months notice prior to removing deprecated endpoints/channels.

---

## 8. Security & Privacy Properties

- **Authentication:** Token format and identity verification.
- **Authorization:** Role-Based Access Control (RBAC) or Scope requirements.
- **Encryption:** TLS 1.3 in transit, payload encryption at rest if sensitive.

---

## 9. Verification & Automated Testing

- **Contract Testing:** Pact, Postman/Newman, or AsyncAPI validation.
- **Mock Servers:** Automated mock generation from OpenAPI/AsyncAPI files.
- **CI Quality Gate:** Automated schema compatibility checks in pipeline.
