# ATAM Analysis + Risk Assessment

## Risks

### R1 - REST API Limits Peak Performance Under Load

**Decision** - Adoption of REST (JSON over HTTPS) as the primary communication protocol.

**QA Response** - Scalability (QA-5); System must handle up to 5,000 concurrent users (CRN-2) while maintaining a <2s response (CRN-6).

**Rationale** - REST adds overhead due to text encoding and statelessness. Under peak traffic,
response time may exceed requirements and external systems may experience degraded performance.

### R2 - Logging Volume may Degrade System Response Time

**Decision** - Full logging of all API interactions to support monitoring and debugging.

**QA Response** - Maintainability (QA-6) and Performance (CRN-6)

**Rationale** - Detailed logs increase disk I/O and processing time. During peak load, logging
overhead may raise latency past 2 seconds or exhaust storage if log rotation is not implemented.

### R3 - Rate-Limiting may Block Legitimate Student or Faculty Requests

**Decision** - Introduction of API rate-limiting to ensure stability under load.

**QA Response** - Scalability (QA-5) and Usability (QA-2).

**Rationale** - Aggressive rate thresholds may prevent students from accessing critical services
(e.g., schedule export or analytics) during normal usage spikes, such as registration week.

### R4 - Inconsistent API Versioning Could Break External Integrations

**Decision** - REST interfaces shared with LMS, calendar, and registration systems.

**QA Response** - Interoperability (QA-4)

**Rationale** - Without a defined versioning strategy, changes to API schemas may cause failures in
external systems relying on stable contracts.

## Non-Risks

### N1 - REST API Provides Broad Compatability with University Systems

**Decision** - Use of REST with JSON over HTTPS

**QA Response** - Interoperability (QA-4)

**Rationale** - REST is widely supported and integrated cleanly with browsers, server applications,
and movile clients. This greatly reduces the effort required for integration.

### N2 - Structured Logging Improves Long-Term Maintainability

**Decision** - Centralized logging of all requests and responses.

**QA Response** - Maintainability (QA-6)

**Rationale** - Logs allow developers to trace interactions, isolate faults, and analyze failing
use cases (e.g., UC-6 analytics generation) quickly and accurately.

### N3 - Authentication on All Endpoints Improves Privacy and Security

**Decision** - Mandatory authentication + authorization filtering

**QA Response** - Privacy & Security (QA-3)

**Rationale** - Enforcing access control by default prevents unauthorized data access and aligns
with institutional compliance rules, with minimal architectural risk.

## Sensitivity Points

### S1 - Logging Verbosity Level

Small increases in logging detail significantly affects latency and system throughput under load, impacting CRN-6.

### S2 - Rate-Limiting Threshold Configuration

Minor adjustments can determine whether legitimate usage is blocked or whether system instability occurs
during traffic spikes.

### S3 - API Schema Consistency and Versioning

Interoperability is highly sensitive to even minor breaking changes, such as renaming fields or altering JSON structures.

### S4 - Authentication Token Expiration Time (TTL)

Shorter TTL improves security, but dramatically increases authentication overhead. A longer TTL reduces auth load,
but increases risk of misuse.

## Trade-Off Points

### T1 - REST Simplicity vs High-Performance Alternatives (i.e. gRPC)

REST maximizes Interoperability, but sacrifices performance under high-concurrency loads when compared to binary protocols
like gRPC.

### T2 - Increased Logging Improves Debugging but Reduces Performance

Logging supports maintainability, but introduces CPU and I/O overhead, negatively impacting average response time.

### T3 - Rate-Limiting Improves System Stability, but Hurts User Experience

While rate-limiting protects against overload, it risks blocking students & instructors during legitimate high-use
periods.

## ATAM Breakdown

**Scenario** - University AIDAP system under peak load (registration week, analytics requests)
**Attributes** - Scalability, Performance, Maintainability, Interoperability, Privacy & Security
**Stimulus** - 5,000 concurrent users, heavy logging, API calls, authentication requests
**Environment** - Cloud-native REST APIs integrated with LMS, calendar, registration systems
**Response** - Maintain <2s latency, stable throughput, secure access, reliable integrations

| Architecture Decision                 | Sensitivity | Tradeoff | Risk | Non-Risk |
| ------------------------------------- | ----------- | -------- | ---- | -------- |
| AD1: REST API (JSON over HTTPS)       | S3          | T1       | R1   | N1       |
| AD2: Full Logging of API Interactions | S1          | T2       | R2   | N2       |
| AD3: API Rate Limiting                | S2          | T3       | R3   | -        |
| AD4: API Versioning Strategy          | S3          | -        | R4   | -        |
| AD5: Authentication & Authorization   | S4          | -        | -    | N3       |
