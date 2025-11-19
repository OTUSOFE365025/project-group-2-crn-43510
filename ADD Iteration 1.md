Include in this file the 7 steps for Iteration 1
## STEP 1 [Review Inputs]

## 1.1 Primary Functional Drivers [Use Cases]

|Use Case|Description|Associated Requirement ID|
|--------|-----------|-------------------------|
|UC-1:Student Query & System Answer|The Student Asks the system a question, the system interprets the query, then generates a response using both stored knowledge and live data.|RS1, R5, R6|
|UC-2: Lecturer Announcement to Students|The Lecturer requests to send a new announcement to their students, the systems authorizes the Lecturer's access, interprets the update, then notifies the students.| R5, RL1, RL2, RL8, RA5|
|UC-3: Lecturer Views Course Analytics Summary|The Lecturer requests a summary of their course analytics, the system interprets the query, retrieves the relevant secure data (grades, attendance, student engagment), then presents the summarized results.| RL3, RL6, R3, R4, R6, R8|
|UC-4: Administrator Broadcasts Campus-Wide Announcement|The Administrator broadcasts an announcement, the system verifies Administrator access, sends the message to the Students and Lecturers, then confirms message delivery.|RA3, RA5, R3, R4, R8, RS2|
|UC-5: Lecturer Informs Students of Low Engaement|The System detects low student engagemnet and notifies the Lecturer, the Lectuerer responds by sending a message to their students addressing the issue and encouraging participation, then the Students recieve the message through the System.| RL7, RS2, R6|
|UC-6: Administrator Recovers Data for Users|The Administrator initiates a system recovery after a system failure, restoring data and access for the Lecturers and Students, ensuring continued support and interaction without disruption.|RA6, RM6, R7, RA5|

## 1.2 Quality Attribute Drivers

|ID|Quality Attribute|Scenario|Associated Use Case|
|--|-----------------|--------|-------------------|
|**QA-1**|**Performance**|The System responds to Student queries within 2 seconds on avergae under normal load.|UC-1|
|**QA-2**|**Security**|Only system authorized Lecturers can send annoucements to their respective courses.|UC-2|
|**QA-3**|**Usability**|The System's user interface and conversational design present student-related analytics in a clear, intuitive, and organized format allowing Lecturers to easily request and interpret data.|UC-3|
|**QA-4**|**Maintainability**|The System allows Administators and System Maintainers to deploy updates and monitoring tools continuously without disrupting user interaction|UC-5|
|**QA-5**|**Availability**|The System maintains a minimum of 99.5% available uptime duirng the academic year to ensure dependable service access.|UC-6|

## 1.3 Constraints

- Cloud-native deployment
- REST or GraphQL used for external integrations
- Must use university Single Sign-On (SSO)
- Supports both text and voice interaction
- Average response time must be within 2 seconds
- Handles up to 5,000 concurrent users
- Supports multiple languages
- Accessible on web, mobile, and voice-enabled devices

## 1.4 Architectural Concerns
- AI model versioning and configuration
- Stability of external integrations and retry mechanisms
- Role-based access for students, lecturers, and administrators
- Handling of user context using both live and historical data
- Data privacy and secure storage of user information
- Monitoring of latency, accuracy, logs, and system metrics
- Fault tolerance and error recovery during service failures
- Scalability to maintain performance under peak load
- Efficient use of resources to manage cloud costs

## STEP 2 [Establish Iteration Goal]

THe goal of Iteration 1 is to establish a high level architecture for AIDAP and define the system structure at a broad level. This iteration focuses on main functions that will impact how the platform operates and behaves. 

Specifically this Iteration will focus on:
- Identifying a suitable reference architecture for AIDAP

- Breaking the system into major layers and components

- Addressing core use cases (UC-1, UC-2, UC-3, UC-4, UC-6)

- Considering key quality attributes like performance, availability, security, usability, and maintainability

- Producing the initial logical architecture and deployment views

- Assigning responsibilities to each high-level component

By the end of this iteration, the system should have a clear architectural foundation. This will be refined in Iteration 2 when domain-specific components and detailed interactions are introduced.

## STEP 3 [Choose Elements of the System to Decompose]

In Iteration 1, the AIDAP system is decomposed at a high level to establish the architectural areas for the primary use cases and quality attributes identified in Step 1. the goal is to break the system into its core layers and subsystems.

The system is decomposed into the following parts:

- Presentation Layer: Web interface, mobile app, and voice/assistant interface used by students, lecturers, and administrators.

- API Gateway / Entry Point: Central access point handling SSO authentication, request routing, and security enforcement.

- Core Application Services Layer: High-level backend services such as conversational/query processing, AI model interaction, context handling, announcements, analytics, and engagement monitoring.

- Integration Layer: Components that connect AIDAP to external systems including LMS, Registration, Calendar, and Email services through REST/GraphQL APIs.

- Data Management Layer: Storage components for conversation history, user profiles and preferences, analytics data, logs, and system metrics.

- External Systems: University SSO provider, LMS, registration system, academic calendar system, email server, and notification services.

## STEP 4 [Choose Design Concepts That Satisfy the Selected Drivers]

The purpose of this step is to select design concepts that will guide how the high-level components identified in Step 3 should be structured. These concepts need to support the main use cases (UC-1 to UC-6), system constraints, and the quality attributes prioritized in Step 1.

# Presentation Layer

Design Concepts:

Thin client interfaces for web and mobile.

Clear separation between UI and backend logic.

Optional support for voice-enabled devices as required by system constraints.

Reason:
This supports multi-platform access, usability, and keeps complex logic on the server side for better performance and maintainability.

# API Gateway / Entry Point

Design Concepts:

API Gateway pattern as a single controlled entry point.

Centralized authentication through the university’s SSO provider.

Routing, access control, and basic request validation.

Reason:
This aligns with the SSO requirement, improves security, and simplifies how different clients communicate with backend services.

# Core Application Services

Design Concepts:

Service-oriented structure with separate modules (query processing, AI model service, announcements, analytics, engagement monitoring).

Stateless service design to enable horizontal scaling.

Support for asynchronous operations when necessary (e.g., analytics).

Reason:
This helps with performance, availability, and maintainability, and it maps directly to the main system use cases.

# Integration Layer

Design Concepts:

Adapter pattern for LMS, Registration, Calendar, and Email systems.

Single integration facade that backend services interact with.

Retry and timeout logic for external service faults.

Reason:
This ensures compatibility with required REST/GraphQL data sources and increases reliability when external systems fail or lag.

# Data Management Layer

Design Concepts:

Repository/Data Access patterns for conversation history, user profiles, analytics, and logs.

Logical separation of operational data, analytics data, and system metrics.

Caching for frequently accessed academic and schedule information.

Reason:
This supports persistence requirements, improves performance, and keeps data concerns cleanly separated.

# External Systems (Boundary)

Design Concepts:

Clearly modeled as external dependencies in the architecture.

Use of standard protocols like REST/GraphQL and SSO standards.

Loose coupling via adapters rather than direct internal integration.

Reason:
This defines system boundaries, reduces coupling, and makes the architecture more adaptable to changes in external university systems.
## STEP 5 [Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces]
## STEP 6 [Sketch Views and Record Design Decisions]
## STEP 7 [Perform Analysis of the Current Design and Review Iteration Goal]
