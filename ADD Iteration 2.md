# ADD Iteration 2

## Step 1 - Review Inputs

The design inputs were established in a previous phase of the project in the following files:

```
Business Driver
Concerns.md
Constraints.md
Quality Attributes.md
Use Cases.md
```

However, they will be briefly reestablished in this document:

### Business Driver

The main driver for AIDAP is to provide a conversational interface for students, faculty, and administrators to interact with

institutional data such as course schedules, deadlines, announcements, and academic analytics. The
assistant integrates with external university systems (LMS, registration, calendars, and mail) and uses AI
to deliver contextual answers.

We want to create a system that is maintainable, scalable and reliable.
For students it will save time and keep them organized.
For instructors, it makes sharing updates and managing classes easy and simple.
For administrators, it will make data management consistent and clear.

### Concerns

- CRN-1 The system shall maintain data integrity and consistency across systems.
- CRN-2 The system shall support scalability to handle up to 5,000 concurrent users.
- CRN-3 The system shall ensure that only authorized lecturers can modify course data.
- CRN-4 The system shall protect user data and comply with institutional privacy policies.
- CRN-5 The system shall remain available 99.5% of the time per month.
- CRN-6 The system shall respond to queries within 2 seconds on average under normal load.

### Quality Attributes

- QA-1 Reliability
- QA-2 Usability
- QA-3 Privacy & Security
- QA-4 Interoperability
- QA-5 Scalability
- QA-6 Maintainability

### Use Cases

- UC-1 The student exports their calendar
- UC-2 The student uses the dashboard to view their grades
- UC-3 A lecturer posts an announcement for their course
- UC-4 A lecturer uploads courses content via the AIDAP
- UC-5 An administrator sends a campus-wide announcement
- UC-6 An administrator generates an analytics report

## Step 2 - Establish Iteration Goal by Selecting Drivers
After reviewing the drivers, iteration 2 will be focused on **Identifying Structures to Support Primary Functionality**.

More specifically, the following drivers will be focused on during this iteration:
|Driver ID | Driver Name                                      |
|----------|--------------------------------------------------|
| QA-5     | Scalability                                      |
| UC-4     | A lecturer uploads courses content via the AIDAP |
| UC-2 | The student uses the dashboard to view their grades|
| CRN-1    |The system shall maintain data integrity and consistency across systems.|
| CRN-2 | The system shall support scalability to handle up to 5,000 concurrent users. |
| CRN-5 | The system shall remain available 99.5% of the time per month. |
| CRN-6 | The system shall respond to queries within 2 seconds on average under normal load. |

## Step 3 - Choose One or More Elements of the System to Decompose

For developing the structures to support primary functionallity, this iteration will be focusing on the **Hosting**, which will include how databases are hosted in the cloud.

## Step 4 - Choose One or More Design Concepts that Satisfy the Inputs Considered in the Iteration

**Design Choice** - Hosting Architecture
| Design Concept | Pros | Cons | Cost |
| ----------------------- | ------------------------------ | ------------------------------------------------- | ---- |
| Distributed Deployment | Scalability (+ QA-5)<br> | Network Latency (- CRN-6) | High |
| Two Tier Deployment | Simple (+ CRN-6)<br> | Not Secure (- CRN-4) | Low |
| Three Tier Deployment | Security (+ CRN-4)<br> | Simple (+ CRN-6)<br> | High |
| Four Tier Deployment | Security (+ CRN-4)<br> | Medium |

After reviewing the above table, the decision is to move forward with the **Distributed Deployment** for the user interface.

## Step 5 - Instantiate Architectural Elements, Allocate Responsibilites, and Define Interfaces

To implement the **Distributed Deployment**, the following design decisions have been made:
| Design Decision | Rationale |
| --------------- | --------- |
|use Postgressql|provides scalability across distributed systems|
|use azure hosting|built-in scaling, load balancing, and redundancy|
|Impliment a rest api|easier scaling and communication|

## Step 6 - Sketch Views and Record Design Decisions



## Step 7 - Perform Analysis of Current Design and Review Iteration Goal and Design Objectives

| Driver ID | Design Decision | Rationale |
| --------- | --------------- | --------- |
|QA-5|Use Azure hosting|Azure provides automatic scaling, redundancy, and distributed load balancing. Perfect for scalability.|
|UC-4|Implement a REST API|This API will make it easy for us to transfer and store data.|
|UC-2|Use PostgreSQL|enables fast retrieval of data.|
|CRN-2|Use Azure hosting|Azure's Cloud infrastructure can easily scale to support well over 5,000 concurrent users under load.|
|CRN-6|Implement a REST API|It will allow us to keep response times under 2 seconds|