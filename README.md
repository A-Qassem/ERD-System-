erDiagram
    CENTER ||--o{ CLASSROOM : has
    CENTER ||--o{ STORAGE : contains
    CENTER ||--o{ EMPLOYEE : employs
    CENTER ||--o{ CLASS : offers
    CENTER ||--o{ PAYMENT : records
    TEACHER ||--o{ TEACHER_CENTER : assigned_to
    CENTER ||--o{ TEACHER_CENTER : includes
    TEACHER ||--o{ TEACHER_SUBJECT : teaches
    SUBJECT ||--o{ TEACHER_SUBJECT : taught_by
    STUDENT ||--o{ ATTENDANCE : recorded_in
    STUDENT ||--o{ PAYMENT : makes
    CLASS ||--o{ ATTENDANCE : tracks
    CLASS ||--o{ PAYMENT : billed_for
    CLASS }o--|| TEACHER : led_by
    CLASS }o--|| SUBJECT : covers
    CLASS }o--|| CLASSROOM : located_in
    STORAGE ||--o{ INVENTORYITEM : stores
    INVENTORYITEM ||--o{ ITEMTRANSACTION : involved_in
    EMPLOYEE ||--o{ ATTENDANCE : records
    EMPLOYEE ||--o{ PAYMENT : records
    EMPLOYEE ||--o{ ITEMTRANSACTION : records

    CENTER {
        int CenterID PK
        string Name
        string Location
        string Phone
        string FinancialManager
        datetime CreatedAt
    }

    CLASSROOM {
        int ClassroomID PK
        int CenterID FK
        string Name
        int Capacity
        string Type
    }

    STORAGE {
        int StorageID PK
        int CenterID FK
        string Name
        string Description
    }

    EMPLOYEE {
        int EmployeeID PK
        int CenterID FK
        string Name
        string Email
        string Phone
        string PasswordHash
        string Role
        date HireDate
    }

    TEACHER {
        int TeacherID PK
        string Name
        string Email
        string Phone
        string PasswordHash
        decimal PercentageRate
        date JoinedDate
    }

    TEACHER_CENTER {
        int TeacherCenterID PK
        int TeacherID FK
        int CenterID FK
        boolean Active
    }

    STUDENT {
        int StudentID PK
        string Code Unique
        string Name
        string Email
        string Phone
        string PasswordHash
        date JoinDate
        string Address
    }

    SUBJECT {
        int SubjectID PK
        string Name
        string Description
    }

    TEACHER_SUBJECT {
        int TeacherSubjectID PK
        int TeacherID FK
        int SubjectID FK
    }

    CLASS {
        int ClassID PK
        int CenterID FK
        int SubjectID FK
        int TeacherID FK
        int ClassroomID FK
        string Schedule
        decimal MonthlyFee
    }

    ATTENDANCE {
        int AttendanceID PK
        int StudentID FK
        int ClassID FK
        date Date
        string Status
        int RecordedBy FK
    }

    PAYMENT {
        int PaymentID PK
        int StudentID FK
        int ClassID FK
        int CenterID FK
        decimal Amount
        string Type
        date Date
        int RecordedBy FK
        string Notes
    }

    INVENTORYITEM {
        int ItemID PK
        int StorageID FK
        string Name
        int Quantity
        decimal CostPerUnit
        string Type
    }

    ITEMTRANSACTION {
        int TransactionID PK
        int ItemID FK
        int CenterID FK
        int QuantityChanged
        string TransactionType
        date Date
        int RecordedBy FK
    }
