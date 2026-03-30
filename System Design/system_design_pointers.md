# System Design Pointers

Things to keep in mind while designing an architecture:
- Design the system based on your knowledge.
- Split the requirement into 6 parts:
  - Decide the target database (Snowflake/Redshift).
  - Data extraction/ingestion from sources.
  - Data loading into target database.
  - Data transformation tools/methodology.
  - Scheduling mechanism.
  - CI/CD and Dev Ops.

Analyze your design/architecture with respect to the following points:
1. Target Database ACID Compliance:
  * ACID (Atomicity, Consistency, Isolation, Durability) refers to a standard set of properties that guarantee database transactions are processed reliably.
    * Atomicity means that either all transactions succeed or no transactions succeed. There is no possibility of some transactions succeeding and others failing.
    * Consistency ensures that all data will be consistent.
    * Isolation guarantees that all transactions will occur in isolation, meaning no transaction will be affected by another transaction. A transaction cannot read data from another transaction that has not completed.
    * Durability ensures that, once a transaction is committed, it will remain in the system even if there is a system crash immediately following the transaction.
2. Data Partitioning and Change Data Capture
3. Support and Community
4. **Fault Tolerance**
5. **Data Lineage - Optional**
6. **Data Governance - Optional**
7. **Data Quality - Optional**
8. **Data/Failure Recovery**
9. Alerts and Monitoring
10. Scheduling Mechanism
  * Dependency Management
  * Compatibility with ETL tools
  * API Access
  * Error Handling
  * Monitoring and Logging
  * User Friendly/Interface
  * Alerts and Notifications