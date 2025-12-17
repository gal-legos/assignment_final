| Layer        | Service (Cloud)   | Role In Solution                                                                 | Related Assingment   |
| ------------ | ----------------- | -------------------------------------------------------------------------------- | -------------------- |
| Storage      | GCP Cloud storage | Stores raw JSON symptom logs and wearable event data for durability and auditing | Module 6             |
| Compute      | Cloud Run         | Hosts flask application used to collect patient symptom adn wearable data.       | Module(s) 3, 5, and 10 |
| Database/SQL | Cloud SQL         | Stores cleaned, structured, and aggregated patient summaries and alert flags     | Module(s) 7 |


## Data Flow Narrative
Step 1: Patients submit daily symptom reports through the patient app UI. Optional wearable data is included based on provider configuration.

Step 2: The patient app sends data to the Flask backend via HTTPS REST API endpoints hosted on Cloud Run.

Step 3: The Flask backend writes raw symptom and wearable data to Google Cloud Storage as JSON files for durability and traceability.

Step 4: The Flask backend cleans and aggregates incoming data and writes structured records to Cloud SQL.

Step 5: New or updated summaries trigger Cloud Functions, which evaluate rule-based thresholds and trends.

Step 6: If alert conditions are met, Cloud Functions update alert flags and metadata in Cloud SQL.

Step 7: Providers access patient summaries and alerts through the provider dashboard, which queries Cloud SQL via the Flask API.

## Security, Identity, and Governence 
Authentication and authorization are enforced at the application and cloud service levels. The Flask backend running on Cloud Run uses a dedicated service account with least-privilege IAM roles to access Cloud Storage and Cloud SQL. Provider and patient access is separated using role-based access control (RBAC) within the application, ensuring that alerts and patient summaries are visible only to authorized providers.

Sensitive credentials such as database connection strings are stored as environment variables and managed using GCP service accounts rather than hard-coded secrets. To reduce risk, the system uses simulated data only and avoids storing real protected health information (PHI). Access to cloud resources is restricted to private networks and authenticated services where possible.

## Cost and Operational Costs
Cloud Run and Cloud Functions are used to minimize costs by scaling to zero during periods of inactivity, making them well-suited for a student-budget project. Compute costs are expected to be low since workloads are event-driven and lightweight. Cloud Storage costs remain minimal due to the small size of JSON symptom and wearable data files.

Cloud SQL represents the most consistent cost component due to persistent storage and availability requirements; however, costs can be controlled by using a small instance size and limiting retention. Serverless services are favored over always-on virtual machines to reduce operational overhead while still supporting scalability and reliability.