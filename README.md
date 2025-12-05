README.md — Dockerized Python + PostgreSQL App
 Project Overview
This project demonstrates how to:
Build a simple Python application
Connect it to a PostgreSQL database
Dockerize both services
Run everything using Docker Compose
The Python app:
Waits for PostgreSQL to be ready
Creates a table named people
Inserts a row
Reads and prints that row
This project is ideal for Beginners learning Docker, DevOps, or QA Automation.
🏗️ Project Structure
dockerized-postgres-app/
│── docker-compose.yml
│── app/
│     ├── app.py
│     ├── requirements.txt
│     └── Dockerfile
🚀 How It Works
1. PostgreSQL Service
The db service runs PostgreSQL with:
Database: mydb
User: user
Password: pass
A Docker volume stores the database data.
2. Python App Service
The app service:
Builds from the Dockerfile inside /app
Installs dependencies (psycopg2-binary)
Runs the Python script app.py
Connects to PostgreSQL using environment variables
🐳 Docker Compose Configuration
Your docker-compose.yml defines two services:
services:
  db:
    image: postgres:15-alpine
    container_name: dp_postgres
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb
    volumes:
      - pg-data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user -d mydb"]
      interval: 5s
      timeout: 5s
      retries: 10
  app:
    build:
      context: ./app
      dockerfile: Dockerfile
    container_name: dp_app
    depends_on:
      db:
        condition: service_healthy
    environment:
      POSTGRES_HOST: db
      POSTGRES_PORT: 5432
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
volumes:
  pg-data:
🧪 Python Script Behavior
Your app.py:
Waits until PostgreSQL is ready
Connects to the database
Creates table people
Inserts a row ('Docker User')
Reads and prints the row
Example output:
Postgres is ready!
Inserted ID: 1
Row: (1, 'Docker User')
▶️ How to Run the Project
1. Navigate to project folder
cd dockerized-postgres-app
2. Start Docker Compose
docker compose up --build
3. Watch the logs
PostgreSQL initializes
Python waits for DB
Python app inserts & reads data
Container exits with code 0 (success)
🛑 Stopping the Project
Press:
CTRL + C
Then run:
docker compose down
To remove database data too:
docker compose down -v
📦 Technologies Used
Python 3.10
PostgreSQL 15
Docker
Docker Compose
🌱 Learning Outcomes
By completing this project, you learned:
✔ How to write a Python app that connects to PostgreSQL
✔ How to create a Dockerfile
✔ How to use Docker Compose for multi-container apps
✔ How to use health checks
✔ How to automate app startup dependencies
✔ How containers communicate over a Docker network
🚀 Next Steps (Optional Enhancements)
You can extend this project by adding:
Flask API to insert/read data
pgAdmin for GUI access
Environment variables via .env file
CI/CD pipeline (GitHub Actions)
Docker Hub image publishing
Tell me if you want any of these and I’ll help you build it!
