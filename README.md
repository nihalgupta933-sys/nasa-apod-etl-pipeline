## 📊 Project Visuals & Execution Monitoring

### 1. 💻 Code Construction & DAG Definition
The core ETL pipeline is modularized within VS Code using custom Airflow connection hooks to keep database credentials and external API authentication secrets safely out of source control.
![Local Development Environment](./ss/Screenshot%202026-08-22%20131117.png)

### 2. 🔄 Debugging History & Run Optimization
The pipeline status chart highlights our development lifecycle. The initial red markings show runtime mapping failures encountered while testing and refining database constraint criteria. After debugging structural column mappings, the sequential runs execute completely green—achieving 100% data execution success.
![Airflow DAG History Status](./ss/Screenshot%202026-08-22%20131052.png)

### 3. 🔌 Verified Airflow Connections
Secure connections for both the destination database mapping layer (`my_postgres_connection`) and the target network ingestion endpoint (`nasa_api`) are managed natively within Airflow Admin parameters.
![Airflow UI Connections Setup](./ss/Screenshot%202026-08-22%20131254.png)

### 4. 📈 Task Execution View & Real-time Logs
A complete graph view layout of the DAG runtime environment executing sequentially across our discrete extraction, validation, and storage functions.
![Airflow Dag Tasks Flow](./ss/Screenshot%202026-08-22%20131441.png)

### 5. 🔄 Data Transformation Payload (XComs)
Verifying raw key-value payload transfers between task boundaries using native Airflow XCom metadata exchange storage rules.
![Airflow XCom Data Flow](./ss/Screenshot%202026-08-22%20131653.png)

### 6. ⚙️ Database Network Orchestration
A containerized environment using Docker Compose powers our back-end infrastructure microservices (Postgres, database migrations, scheduler, and web server triggers) simultaneously.
![Docker Container Infrastructure](./ss/Screenshot%202026-08-22%20132522.png)

### 📦 7. Output Verification (Target Database Payload)
Executing an active analytical query (`SELECT * FROM apod_data;`) via DBeaver confirms that incoming raw payloads from NASA are transformed and loaded securely into our table.
![PostgreSQL Target Table Metadata Verification](./ss/Screenshot%202026-08-22%20131135.png)

---

## 🚧 Current Deployment Progress (Astronomer Cloud)

Our production instance profile (`nasa-etl-prod`) is up, running, and completely healthy within the Astro Platform interface. All secure data connections are successfully mapped out behind the scenes. 

*Note: I am currently addressing an issue where core DAG files are not resolving visually inside the platform cloud view. Local functionality remains fully stable, and a cloud-sync solution is currently in development.*
![Astro Deployment Dashboard UI](./ss/Screenshot%202026-08-22%20141201.png)
