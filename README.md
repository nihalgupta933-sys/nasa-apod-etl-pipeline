# 🌌 NASA APOD ETL Pipeline with Apache Airflow & PostgreSQL

An automated data engineering pipeline that orchestrates the daily extraction, transformation, and loading (ETL) of NASA's Astronomy Picture of the Day (APOD) metadata into a local containerized PostgreSQL database.

## 🚀 Architecture Overview
- **Framework & Runtime:** Powered by Astro (Astronomer CLI) for robust local dependency management and scaffolding.
- **Orchestration Engine:** Apache Airflow 2.x utilizing the modern TaskFlow API (`@task` decorator) mixed with traditional operators.
- **Data Source Ingestion:** Integrated directly with the **NASA Open API Engine** (`planetary/apod`) to fetch high-resolution cosmic metadata daily.
- **Target Storage Engine:** PostgreSQL 13 running within an isolated Docker network.

---

## 🛠️ Pipeline Workflow (DAG: `nasa_postgres`)

1. **DDL Pre-checks (`create_table`):** Initializes a connection via `PostgresHook` to check and generate the target database schema structure safely.
2. **Data Extraction (`extract_apod`):** A dedicated `HttpOperator` securely passes environment configurations to pull daily JSON telemetry payloads from the NASA API.
3. **Data Transformation (`transform_apod_data`):** Python dictionary parsing normalizes unstructured responses, filtering default fallbacks for potential missing API fields.
4. **Data Loading (`load_data_to_postgres`):** Uses parameterized multi-variable inputs via raw SQL execution to prevent injection attacks and commit rows to the storage layer.

---

## 📊 Project Visuals & Execution Monitoring

### 💻 Code Construction
The core ETL pipeline is modularized using custom Airflow connections to completely separate database targets and external API authentication secrets from source control.
![Local Development Environment](./ss/Screenshot%202026-08-22%20131117.png)

### ⚙️ Database Network Orchestration
A custom environment using Docker Compose powers our back-end infrastructure microservices (Postgres, database migrations, scheduler, and web server triggers) simultaneously.
![Docker Container Infrasructure](./ss/Screenshot%202026-08-22%20132522.png)

### 🔌 Verified Airflow Connections
Secure connections for both the destination database mapping layer (`my_postgres_connection`) and the target network ingestion endpoint (`nasa_api`) are managed natively within Airflow Admin parameters.
![Airflow UI Connections Setup](./ss/Screenshot%202026-08-22%20131254.png)

### 📈 Task Execution View & Real-time Logs
A complete graph view layout of the DAG runtime environment executing sequentially across our discrete extraction, validation, and storage functions.
![Airflow Dag Tasks Flow](./ss/Screenshot%202026-08-22%20131441.png)

### 🔄 Debugging History & Code Optimization
The pipeline status chart highlights our development lifecycle. The initial red markings show runtime mapping failures encountered while testing and refining database constraint criteria. After debugging structural column mappings, the sequential runs execute completely green—achieving 100% data execution success.
![Airflow DAG History Status](./ss/Screenshot%202026-08-22%20130819.png)

### 📦 Output Verification (Target Database Payload)
Executing an active analytical query (`SELECT * FROM apod_data;`) via DB-Viewer confirms that incoming raw payloads from NASA are transformed and loaded securely into our table.
![PostgreSQL Target Table Metadata Verification](./ss/Screenshot%202026-08-22%20131653.png)

---

## 🚧 Current Deployment Progress (Astronomer Cloud)

Our production instance profile (`nasa-etl-prod`) is up, running, and completely healthy within the Astro Platform interface. All secure data connections are successfully mapped out behind the scenes. 

*Note: I am currently addressing an issue where core DAG files are not resolving visually inside the platform cloud view. Local functionality remains fully stable, and a cloud-sync solution is currently in development.*
![Astro Deployment Dashboard UI](./ss/Screenshot%202026-08-22%20141201.png)
