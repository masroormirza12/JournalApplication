🧠 JournalApplication (Backend - Spring Boot)
A backend-only journal application built using Spring Boot, offering secure journaling with JWT + OAuth authentication, sentiment-driven mail alerts, Kafka messaging, and role-based access control — all persisted in MongoDB.

🚦 Features Overview
✅ User Sign-up & Login (JWT Auth)

🔐 OAuth2.0 Integration (Google, etc.)

📓 Journal CRUD (admin-managed, user-selectable)

📬 Email Triggering (Kafka → SMTP fallback)

🧠 Sentiment Analysis on journal entries

📡 Health-check public API (/api/public/health-check)

🧪 JUnit Testing + Khusko AI for API validation

🗂️ Role-based authorization: ROLE_USER, ROLE_ADMIN

🔄 System Flow Diagram
mermaid
Copy
Edit
flowchart TD
    A[User Signup/Login] -->|JWT/OAuth| B[Authentication Service]
    B --> C[Role Checker]
    C -->|ROLE_USER| D[Select Journals]
    C -->|ROLE_ADMIN| E[Manage Journals]
    D --> F[Sentiment Engine]
    F --> G[Kafka Topic (mail)]
    G -->|If fail| H[SMTP Mail Sender]
    H --> I[User Email Inbox]
🛠️ Technology Stack
Component	Technology Used
Backend Framework	Spring Boot (Java)
Auth	JWT + Spring Security + OAuth2
DB	MongoDB
Email	Kafka + SMTP fallback
Testing	JUnit, Khusko AI
Build Tool	Maven
📁 Project Structure
bash
Copy
Edit
JournalApplication/
│
├── controller/          # API endpoints
├── model/               # Entity classes (User, Journal, etc.)
├── service/             # Business logic
├── repository/          # MongoDB Repositories
├── security/            # JWT, OAuth2 configurations
├── kafka/               # Kafka producer/consumer
└── config/              # App configs
🚀 Running the Project
bash
Copy
Edit
# Clone repo
git clone https://github.com/masroormirza12/JournalApplication.git
cd JournalApplication

# Build & run
./mvnw clean install
./mvnw spring-boot:run
🔑 Roles & Access
Role	Access
Admin	Full CRUD on journals, view all users
User	View/select journals, sentiment analysis, receive alerts
📬 Email Architecture
mermaid
Copy
Edit
sequenceDiagram
  participant App as Spring Boot App
  participant Kafka as Kafka Topic
  participant SMTP as SMTP Mail Service
  participant User as User Email

  App->>Kafka: Publish sentiment-based mail request
  Kafka-->>App: (Fails)
  App->>SMTP: Send mail directly
  SMTP->>User: Email delivered
🧪 Testing & Quality
✔️ Unit Testing: JUnit 5

✔️ API Testing: Khusko AI

✔️ Health Check: /api/public/health-check

📬 Mail Trigger Logic
On journal selection or update, the sentiment of previous journals is analyzed.

If a mail should be sent, it’s pushed to Kafka.

If Kafka is unavailable, fallback is SMTP-based direct mailing.

🧑‍💻 Want to Contribute?
Fork the repo

Create a feature branch

Push your changes

Open a Pull Request 🚀
