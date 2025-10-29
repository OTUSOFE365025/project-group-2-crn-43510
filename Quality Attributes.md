## Quality Attributes

The main quality goals drive the architecture decisions. Each one maps to user needs or explicit requirements.

| Attribute | Reason |
|------------|---------|
| **Performance** | The system should respond to most queries within 2 seconds to keep the conversation natural. |
| **Availability** | Needs to stay up at least 99.5% of the time to be useful during the academic year. |
| **Scalability** | Must support growth up to around 5,000 concurrent users as usage expands. |
| **Security and Privacy** | Uses institutional SSO and must comply with campus privacy policies. |
| **Usability** | Conversational design should feel simple and intuitive across text and voice. |
| **Reliability** | Must handle temporary data source failures without crashing. |
| **Modifiability** | Easy integration of future AI models or new external data systems. |
| **Maintainability** | Should allow continuous deployment and clear monitoring tools. |

---

|ID|Quality Attribute|Scenario|Associated Use Case|
|--|-----------------|--------|-------------------|
|**QA-1**|**Performance**|The System responds to Student queries within 2 seconds on avergae under normal load.|UC-1|
|**QA-2**|**Security**|Only system authorized Lecturers can send annoucements to their respective courses.|UC-2|
|**QA-3**|**Usability**|The System's user interface and conversational design present student-related analytics in a clear, intuitive, and organized format allowing Lecturers to easily request and interpret data.|UC-3|
|**QA-4**|**Maintainability**|The System allows Administators and System Maintainers to deploy updates and monitoring tools continuously without disrupting user interaction|UC-5|
|**QA-5**|**Availability**|The System maintains a minimum of 99.5% available uptime duirng the academic year to ensure dependable service access.|UC-6|

---
