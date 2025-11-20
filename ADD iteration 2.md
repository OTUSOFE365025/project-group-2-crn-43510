Include in this file the 7 steps for Iteration 2

Iteration 2 focuses on more detailed decisions that drive implementation, moving from generic to specific.
In Iteration 2 we will build upon the results of Iteration 1 (the overall structure).

# STEP 1 [Review Inputs]

## 1.1 Primary Functional Drivers [Use Cases]

|Use Case|Description|Associated Requirement ID|
|--------|-----------|-------------------------|
|UC-1:Student Query & System Answer|The Student Asks the system a question, the system interprets the query, then generates a response using both stored knowledge and live data.|RS1, R5, R6|
|UC-2: Lecturer Announcement to Students|The Lecturer requests to send a new announcement to their students, the systems authorizes the Lecturer's access, interprets the update, then notifies the students.| R5, RL1, RL2, RL8, RA5|
|UC-3: Lecturer Views Course Analytics Summary|The Lecturer requests a summary of their course analytics, the system interprets the query, retrieves the relevant secure data (grades, attendance, student engagment), then presents the summarized results.| RL3, RL6, R3, R4, R6, R8|
|UC-4: Administrator Broadcasts Campus-Wide Announcement|The Administrator broadcasts an announcement, the system verifies Administrator access, sends the message to the Students and Lecturers, then confirms message delivery.|RA3, RA5, R3, R4, R8, RS2|
|UC-5: Lecturer Informs Students of Low Engaement|The System detects low student engagemnet and notifies the Lecturer, the Lectuerer responds by sending a message to their students addressing the issue and encouraging participation, then the Students recieve the message through the System.| RL7, RS2, R6|
|UC-6: Administrator Recovers Data for Users|The Administrator initiates a system recovery after a system failure, restoring data and access for the Lecturers and Students, ensuring continued support and interaction without disruption.|RA6, RM6, R7, RA5|

---

## 1.2 Quality Attributes

|ID|Quality Attribute|Scenario|Associated Use Case|
|--|-----------------|--------|-------------------|
|**QA-1**|**Performance**|The System responds to Student queries within 2 seconds on avergae under normal load.|UC-1|
|**QA-2**|**Security**|Only system authorized Lecturers can send annoucements to their respective courses.|UC-2|
|**QA-3**|**Usability**|The System's user interface and conversational design present student-related analytics in a clear, intuitive, and organized format allowing Lecturers to easily request and interpret data.|UC-3|
|**QA-4**|**Maintainability**|The System allows Administators and System Maintainers to deploy updates and monitoring tools continuously without disrupting user interaction|UC-5|
|**QA-5**|**Availability**|The System maintains a minimum of 99.5% available uptime duirng the academic year to ensure dependable service access.|UC-6|

---

## 1.3 Concerns

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

## 1.4 Constraints

The primary use cases that will be emphasized in this iteration are: 
- UC-1: Student Query & System Answer
- UC-2: Lecturer Announcement to Students
- UC-3: Lecture

