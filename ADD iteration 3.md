
## STEP 1 [Review Inputs]

##### Iteration 3 focuses on results of Iterations 1 and 2 by refining the remaining high-priority use cases and quality attributes that we did not fully address previously. The focus of this iteration is on implementing system behaviors related to engagement monitoring, low-engagement detection, and notification workflows. These capabilities require deeper refinement of background processing, analytics retrieval, and event-based triggers. 

### 1.1 Primary Functional Drivers [Use Cases]

|Use Case|Description|Associated Requirement ID|
|--------|-----------|-------------------------|
|UC-1:Student Query & System Answer|The Student Asks the system a question, the system interprets the query, then generates a response using both stored knowledge and live data.|RS1, R5, R6|
|UC-2: Lecturer Announcement to Students|The Lecturer requests to send a new announcement to their students, the systems authorizes the Lecturer's access, interprets the update, then notifies the students.| R5, RL1, RL2, RL8, RA5|
|UC-3: Lecturer Views Course Analytics Summary|The Lecturer requests a summary of their course analytics, the system interprets the query, retrieves the relevant secure data (grades, attendance, student engagment), then presents the summarized results.| RL3, RL6, R3, R4, R6, R8|
|UC-4: Administrator Broadcasts Campus-Wide Announcement|The Administrator broadcasts an announcement, the system verifies Administrator access, sends the message to the Students and Lecturers, then confirms message delivery.|RA3, RA5, R3, R4, R8, RS2|
|UC-5: Lecturer Informs Students of Low Engagement|The System detects low student engagemnet and notifies the Lecturer, the Lectuerer responds by sending a message to their students addressing the issue and encouraging participation, then the Students recieve the message through the System.| RL7, RS2, R6|
|UC-6: Administrator Recovers Data for Users|The Administrator initiates a system recovery after a system failure, restoring data and access for the Lecturers and Students, ensuring continued support and interaction without disruption.|RA6, RM6, R7, RA5|

---

### 1.2 Quality Attributes

|ID|Quality Attribute|Scenario|Associated Use Case|
|--|-----------------|--------|-------------------|
|**QA-1**|**Performance**|The System responds to Student queries within 2 seconds on avergae under normal load.|UC-1|
|**QA-2**|**Security**|Only system authorized Lecturers can send annoucements to their respective courses.|UC-2|
|**QA-3**|**Usability**|The System's user interface and conversational design present student-related analytics in a clear, intuitive, and organized format allowing Lecturers to easily request and interpret data.|UC-3|
|**QA-4**|**Maintainability**|The System allows Administators and System Maintainers to deploy updates and monitoring tools continuously without disrupting user interaction|UC-5|
|**QA-5**|**Availability**|The System maintains a minimum of 99.5% available uptime duirng the academic year to ensure dependable service access.|UC-6|

---

### 1.3 Concerns

| ID   | Concern |
|----  |---------|
|CRN-1|**AI model management:** Different models or versions may affect accuracy and latency, so version control and configuration are key|
|CRN-2|**Integration stability:** External systems like LMS or calendars may go down, requiring retry and recovery mechanisms|
|CRN-3|**Role-based access:** Students, lecturers, and administrators have different permissions, so RBAC must be enforced|
|CRN-4|**Context handling:** The assistant must blend live and stored data for accurate, contextual answers|
|CRN-5|**Data privacy:** Conversations and user data should be securely stored and anonymized when possible| 
|CRN-6|**Scalability:** Large scalability causes monetary and operational expenses especially during peak academic season|
|CRN-7|**Monitoring and observability:** Logging latency, accuracy, and usage metrics is essential for maintainers|
|CRN-8|**Error recovery and fault tolerance:** The system must handle runtime failures (e.g., API timeouts, service crashes) without losing critical user data or context.|
|CRN-9|**Energy and resource efficiency:** The system should manage AI processes and overall resource usage efficiently to reduce cloud costs and maintain performance during peak activity.|

---

### 1.4 Constraints

| ID | Constraint |
|----|------------|
|CON-1|The system will be deployed as a cloud-native service to support scaling and uptime|
|CON-2|Integrations must rely on standard REST or GraphQL APIs for interoperability|
|CON-3|User authentication will use the university’s single sign-on (SSO)|
|CON-4|The assistant must support both text and voice interaction|
|CON-5|Privacy and security compliance is mandatory under institutional policy|
|CON-6|System uptime should be 99.5% or higher with proper fail-over|
|CON-7|Average response time should stay under 2 seconds in normal load conditions|
|CON-8|The platform should support around 5,000 concurrent users|
|CON-9|The system must support multi-language queries and responses|
|CON-10|The system must be accessible and available on mobile, web, and voice-assistant devices|

 ---

 ## STEP 2 [Establish Iteration Goal by Selecting Drivers]

