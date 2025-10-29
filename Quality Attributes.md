# Quality Attributes
After reviewing the requirements, the following Quality Attributes were identified, with up to three requirements provided for each as examples:

- Reliability
  - [RS7] The system shall remain available 99.5% of the time per month.
  - [RA6] The system shall provide high availability with automatic fail-over and backup recovery.
  - [RD3] The system shall handle failures in data source availability gracefully (retry and recovery).
- Usability
  - [RS1] The system shall allow students to ask academic or administrative questions (e.g., "When is my next exam?").
  - [RL1] The system shall allow lecturers to publish or update course materials accessible to students through the assistant.
  - [RA3] The system shall allow administrators to broadcast campus-wide announcements via the assistant.
- Privacy & Security
  - [RS8] The system shall ensure that student-specific data are visible only to the authenticated user.
  - [RL8] The system shall ensure that only authorized lecturers can modify course data.
  - [RA5] The system shall ensure compliance with institutional security and privacy regulations.
- Interoperability
  - [RS7] The system shall provide secure authentication through the institution's single sign-on (SSO).
  - [RA1] The system shall allow administrators to manage institutional integrations (LMS, registration, calendars).
  - [RD1] The system shall synchronize data with connected university systems at configurable intervals.
- Scalability
  - [RA7] The system shall support scalability to handle up to 5,000 concurrent users.
  - [RM5] The system shall be easily extensible to integrate new AI services or external data sources.
- Maintainability
  - [RM1] The system shall allow maintainers to deploy updates with zero downtime using continuous deployment pipelines.
  - [RM2] The system shall provide monitoring dashboards (health, latency, errors).
