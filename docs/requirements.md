
# Health MVP Deployment Project Requirements

This document outlines the core requirements for the Minimum Viable Product (MVP) of the Health Web App and its supporting DevOps infrastructure.

## 1. Functional Requirements (What the app does)

* **F1. Data Persistence:** The application must successfully connect to the **PostgreSQL** database.
* **F2. Simple Read/Write:** Users must be able to submit a simple entry (e.g., a "Mood Check-in" or a "Daily Water Intake" record) via a web form.
* **F3. Data Display:** The application's homepage must display the 5 most recent entries retrieved from the database.
* **F4. Health Check Endpoint:** A dedicated `/health` endpoint must exist that returns a successful HTTP 200 status code and the current server date.

## 2. Non-Functional Requirements (How the app runs)

* **N1. Infrastructure as Code (IaC):** The entire AWS infrastructure (VPC, EC2 instance, Security Groups, IAM roles) must be defined and provisioned using **Terraform**.
* **N2. Containerization:** The Node.js application must be packaged and run inside a **Docker container**.
* **N3. Continuous Integration/Continuous Deployment (CI/CD):**
    * A **GitHub Actions** pipeline must be implemented.
    * The pipeline must automatically **build** the Docker image, **push** it to a container registry (e.g., Docker Hub or AWS ECR), and **deploy** the application to the AWS EC2 instance upon every successful merge to the `main` branch.
* **N4. Security:** The EC2 instance must only be accessible via SSH through a bastion host or restricted Security Group rules (e.g., only open to your IP address). The database credentials must be handled securely (e.g., using environment variables).
* **N5. Idempotency:** The deployment process (both IaC and CI/CD) must be repeatable without causing unintended side effects.