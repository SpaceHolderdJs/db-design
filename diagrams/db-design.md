# PostgreSQL Database Relations Diagram (DB Design)

```mermaid
erDiagram
    USERS ||--|| USER_DETAILS : "has"
    USERS ||--|| USER_AUTH : "has"
    USERS ||--o{ ADDRESSES : "has"
    USERS ||--o{ TASKS : "assigned to"
    USERS ||--|| SETTINGS : "has"
    USERS ||--o{ NOTIFICATIONS : "receives"
    USERS ||--o{ PAYMENTS: "receives"
    USERS ||--o{ WITHDRAWS : "requests"
    USERS ||--o{ REFERRALS : "has"
    USERS ||--|| APPLICATIONS : "submits"
    USERS ||--o{ USER_RATINGS : "has"
    WITHDRAWS ||--|| WITHDRAW_STATUSES : "has"
    PAYMENTS ||--|| PAYMENTS_STATUSES : "has"
    USERS ||--o{ VIDEOS : "uploads"
    TASKS ||--o{ VIDEOS : "has"
    TASKS }|--|| TASK_STATUSES : "has"
    TASKS ||--|| PAYMENTS : "associated with"
    TASKS ||--|| APPLICATIONS : "has"
    APPLICATIONS ||--|| APPLICATION_STATUSES : "has"

    USERS {
        int id PK
        string username
        string email
    }
    USER_DETAILS {
        int id PK
        int user_id FK
        string country
        string gender
        date DOB
        float delivery_percentage
        boolean is_locked
        string image_url
    }
    USER_AUTH {
        int id PK
        int user_id FK
        string hashed_password
        string google_token
        string facebook_token
    }
    USER_RATINGS {
        int id PK
        int user_id FK
        float rating
        date created_at
        date updated_at
    }
    ADDRESSES {
        int id PK
        int user_id FK
        string full
        string street
        string district
        string house
        string city
        float lat
        float lon
    }
    SETTINGS {
        int id PK
        int user_id FK
        string facebook_connection_token
        string google_connection_token
    }
    TASKS {
        int id PK
        string title
        string type
        text description
        date due_date
        int user_id FK
        int status_id FK
    }
    TASK_STATUSES {
        int id PK
        string name
    }
    NOTIFICATIONS {
        int id PK
        int user_id FK
        string message
        boolean is_read
        date created_at
    }
    WITHDRAWS {
        int id PK
        int user_id FK
        float amount
        string payment_details
        string stripe_token
        string receiver
        date created_at
    }
    WITHDRAW_STATUSES {
         int id PK
         enum name
    }
    PAYMENTS {
        int id PK
        int user_id FK
        int task_id FK
        float amount
        string payment_details
        string stripe_token
        string receiver
        date created_at
    }
    PAYMENTS_STATUSES {
         int id PK
         enum name
    }
    VIDEOS {
        int id PK
        int user_id FK
        int task_id FK
        string title
        date uploaded_at
        string content_url
        enum type
    }
    REFERRALS {
        int id PK
        int user_id FK
        string referral_code
        int referred_user_id FK
        date created_at
    }
    APPLICATIONS {
        int id PK
        int task_id FK
        int user_id FK
        enum status
        date applied_at
    }
    APPLICATION_STATUSES {
         int id PK
         enum name
    }
```
