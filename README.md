# 🧠 AI-Powered Natural Language to SQL Converter

This is a Spring Boot application that uses **OpenAI's GPT model** to convert user questions (in plain English) into valid SQL queries. It reads your database schema dynamically and generates queries intelligently using an LLM.

---

## 🔧 Features

- ✅ Natural language to SQL conversion using OpenAI GPT.
- ✅ Auto-detects table and column names from your database.
- ✅ Clean and modular Spring Boot backend.
- ✅ Easily extendable to execute the generated SQL queries.

---

## 📦 Tech Stack

| Technology    | Version      |
|---------------|--------------|
| Java          | 17           |
| Spring Boot   | 3.4.2        |
| Maven         | Yes          |
| OpenAI API    | GPT-3.5/4    |
| Database      | MySQL        |
| ORM           | Spring Data JPA |
| REST Client   | RestTemplate |

---

## 📁 Project Structure

sqlproject/
├── src/
│ ├── main/
│ │ ├── java/com/llm/sqlproject/
│ │ │ ├── controller/ # REST APIs
│ │ │ ├── service/ # Business logic + OpenAI integration
│ │ │ ├── model/ # JPA entities
│ │ │ ├── repository/ # Data access layer
│ │ │ └── SqlProjectApp.java
│ ├── resources/
│ │ └── application.properties
├── pom.xml
└── README.md

yaml
Copy
Edit

---

## ⚙️ How It Works

1. User sends a question like:
What are the top 5 customers by order count?

yaml
Copy
Edit
2. App extracts the DB schema (tables & columns).
3. App sends a formatted prompt to OpenAI using your API key.
4. GPT returns a valid SQL query.
5. (Optional) You can execute it using JPA or JDBC.

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/sqlproject.git
cd sqlproject
2. Configure MySQL
Create your database (example: orders_db) and set up relevant tables and data.

sql
Copy
Edit
CREATE DATABASE orders_db;
3. Add OpenAI API Key
In src/main/resources/application.properties, update:

properties
Copy
Edit
spring.datasource.url=jdbc:mysql://localhost:3306/orders_db
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.jpa.hibernate.ddl-auto=none

openai.api.key=your_openai_key
openai.model=gpt-3.5-turbo
Replace your_openai_key with your actual key from https://platform.openai.com.

▶️ Run the Application
bash
Copy
Edit
mvn clean install
mvn spring-boot:run
📡 API Endpoint
POST /api/nl-to-sql
Request:
json
Copy
Edit
{
  "question": "List all customers who ordered in the last 7 days"
}
Response:
json
Copy
Edit
{
  "sql": "SELECT * FROM customers WHERE order_date >= CURDATE() - INTERVAL 7 DAY;"
}
🔐 Get Your OpenAI API Key
Go to: https://platform.openai.com/account/api-keys

Login or sign up

Generate a new API key

Paste it in your application.properties

🧪 Future Enhancements
Query execution + result output

Frontend UI (Angular/React) for inputs and results

Auto-suggestion of queries based on schema

Export query result as CSV

👨‍💻 Author
Built with 💡 by @yourusername
Reach out on LinkedIn or raise an issue in this repo!

📄 License
This project is licensed under the MIT License.

vbnet
Copy
Edit

Let me know if:
- You’d like the query results to be included in the response.
- You want badges, Docker support, or deployment steps added.
