## Use Case Models

The AIDAP system is designed to help students, lecturers, and administrators interact with university data through a single AI-powered assistant. Below is a summary of the main use cases for each actor.

**Students**
- Ask academic or administrative questions (e.g., “When is my next exam?”)
- Receive notifications about deadlines and announcements  
- View a personalized dashboard showing schedules and performance  
- Change preferences like language and notification settings  
- Export academic events to their personal calendars  

**Lecturers**
- Publish or update course materials through the assistant  
- Post announcements or reminders for classes  
- View analytics such as attendance, grades, and engagement  
- Manage access for teaching assistants  

**Administrators**
- Manage integrations with systems like LMS, registration, and calendar  
- Define global privacy or data retention policies  
- Broadcast university-wide announcements  
- Monitor overall usage and generate reports
- The system shall provide high availability with automatic fail-over and backup recovery

**System Maintainer**
- Deploy and update the platform with minimal downtime  
- Configure and test AI models and API keys  
- Monitor the health and performance of the system  

**External Data Systems**
- Provide academic and administrative data (LMS, registration, calendar, mail)
- Allow synchronization and updates through APIs

|Use Case|Description|Associated Requirement ID|
|--------|-----------|-------------------------|
|UC-1:Student Query & System Answer|The Student Asks the system a question, the system interprets the query, then generates a response using both stored knowledge and live data.|RS1, R5, R6|
|UC-2: Lecturer Announcement to Students|The Lecturer requests to send a new announcement to their students, the systems authorizes the Lecturer's access, interprets the update, then notifies the students.| R5, RL1, RL2, RL8, RA5|
|UC-3: Lecturer Views Course Analytics Summary|The Lecturer requests a summary of their course analytics, the system interprets the query, retrieves the relevant secure data (grades, attendance, student engagment), then presents the summarized results.| RL3, RL6, R3, R4, R6, R8|
|UC-4: Administrator Broadcasts Campus-Wide Announcement|The Administrator broadcasts an announcement, the system verifies Administrator access, sends the message to the Students and Lecturers, then confirms message delivery.|RA3, RA5, R3, R4, R8, RS2|
|UC-5: Lecturer Informs Students of Low Engaement|The System detects low student engagemnet and notifies the Lecturer, the Lectuerer responds by sending a message to their students addressing the issue and encouraging participation, then the Students recieve the message through the System.| RL7, RS2, R6|
|UC-6: Administrator Recovers Data for Users|The Administrator initiates a system recovery after a system failure, restoring data and access for the Lecturers and Students, ensuring continued support and interaction without disruption.|RA6, RM6, R7, RA5|
