# Class Diagram

```mermaid
classDiagram
    direction TB

    class User {
        +String id
        +String name
        +String email
        +String passwordHash
        +Enum role
        +DateTime createdAt
        +register()
        +login()
        +logout()
    }

    class ArchitectProfile {
        +String userId
        +String bio
        +String location
        +String specialization
        +Float rating
        +updateProfile()
        +getProjects()
        +getDashboardStats()
    }

    class ClientProfile {
        +String userId
        +String phone
        +getBookmarks()
        +getSentInquiries()
    }

    class Admin {
        +String userId
        +approveProject()
        +rejectProject()
        +removeUser()
    }

    class Project {
        +String architectId
        +String title
        +String category
        +Integer year
        +Enum status
        +create()
        +update()
        +delete()
    }

    class ProjectImage {
        +String projectId
        +String imageUrl
        +Boolean isPrimary
    }

    class Inquiry {
        +String clientId
        +String architectId
        +String projectId
        +String message
        +Enum status
        +send()
        +markAsRead()
    }

    class InquiryReply {
        +String inquiryId
        +String senderId
        +String message
        +DateTime createdAt
    }

    class Bookmark {
        +String clientId
        +String projectId
        +DateTime savedAt
        +add()
        +remove()
    }

    User <|-- ArchitectProfile : extends
    User <|-- ClientProfile : extends
    User <|-- Admin : extends

    ArchitectProfile "1" --> "0..*" Project : posts
    Project "1" --> "0..*" ProjectImage : has

    ClientProfile "1" --> "0..*" Inquiry : sends
    ArchitectProfile "1" --> "0..*" Inquiry : receives
    Inquiry "1" --> "0..*" InquiryReply : has

    ClientProfile "1" --> "0..*" Bookmark : saves
    Bookmark "0..*" --> "1" Project : references
```
