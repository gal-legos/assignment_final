# Reflection

## Confidence in the Design

The part of this design I feel most confident about is the overall cloud architecture and service selection. The separation between the frontend/access layer, compute layer, and data layer is clear and aligns well with common cloud-native design patterns. Using Google Cloud Run for the Flask application and Cloud Functions for alert processing provides a useable, serverless-first approach that is cost-effective and appropriate for a healthcare monitoring application. The data flow from raw data in Cloud Storage to structured summaries in Cloud SQL is also straightforward and easy. I am also confident in the alerting workflow. Placing alert logic in Cloud Functions ensures that alerts are evaluated only when new or updated data is available, rather than continuously polling the database. This design minimizes cost, reduces unnecessary compute usage, and supports future expansion to more advanced analytics or machine learning-based alerting if needed.

## Areas of Uncertainty

The area I am least confident about is wearable device integration, particularly how different vendors expose data through APIs and how frequently data can be synchronized. In this design, wearable data ingestion is intentionally abstracted to avoid dependency on specific vendors or hardware. While this abstraction keeps the project within scope, a real-world implementation would require deeper consideration of API rate limits, data normalization challenges, and device-specific authentication workflows. 

## Alternative Architecture Considered

An alternative architecture considered was deploying the Flask application on a persistent Google Compute Engine virtual machine instead of using Cloud Run. While this approach would provide greater control over the runtime environment, it would introduce additional operational overhead, higher costs, and the need for manual scaling and maintenance. Given the event-driven and intermittent nature of symptom reporting, Cloud Run was a better fit.


## Future Improvements

If given an additional four to eight weeks and unlimited cloud credits, the next steps would include implementing a fully functional prototype with user authentication, provider-specific dashboards, and richer visualization of symptom trends. Additional enhancements could include integrating a machine learning model in Vertex AI to detect anomalies or predict worsening conditions based on historical data. Other future improvements would involve implementing stronger security controls, such as fine-grained IAM policies, encrypted secrets management, and automated audit logging. Support for real wearable device APIs and real-time streaming data ingestion could also be added to make the system closer to a production-ready healthcare application.