Goal: The goal of this iteration is to introduce architectural refinements that support event-driven engagement monitoring, trend analysis, and automated lecturer notifications for UC-5. This iteration focuses on creating background processing components, establishing new data flows for engagement trends, and defining end-to-end interactions for the low-engagement workflow.

 Drivers: 
 The primary drivers that will be emphasized in this iteration are:
 
 - Primary Use Cases:
     - UC-5: Lecturer Informs Students of Low Engagement
 - Quality Attributes:
     - QA-1: Performance 
     - QA-4: Maintainability
     - QA-5: Availability

## STEP 3 [Choose One or More Elements of the System to Refine]

For Iteration 3, the elements from iterations 1 and 2 that will be refined are:
- Core Application Services
- Data Management Layer
- Integration Layer

These elements were chosen because they are directly affected by the primary functional driver (UC-5), and the key quality attributes (QA-1, QA-4, QA-5). This use case relies on trend analysis, automated background jobs, accurate data retrieval and notification delivery. Refining these elements of Iteration 2 provides architectural clarity and reduces implementation risks.

The Core Application Services will be refined into the following modules:
- NLU Service
- Engagement Monitoring Service
- Notification Builder
- Analytics Processor

The Data Management layer will be refined into the following modules:
- Engagement Metrics Store
- Student Activity Log Store
- Update to Analytics Repository to store engagement scores

The Integration layer will be refined into the following modules:
- Notification Adapter
- LMS Adapter

## STEP 4 [Choose One or More Design Concepts That Satisfy the Selected Drivers]

| Design Location and Location | Rationale and Assumption |
|------------------------------|--------------------------|
| Observer Pattern | When a low-engagement event triggers, subscribed components (Notification Builder, Announcement Manager) react accordingly. |
| Scheduler / Background Workers | Engagement analysis must run periodically without user initiation. This supports performance (QA-1) and availability (QA-5). |
| Event-Driven Architecture | UC-5 requires asynchronous triggers (e.g., "low engagement detected") without blocking API requests. |
| Repository Pattern | Extension	Supports new data stores for engagement metrics and activity logs. |
| Pipes-and-Filters Pattern | Engagement monitoring pipeline can clean, transform, and calculate metrics from raw logs. It improves maintainability (QA-4). |

## STEP 5 [Instantiate Architectural Elements, Allocate Responsibilities and Define Interfaces]

## 5.1 Core Application Services Layer

### Components and Responsibilities
| Component | Responsibilities |
|----------|------------------|
| **Notification Builder** | Creates structured low-engagement alert messages based on templates and passes them to Notification Adapter. |
| **Analytics Processor** | Collects and summarizes course analytics through integration adapters. Performs asynchronous data processing for performance. Generates engagement scores and stores them in the Engagement Metrics Store. |
| **Engagement Monitoring Service** | Periodically retrieves student activity logs, runs engagement calculations, identifies low-activity users, and triggers alerts to lectures. |
| **NLU Service** | Performs natural language understanding: intent detection, entity extraction, and classification. Supports multi-language queries. Interprets lecturer queries related to engagement insights (e.g., “Which students are falling behind?”). |

## 5.2 Integration Layer

### Components and Responsibilities
| Component | Responsibilities |
|----------|------------------|
| **LMS Adapter** | Communicates with the LMS to retrieve course content and analytics inputs. Fetches raw participation and activity statistics for each student. |
| **Email/Notification Adapter** | Sends low-engagement alerts via email or notification channels and supports templated messages. |

## 5.3 Data Management Layer

### Components and Responsibilities
| Component | Responsibilities |
|----------|------------------|
| **Engagement Metrics Store** | Stores computed engagement scores per student, per course. |
| **Analytics Data Store** | Stores processed analytics and engagement metrics. Includes engagement summary endpoints for lecturers. |
| **Student Activity Log Store** | Stores participation logs, attendance, submission timestamps, and LMS activity. |


## 5.4 Summary

These instantiated architectural elements refine the Core Services and Data Management layers to support low-engagement detection and lecturer notifications. The added components define how engagement analysis and alert workflows operate. These updates complete the architectural support needed for UC-5.

## STEP 6 [Sketch Views and Record Design Decisions]

**Use Case Sequence Diagrams**
*UC-5: Low Engagement Detection & Lecturer Notification*

**Use Case Sequence Diagram Description**

*UC-5: Low Engagement Detection & Lecturer Notification*

| Element | Method Name | Description |
|---------|-------------|-------------|
| Web UI | sendQuery(userTok, queryText) | Sends the user entered NL query and session token to the backend |
| API Gateway | handleQuery(userContext, queryText) | Coordinates query interpretation, AI response generation, chat logging, then returns answer |
| NLU Service | interpret(queryText, userContext) | sends the user's NL query to be interpreted |
| Context Manager | generateContext(userId, intent) | Creates a conversation context object |
| Course and Schedule Cache | getCourseAndSchedule(userId) | Returns user's courses and scheduless |
| AI Gateway | generateResponse(queryContext, intent) | Generates a NL draft response to user's NL query |
| Chat Log Repository | saveMessage(conversationId, userId, queryText, draftAnswer) | Logs user's query, system's draft answer, user's ID, and the conversation ID |
