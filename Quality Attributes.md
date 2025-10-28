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