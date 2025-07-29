# 🧠 AI-Powered Natural Language to SQL Converter

This is a Spring Boot application that uses **OpenAI's GPT model** to convert natural language questions into valid SQL queries. It dynamically reads your database schema and crafts SQL intelligently using LLMs.

---

## 🔧 Features

- ✅ Convert plain English questions to SQL queries
- ✅ Uses OpenAI GPT models (GPT-3.5 or GPT-4)
- ✅ Extracts table and column information from your MySQL DB
- ✅ Clean RESTful architecture with Spring Boot
- ✅ Modular service + controller layer
- ✅ Extensible for query execution or UI integration

---

## 📦 Tech Stack

| Technology    | Version      |
|---------------|--------------|
| Java          | 17           |
| Spring Boot   | 3.4.2        |
| Maven         | ✔️           |
| OpenAI API    | GPT-3.5 / GPT-4 |
| Database      | MySQL        |
| ORM           | Spring Data JPA |
| REST Client   | RestTemplate |

---

## 📁 Project Structure

```
sqlproject/
├── src/
│   ├── main/
│   │   ├── java/com/llm/sqlproject/
│   │   │   ├── controller/       # API endpoints
│   │   │   ├── service/          # Core business logic
│   │   │   ├── model/            # Entity and schema representations
│   │   │   ├── repository/       # DB access
│   │   │   └── SqlProjectApp.java # Spring Boot main app
│   ├── resources/
│   │   ├── application.properties # DB & API configuration
│   │   └── schema.sql             # (Optional) Sample DB schema
├── pom.xml
└── README.md
```

---

## ⚙️ How It Works

1. **User sends a natural language query** to `/api/nl-to-sql`
2. The app **dynamically extracts schema** (tables and columns)
3. The app **sends a prompt to OpenAI** with schema + question
4. OpenAI returns an **SQL query**
5. The app **executes this SQL on MySQL**
6. The **result is returned as a JSON response**

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/sqlproject.git
cd sqlproject
```

### 2. Set Up MySQL Database

Make sure MySQL is running, and create a database:

```sql
CREATE DATABASE orders_db;
```

Populate it with some sample tables and data. Example:

```sql
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255),
    email VARCHAR(255),
    created_at DATE
);

CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    amount DECIMAL(10, 2),
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);

INSERT INTO customers (name, email, created_at) VALUES
('Alice', 'alice@example.com', '2023-01-10'),
('Bob', 'bob@example.com', '2023-02-14');

INSERT INTO orders (customer_id, amount, order_date) VALUES
(1, 120.50, '2023-03-01'),
(2, 95.00, '2023-03-05'),
(1, 180.00, '2023-03-20');
```

---

```

### 3. Add OpenAI API Key

In `src/main/resources/application.properties`, add:

```properties
# Database
spring.datasource.url=jdbc:mysql://localhost:3306/orders_db
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.jpa.hibernate.ddl-auto=none

# OpenAI
openai.api.key=sk-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
openai.model=gpt-3.5-turbo
```

Replace `yourpassword` and `sk-...` with your actual DB password and OpenAI API key.

---

## ▶️ Run the Application

```bash
mvn clean install
mvn spring-boot:run
```

Once started, the backend will be available at:

```
http://localhost:8080
```

---

## 📡 API Endpoint

### `POST /api/nl-to-sql`

#### Request:

```json
{
  "question": "Show me the customers with order amount greater than 100"
}
```

#### Response:

```json
{
  "sql": "SELECT c.name FROM customers c JOIN orders o ON c.id = o.customer_id WHERE o.amount > 100",
  "result": [
    {
      "name": "Alice"
    }
  ]
}
```

---

## 📄 Sample Prompt Sent to OpenAI

```
Given this schema:
TABLE customers(id, name, email, created_at)
TABLE orders(id, customer_id, amount, order_date)

Convert this question into SQL:
"Show me the top 5 customers by order amount"
```

---

## 💡 Use Cases

- Text-to-SQL assistants
- Data exploration tools
- Internal dashboards
- Chatbots for querying databases

---

## 📌 To-Do / Future Work

- [ ] Add SQL execution & result preview
- [ ] Add a React/Angular UI frontend
- [ ] Add query history & logging
- [ ] Support other databases like PostgreSQL or SQLite
- [ ] Query validation / explanation

---

## 🔐 How to Get OpenAI API Key

1. Go to: https://platform.openai.com/account/api-keys
2. Login with your OpenAI account
3. Generate a new API key
4. Copy and paste into `application.properties`

---

## 🧪 Testing

Run all tests:

```bash
mvn test
```

You can also write controller tests to validate prompt formation and response parsing.

---

## 🙋‍♂️ Author

Developed by [@vidhyang789](https://github.com/vidhyang789)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
