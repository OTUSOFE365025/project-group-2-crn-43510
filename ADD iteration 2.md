Include in this file the 7 steps for Iteration 2



## STEP 1 [Review Inputs]

##### Iteration 2 focuses on making more detailed architectural decisions that drive implementation, moving from generic to specific. In Iteration 2 we will build upon the results of Iteration 1. In Iteration 1, the overall architecture structure was established and the primary drivers were identified (use cases, quality attributes, concerns, and constraints). Throughout the second iteration, the results of the first iteration will be further refined and modeled to support implementation. 

### 1.1 Primary Functional Drivers [Use Cases]

|Use Case|Description|Associated Requirement ID|
|--------|-----------|-------------------------|
|UC-1:Student Query & System Answer|The Student Asks the system a question, the system interprets the query, then generates a response using both stored knowledge and live data.|RS1, R5, R6|
|UC-2: Lecturer Announcement to Students|The Lecturer requests to send a new announcement to their students, the systems authorizes the Lecturer's access, interprets the update, then notifies the students.| R5, RL1, RL2, RL8, RA5|
|UC-3: Lecturer Views Course Analytics Summary|The Lecturer requests a summary of their course analytics, the system interprets the query, retrieves the relevant secure data (grades, attendance, student engagment), then presents the summarized results.| RL3, RL6, R3, R4, R6, R8|
|UC-4: Administrator Broadcasts Campus-Wide Announcement|The Administrator broadcasts an announcement, the system verifies Administrator access, sends the message to the Students and Lecturers, then confirms message delivery.|RA3, RA5, R3, R4, R8, RS2|
|UC-5: Lecturer Informs Students of Low Engaement|The System detects low student engagemnet and notifies the Lecturer, the Lectuerer responds by sending a message to their students addressing the issue and encouraging participation, then the Students recieve the message through the System.| RL7, RS2, R6|
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

Goal: The goal of this iteration is to identify concrete structures that support the AIDAP's primary functionality and act as units of implementation for development teams. This moves the architecture from a more generalized structure to distinct modules that can be independently developed, implemented, and tested.

 Drivers: 
 The primary drivers that will be emphasized in this iteration are:
 
 - Primary Use Cases:
     - UC-1: Student Query & System Answer
     - UC-2: Lecturer Announcement to Students
     - UC-3: Lecturer Views Course Analytics Summary
 - Quality Attributes:
     - QA-1: Performance 
     - QA-2: Security 
     - QA-4: Maintainability
     - QA-5: Availability 

## STEP 3 [Choose One or More Elements of the System to Refine]

In Iteration 1, the architecture of the AIDAP was defined at a high level. The architecture consisted of six (6) parts:
- Presentation Layer
- API Gateway / Entry point
- Core Application Services
- Integration Layer
- Data Management Layer
- External Systems
These parts provided a general overview of the system's structure but did not outline definite modules that will implement the system's primary functionality.

For Iteration 2, the elements from iteration 1 that will be refined are:
- Core Applcation Services
- Data Management Layer

These elements were chosen because they are directly affected by the primary functional drivers (UC-1, UC-2, UC-3), and the key quality attributes (QA-1, QA-2, QA-4, QA-5). These use cases rely on backend logic, AI interaction, analytical services, and data storage. Refining these elements of Iteration 1 provides architectural clarity and reduces implementation risks.

The Core Application Services will be refined into the following modules:
- Conversation Manager
- NLU Service
- Context Management
- AI Gateway
- Announcement Manager
- Analytics Processor

The Data Management layer will be refined into the following modules:
- Chat Log Repository
- User Respository
- Course & Schedule Cache
- Analytics Repository
- System Metrics DB

## STEP 4 [Choose One or More Design Concepts That Satisfy the Selected Drivers]

| Design Location and Location | Rationale and Assumption |
|------------------------------|--------------------------|
| Use a **Layered Architecture** for the Core Application Services and Data Management elements | A layered architecture allows for encapsulation, independent development of modules, and adequate maintainability *(QA-4)*. This architectural pattern also supports the security *(QA-2)* of the system by isolating access to vulnerable data within the Data Management Layer. |
| Use the **Broker Pattern** for the Core Application Services | All three primary use case drivers *(UC-1, UC-2, UC-3)* requires the collaboration between multiple backend services (NLU, AI Gateway, Data Logging, Analytics). The Broker architecture will reduce coupling between services, improve modifiability, and support horizontal scailing *(QA-1 & QA-5)*. |
| Use the **Repository pattern** for Data Management | This pattern provides a clear separation between the client/business logic and the data source/access. This separation facilitates easier maintenance *(QA-4)*, as changes can be made without disturbing the services, allowing the repository to be updated without interruption. This will also improve consistency within the Data Management Layer as all services will utilize the same query logic, which reduces duplication and allows for easier system testing *(QA-4 & QA-5)*. |
| Use the **Facade Pattern** for the AI Gateway | The Facade Pattern hides the complexities of the AI models. It allows for a simplified interface for the Conversation Manager and also allows for the AI models to be updated without affecting the entire system *(QA-5)*. |
| Use the **Adapter pattern** for external systems integration | External services, such as LMS, Registration, Calendar, and email systems, use different incompatible APIs and data formats (XML, JSON). The Adapter pattern will enable these services to work together without altering their source code, thereby improving the availability and maintainability *(QA-4, QA-5)* of the system. |

## STEP 5 [Instantiate Architectural Elements, Allocate Responsibilities and Define Interfaces]

## STEP 6 [Sketch Views and Record Design Decisions]

**Use Case Sequence Diagrams**

*UC-1:  Student Query & System Answer*
<img width="2228" height="1010" alt="UC1 drawio" src="https://github.com/user-attachments/assets/50386b94-23f9-44de-8115-08429e195890" />

*UC-2: Lecturer Announcement to Students*
<img width="2230" height="906" alt="UC2 drawio" src="https://github.com/user-attachments/assets/7717b168-559b-4c97-86bc-b925fb324a00" />

*UC-3: Lecturer Views Course Analytics Summary*
<img width="2070" height="884" alt="UC3 drawio" src="https://github.com/user-attachments/assets/12bb0fda-bb46-4642-9c2c-4be8257fc541" />

**Use Case Sequence Diagram Descriptions**
*UC-1:  Student Query & System Answer*

















