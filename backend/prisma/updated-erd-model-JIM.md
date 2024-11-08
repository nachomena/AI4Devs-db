erDiagram
COMPANY {
int id PK
string name
}

    EMPLOYEE {
        int id PK
        int company_id FK
        string name
        string email
        string role
        boolean is_active
    }

    INTERVIEW_TYPE {
        int id PK
        string name
        text description
    }

    INTERVIEW_FLOW {
        int id PK
        text description
    }

    INTERVIEW_STEP {
        int id PK
        int interview_flow_id FK
        int interview_type_id FK
        string name
        int order_index
    }

    POSITION {
        int id PK
        int company_id FK
        int interview_flow_id FK
        string title
        text description
        string status
        boolean is_visible
        string location
        text job_description
        text requirements
        text responsibilities
        numeric salary_min
        numeric salary_max
        string employment_type
        text benefits
        text company_description
        date application_deadline
        string contact_info
    }

    CANDIDATE {
        int id PK
        string first_name
        string last_name
        string email
        string phone
        string address
    }

    APPLICATION {
        int id PK
        int position_id FK
        int candidate_id FK
        date application_date
        string status
        text notes
    }

    INTERVIEW {
        int id PK
        int application_id FK
        int interview_step_id FK
        int employee_id FK
        date interview_date
        string result
        int score
        text notes
    }

    EDUCATION {
        int id PK
        string institution
        string title
        date start_date
        date end_date
        int candidate_id FK
    }

    WORK_EXPERIENCE {
        int id PK
        string company
        string position
        string description
        date start_date
        date end_date
        int candidate_id FK
    }

    RESUME {
        int id PK
        string file_path
        string file_type
        date upload_date
        int candidate_id FK
    }

    COMPANY ||--o{ EMPLOYEE : employs
    COMPANY ||--o{ POSITION : offers
    POSITION ||--|| INTERVIEW_FLOW : assigns
    INTERVIEW_FLOW ||--o{ INTERVIEW_STEP : contains
    INTERVIEW_STEP ||--|| INTERVIEW_TYPE : uses
    POSITION ||--o{ APPLICATION : receives
    CANDIDATE ||--o{ APPLICATION : submits
    APPLICATION ||--o{ INTERVIEW : has
    INTERVIEW ||--|| INTERVIEW_STEP : consists_of
    EMPLOYEE ||--o{ INTERVIEW : conducts
    CANDIDATE ||--o{ EDUCATION : has
    CANDIDATE ||--o{ WORK_EXPERIENCE : has
    CANDIDATE ||--o{ RESUME : uploads
