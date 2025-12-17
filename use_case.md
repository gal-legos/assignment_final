## Problem Statement 
Patients who are chronically ill or have undiagnosed ongoing health conditions will often experience daily symptoms that can change between clinical visits. These fluctuations in symptoms may be critical to correctly diagnosing and treating patients. Their everyday battles can become important data points that may be beneficial to the treating physicians. These symptom diaries may also be combined with wearable devices when necessary to provide further valuable insight into patient health status. In our current state, providers lack a centralized and automated system that can continuously monitor patient data to this extent. By identifying these trends in a timely manner, it can provide doctors with early warning signs that otherwise would have gone unnoticed. The goal of this system is to use a cloud-based application that allows patients to log daily symptoms and to ingest wearable device data when required to. The system aggregates patient-reported symptoms and wearable metrics, analyzes trends, and generates alerts that are visible only to authorized providers. The goal is to support earlier intervention, improve clinical decision-making, and reduce the burden of manual symptom tracking. The primary users will be patients who submit their daily symptom reports and optional wearable data, and healthcare providers who will be reviewing the patient summaries and alerts

## Data Sources
The data sources will include patient symptom data, optional Bluetooth wearable data, optional non-Bluetooth wearable data, and processed data. For the patient symptom data, it would ideally include daily symptom logs that are submitted through the application and then stored as JSON records. The Bluetooth wearable data will include health metrics that are recorded via bluetooth enabled devices and will be synced to the application when needed by the provider. The non-Bluetooth wearable data will be health data that is retrieved from third-party cloud APIs or uploaded in scheduled batches from wearable platforms that are not Bluetooth-enabled. The inclusion of Bluetooth and non-Bluetooth data will help give providers a bigger picture when looking at patient summaries, which is part of the processed data source. Cleaned daily summaries and alert indicators derived from the raw symptom and wearable data woud be the last data source utilized.

## Basic Workflow 
1. Patients log into the application and submit daily symptom reports through a mobile-friendly web interface.

2. Based on provider settings, the application may enable wearable data integration:
    a. Bluetooth-enabled devices sync data through the app.
    b. Non-Bluetooth devices provide data via external cloud APIs or scheduled imports.

3. Raw symptom and wearable data are stored in cloud object storage for durability and auditing.

4. Cloud-based compute services process incoming data to normalize formats and remove errors.

5. Cleaned and aggregated data are written to a managed SQL database for efficient querying.

6. Alert logic evaluates symptom trends and wearable metrics against predefined thresholds or rules.

7. Authorized providers access patient summaries and flagged alerts through a secure provider-facing interface.
