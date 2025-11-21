Include in this file the 7 steps for Iteration 2

**STEP 1 [Review Inputs]**

**1.1 Primary Functional Drivers [Use Cases]**


|Use Case|Description|Associated Requirement ID|
|--------|-----------|-------------------------|
|UC-1:Student Query & System Answer|The Student Asks the system a question, the system interprets the query, then generates a response using both stored knowledge and live data. This requires detailed handling of query interpretation, model selection, and data retrieval.|RS1, R5, R6|
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

The goal of Iteration 2 is to refine the components of the system and introduce the pieces that make the architecture more complete and clearer from an implementation point of view.

Specifically this Iteration will focus on:
- Creating a simple deployment view that shows how AIDAP fits into a cloud environment (e.g., API Gateway, core backend services, data stores, and external university systems).

- Adding a basic domain model that highlights the main entities the system works with, such as Student, Lecturer, Course, Announcement.

- Addressing the architectural concerns from Iteration 1 by showing which newly added components directly support them.

- Adding more detailed components inside each major layer.

- Introducing the integration parts that were only mentioned broadly before, such as the Calendar integration and general Notification/Email integration.

By the end of this iteration, the overall structure of the architecture will be refined with the extra details and components needed to better understand how the system will function.

## STEP 3 [Choose Elements of the System to Decompose]

In Iteration 1, the system was decomposed into major architectural layers to establish the overall structure of AIDAP. Iteration 2 continues this process by breaking those high-level layers into the specific components that will actually carry out the system’s core functions. The goal here is to introduce the domain-specific modules and integration points that are needed to support the detailed design.

The system is decomposed into the following parts:

- Presentation Layer: Web interface, mobile app, and voice/assistant interface (used by students, lecturers, and administrators) with support for structured input handling.

- API Gateway / Entry Point: Central access point handling SSO authentication, request routing, Role-based Access Control (RBAC) validator. and security enforcement.

- Core Application Services Layer: High-level backend services such as conversational/query processing, AI model interaction, context handling, announcements, analytics, and engagement monitoring.

- Integration Layer: Components that connect AIDAP to external systems including LMS, Registration, Calendar, and Email services through REST/GraphQL APIs.

- Data Management Layer: Storage components for conversation history, user profiles and preferences, analytics data, logs, caching layers and system metrics.

- External Systems: University SSO provider, LMS, registration system, academic calendar system, email server, and notification services.

## STEP 4 [Choose Design Concepts That Satisfy the Selected Drivers]

The purpose of this step is to update the design concepts from Iteration 1 and apply them to the new components added in Iteration 2 to better support the system’s requirements.

# 4.1 Presentation Layer

Design Concepts:

Thin client interfaces for web and mobile now support structured formatting of user queries before they are forwarded to backend services.

Clear separation between UI and backend logic.

Shared UI elements for announcements, analytics, and notifications to maintain consistency across platforms.

Optional support for voice-enabled devices as required by system constraints.

Reason:
This supports multi-platform access, usability, and keeps complex logic on the server side for better performance and maintainability while ensuring that user inputs are clean and consistent before reaching the query interpretation flow.

# 4.2 API Gateway / Entry Point

Design Concepts:

Basic rate-limiting to prevent overload during peak academic periods.

Centralized authentication through the university’s SSO provider with RBAC validation added to enforce permissions for students, lecturers, and administrators.

Routing, access control, basic request validation and new domain services (announcements, analytics, engagement monitoring).

Reason:
These help support security, performance, and the system’s requirement to manage different user roles properly.

# 4.3 Core Application Services

Design Concepts:

Service-oriented structure with separate modules (query processing, AI model service, announcements, analytics, engagement monitoring).

Stateless service design to enable horizontal scaling and maintain scalability, but the Context Manager uses session/state stitching for personalized responses.

Support for asynchronous operations when necessary (e.g., analytics).

Reason:
This reflect actual system behavior more closely, helps with performance, availability, and maintainability, and it maps directly to the main system use cases.
