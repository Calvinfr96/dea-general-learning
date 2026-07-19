# AWS Athena Interview Questions

## Basic Questions
1. What is AWS Athena?
    - Answer: AWS Athena is an interactive query service that allows users to analyze data stored in Amazon S3 using standard SQL. It is serverless, meaning there is no need to manage infrastructure, and users pay only for the queries they run.

1. How does AWS Athena work?
    - Answer: Athena works by running queries on data stored in Amazon S3 using Presto, a distributed SQL query engine. It uses the AWS Glue Data Catalog to manage metadata and schema information.

1. What types of data can you analyze using AWS Athena?
    - Answer: Athena can analyze structured, semi-structured, and unstructured data stored in formats like CSV, JSON, Parquet, ORC, and Avro in Amazon S3.

1. What are the benefits of using AWS Athena?
    - Answer: Benefits include serverless architecture, ease of use with SQL, integration with AWS Glue for data cataloging, cost-effectiveness (pay-per-query), and scalability.

1. How does AWS Athena integrate with AWS Glue?
    - Answer: AWS Glue provides a Data Catalog that stores metadata for data sources. Athena uses this catalog to retrieve schema information when executing queries.

1. What data formats are best suited for use with AWS Athena?
    - Answer: Optimized data formats like Parquet and ORC are preferred because they support columnar storage, which reduces the amount of data scanned and speeds up query performance.

1. Why is it important to optimize data for querying in Athena?
    - Answer: Optimizing data reduces the amount of data scanned per query, which lowers costs and improves query performance.

1. Can you explain the difference between partitioning and bucketing in Athena?
    - Answer: Partitioning divides data into segments based on a key (e.g., date), allowing queries to skip irrelevant partitions. Bucketing divides data into a fixed number of files (buckets) based on a hash function, which can improve query performance by organizing data more efficiently.

1. How do you create a table in Athena?
    - Answer: A table can be created using the SQL `CREATE TABLE` statement, specifying the data location in S3 and the schema.

1. What is the maximum query timeout in AWS Athena?
    - Answer: The maximum query timeout for AWS Athena is 30 minutes.

1. How can you improve query performance in AWS Athena?
    - Answer: Improving query performance can be achieved by using partitioning and bucketing, choosing efficient file formats, reducing data size, and writing optimized SQL queries.

1. What are some best practices for writing SQL queries in Athena?
    - Answer: Best practices include selecting only necessary columns, using `WHERE` clauses to filter data, avoiding `SELECT *`, and leveraging partitioning effectively.

1. How can you secure data in AWS Athena?
    - Answer: Data can be secured using AWS Identity and Access Management (IAM) policies, AWS Key Management Service (KMS) for encryption, and securing S3 bucket policies.

1. What is AWS Lake Formation, and how does it relate to Athena?
    - Answer: AWS Lake Formation is a service that simplifies setting up a secure data lake. It integrates with Athena to provide data cataloging, security, and access controls.

1. How does AWS Athena handle schema evolution?
    - Answer: Athena supports schema evolution, allowing users to modify table schemas to accommodate changes in data without needing to rewrite existing data.

1. What happens to the data in S3 when you drop a table in Athena?
    - Answer: Dropping a table in Athena removes the table metadata but does not delete the actual data stored in S3.

1. How is pricing determined in AWS Athena?
    - Answer: Pricing is based on **the amount of data scanned** by each query. Users are charged per terabyte (TB) of data scanned.

1. What strategies can you use to minimize costs when using AWS Athena?
    - Answer: Strategies include using compressed file formats, partitioning data, selecting specific columns, and using views to optimize queries.

1. What is the AWS Athena Data Catalog?
    - Answer: The Data Catalog is a persistent metadata repository that stores schema information, allowing users to manage tables and metadata for datasets stored in S3.

1. How do you work with JSON data in AWS Athena?
    - Answer: JSON data can be queried directly using Athena by defining the schema in a table and utilizing functions like json_extract to access nested fields.

1. What are some limitations of AWS Athena?
    - Answer: Limitations include the maximum timeout of 30 minutes per query, a limit on the number of partitions per table (currently 20,000), and no support for stored procedures.

1. How does Athena handle data versioning?
    - Answer: Athena does not natively support data versioning. However, users can implement versioning in S3 and manage versions via naming conventions.

1. What challenges might you face when using AWS Athena with large datasets?
    - Answer: Challenges include long query times, high costs due to data scanning, and potential performance issues with complex queries.

1. How do you troubleshoot slow queries in AWS Athena?
    - Answer: Troubleshooting steps include analyzing the query execution plan, optimizing the data format and partitioning, and reviewing the amount of data scanned.

1. How can you optimize query performance in AWS Athena?
    - Answer: Query performance can be optimized by ensuring proper partitioning, using efficient file formats, and simplifying complex queries.

1. What is the role of the Query Execution Engine in Athena?
    - Answer: The Query Execution Engine in Athena is responsible for parsing SQL queries, optimizing them, and executing them against the underlying data in S3.

1. How do you handle errors in AWS Athena queries?
    - Answer: Handling errors involves reviewing error messages provided by Athena, checking SQL syntax, and validating the schema and data types in S3.

1. How can you ensure data quality in AWS Athena?
    - Answer: Ensuring data quality involves validating data schemas, conducting regular audits of data in S3, and monitoring query results for anomalies.

1. What is federated querying in AWS Athena?
    - Answer: Federated querying allows Athena to run queries against data stored in different sources, such as RDS or DynamoDB, in addition to S3.

1. How does AWS Athena scale to handle large datasets?
    - Answer: Athena scales automatically to handle large datasets by distributing query processing across multiple nodes.

1. What is the significance of the AWS Athena query history?
    - Answer: Query history provides insights into past queries, helping users optimize performance, troubleshoot issues, and track usage patterns.

1. How do you manage data lifecycle policies in S3 for Athena?
    - Answer: S3 lifecycle policies can automatically transition or delete data after a certain period, helping to manage costs and storage.

1. How does AWS Athena compare with traditional data warehousing solutions?
    - Answer: Unlike traditional data warehouses, Athena is serverless, requiring no infrastructure management, and it operates directly on data in S3, offering flexibility and cost savings.

1. What factors would you consider when deciding between using Athena and a data warehouse?
    - Answer: Factors include data size, query complexity, required performance, cost considerations, and the need for real-time data processing.

## Scenario-Based Questions
1. You used Athena to query data. Why didn't you just load the data into a database like MySQL or Redshift first?
    - The Answer: We chose Athena for its Serverless and Ad-Hoc nature.
    - No ETL Required: Loading data into Redshift or MySQL takes time (ETL pipeline) and costs money for running servers 24/7.
    - Schema-on-Read: With Athena, the data stays in S3 in its raw format (CSV/JSON). We just define a table structure on top of it.
    - Use Case: It was perfect for our data scientists who needed to explore raw logs immediately without waiting for a formal data warehouse pipeline to be built.

1. How does Athena charge you? Is it per hour or per user?
    - The Answer: Neither. Athena charges Per Terabyte Scanned (roughly $5 per TB).
    - The Implication: This dictates how we write queries. If I run `SELECT * FROM table`, Athena scans every single file in the S3 bucket, which is expensive.
    - The Goal: My primary job as a Data Engineer is to reduce the amount of data scanned by using Partitioning and Columnar Formats.

1. You created a table in Athena. Where is the data actually stored?
    - The Answer: The data is stored in Amazon S3, not in Athena.
    - The Separation: Athena is just a query engine (based on Presto/Trino). It has no storage of its own.
    - The Metadata: The table definitions (schema, column names) are stored in the AWS Glue Data Catalog.
    - The Flow: When I run a query, Athena looks up the schema in Glue, uses that map to read files from S3, processes them in memory, and returns the result.

1. We have a 1TB JSON dataset. Queries are taking 3 minutes and costing $5 per run. How do you optimize this without changing the query?
    - The Answer: I would convert the data to Parquet or ORC format.
    - The Problem with JSON: It is row-based and uncompressed. To read one column (user_id), Athena has to parse the entire JSON file.
    - The Solution: Parquet is Columnar.
    - Compression: It reduces the 1TB file to ~200GB (Snappy compression).
    - Column Pruning: If I select only user_id, Athena grabs only that specific chunk of the file and ignores the rest.
    - Result: The query scans 10GB instead of 1TB, making it 100x cheaper and much faster.

1. Explain Partitioning in Athena. How does it save money?
    - The Answer: Partitioning organizes files into folders like `s3://bucket/data/year=2024/month=01/`.
    - Without Partitioning: A query for 'January 2024' scans the entire bucket (all years).
    - With Partitioning: Athena sees the `WHERE month='01'` clause and physically skips all other folders.
    - Gotcha: We must run `MSCK REPAIR TABLE` (or use a Glue Crawler) after adding new folders so Athena knows they exist.
    - Warning: Too many partitions (e.g., partitioning by second) creates the 'Small Files Problem', which slows down metadata listing.

1. What is CTAS (Create Table As Select) and when do you use it?
    - The Answer: CTAS is a command to query data and write the results back to S3 immediately.
    - Use Case (ETL): I use it to convert formats or aggregate data.
        ```
        CREATE TABLE sales_parquet
        WITH (format = 'PARQUET', external_location = 's3://bucket/processed/')
        AS SELECT * FROM raw_sales_csv;
        ```
    - Benefit: It transforms the data into an optimized format (Parquet) in a single step, making future queries faster.

1. We have data in S3, but we also need to join it with a 'User Profile' table that lives in DynamoDB. Do we have to export DynamoDB to S3 first?
    - The Answer: No, we can use Athena Federated Query.
    - How it works: We deploy a Lambda Data Connector.
        - The Execution: When Athena executes the SQL, it identifies that User_Profile is a DynamoDB table. It triggers the Lambda function to fetch only the relevant rows from DynamoDB and joins them with the S3 data in memory.
    - Benefit: This allows 'Data Mesh' style querying across disparate sources (RDS, Redis, DynamoDB) without building complex ETL pipelines to move everything into one place.

1. We have huge number of partitions (e.g., Logs partitioned by IP_Address). The Glue Crawler takes hours to run, and Athena times out just listing the partitions. How do you fix this?
    - The Answer: We should switch to Partition Projection.
    - The Problem: Standard partitioning relies on the Glue Catalog listing every single folder in S3. If you have 1 million folders, the overhead is massive.
    - The Solution: We define the partition structure in the table properties (e.g., 'Dates range from 2020 to 2030').
    - The Result: Athena can now calculate the folder paths in-memory (mathematically), instead of calling the Glue Catalog API to list them. This makes query planning instantaneous, even for tables with millions of partitions.

1. Athena is read-only. How do you handle 'Updates' or 'Deletes' (e.g., GDPR requests to delete a user) without rewriting the whole dataset?
The Answer: Historically, Athena was read-only. But now, we use Apache Iceberg tables in Athena.
The Feature: Iceberg is a modern table format supported natively by Athena.
Capabilities: It supports ACID transactions. I can run: `DELETE FROM my_iceberg_table WHERE user_id = '123';`.
How it works: It doesn't physically delete the file immediately; it writes a 'delete file' (tombstone) and handles the merge on read. A background compaction job cleans up the old files later. This brings Data Warehouse capabilities to the Data Lake.

1. You partitioned your table by Date. But now you need to join two massive tables on User_ID. The join is slow and crashes with 'Query Exhausted Resources'. How do you fix this?
    - The Answer: We need to implement Bucketing (Clustering) along with Partitioning.
    - The Problem: Partitioning by Date is good for filtering time, but inside the '2024-01-01' folder, the data is random. To join on User_ID, Athena has to shuffle all that data across the network to find matching IDs.
    - The Solution: We bucket the table by `User_ID` into, say, 50 buckets: `CREATE TABLE ... CLUSTERED BY (user_id) INTO 50 BUCKETS`.
    - The Result: Athena knows that User 123 is always in Bucket 5. It can perform a Bucket-to-Bucket Join (co-located join) without shuffling massive amounts of data, which is drastically faster.

1. What is the `HIVE_PARTITION_SCHEMA_MISMATCH` error? You didn't change the table definition, so why is Athena complaining?
    - The Answer: This happens due to **Schema Evolution** in the underlying S3 files.
    - The Scenario:
        1. Yesterday, your ETL job wrote Parquet files where `user_id` was an `INT`.
        1. Today, the developer changed the code, and now `user_id` is written as a `STRING` in the new Parquet files.
    - The Conflict: The Athena table definition says `INT`, but the new partition files contain `STRING`.
    - The Fix: We must either fix the upstream ETL to be consistent or update the Athena table schema to a compatible type (e.g., String) that can handle both values.

1. We need to hide the SSN column from our Data Analysts, but allow the HR team to see it. Do we have to create two separate copies of the data in S3?
    - The Answer: No, duplication is unnecessary. We use AWS Lake Formation.
    - The Old Way: Creating two views (`analyst_view` without SSN, `hr_view` with SSN) and managing IAM permissions for each. Hard to scale.
    - The Modern Way: We register the S3 path in Lake Formation:
    - We define one single table.
    - In Lake Formation console, we create a permission rule:
        ```
        Principal: AnalystRole
        Action: SELECT
        Column Filter: Exclude column SSN.
        ```
    - The Result: When an analyst runs `SELECT *`, Athena returns all columns except SSN. They don't even know it exists.

1. Your team relies heavily on Athena Views. Suddenly, queries using these views start failing or returning wrong results after the underlying table was updated. Why?
    - The Answer: Athena Views are Stale-Prone.
    - How they work: An Athena view stores the SQL Query string, not a hard link to the columns.
    - The Scenario:
        - View Definition: `SELECT * FROM users`. (At creation time, users had columns A, B).
        - Update: You drop column B from the users table.
        - The Failure: When you query the View, it tries to run SELECT *, expects column B (based on metadata cache or specific expansion), and fails because B is gone.
    - Best Practice: Always explicitly list columns in views (`SELECT A, B FROM...`) to avoid `SELECT *` surprises, and **rebuild views when schema changes**.

1. You need to run a 'Top N' query (e.g., top 10 products by sales) on a massive dataset. It is taking forever. How does Athena execute this, and how can you optimize it?
    - The Answer: A standard `ORDER BY` is expensive because it forces all data to a single worker node to sort it globally.
    - The Optimization: If we only need the approximate top 10 (or if the dataset is huge), we can just let it run. But often, the bottleneck is the final sort.
    - The Trick: If we have massive data, we can optimize by doing a Two-Stage Aggregation manually if the query engine struggles.
    - Insight: Athena (Presto) usually handles `LIMIT` efficiently by pushing it down. However, if using complex window functions `RANK() OVER (ORDER BY...)`, it forces a heavy shuffle.
    - Optimization: Ensure the data is Partitioned or Bucketed **by the grouping key** so the sorting happens in parallel on distributed nodes rather than globally.

1. Athena has a 30-minute timeout. You have a massive transformation query that takes 45 minutes. You cannot use Redshift/Spark. How do you solve this in Athena?
    - The Answer: We must break the query down using CTAS and Incremental steps.
    - The Problem: We can't increase the 30-minute quota.
    - The Solution:
        - Step 1: Create a temporary table aggregating data for the first half of the year.
        - Step 2: Create another for the second half.
        - Step 3: Union them in the final query.
    - Alternative: If the issue is simply volume, use Iceberg and process data incrementally (e.g., process only today's data and MERGE it into the main table) rather than reprocessing history every time.

## Error-Based Questions
1. You successfully ran a `CREATE TABLE` statement pointing to `s3://bucket/data/`. The command succeeded. However, `SELECT *` returns 0 records. You checked S3, and there are definitely 1,000 files in there. What happened?
    - The Answer: This is a Partition Metadata issue.
    - The Cause: If the table is partitioned (e.g., `PARTITIONED BY (year string)`), Athena does not automatically scan the S3 directories to find the partitions (folders). It waits for you to tell it which folders exist.
    - The Fix:
    - Manual: Run `MSCK REPAIR TABLE my_table;` to force Athena to scan S3 and register the partitions.
    - Crawler: Run an AWS Glue Crawler to sync the metadata.

1. A user can run `SELECT 1` successfully. But when they run `SELECT * FROM production_table`, they get Access Denied. You checked their IAM policy, and they have `s3:GetObject` on the Data Bucket. What is missing?
    - The Answer: Athena needs permission for TWO S3 locations.
    - The Trap: Athena executes the query and writes the results (CSV) to a separate 'Query Result Location' (usually aws-athena-query-results-...).
    - The Fix: The user needs `s3:PutObject` and `s3:GetObject` permissions on the Output/Result Bucket, not just read access to the source data bucket.

1. You are running a `GROUP BY` query on a large dataset (10TB). The query runs for 5 minutes and then crashes with Query exhausted resources at this scale factor. What resource ran out?
    - The Answer: This usually means you ran out of Memory on the worker nodes.
    - The Mechanism: Athena (Presto) does joins and aggregations in memory. If you `GROUP BY` a column with high cardinality (e.g., User_ID with 1 billion unique users), the hash table grows too large for the worker's RAM.
    - The Fix:
        - Reduce Scope: Filter data first (`WHERE date = 'today'`) to reduce the volume.
        - Cardinality: Don't `GROUP BY` unique IDs directly.
    - Approximation: Use `approx_distinct(user_id)` instead of `count(distinct user_id)` if exact precision isn't required (uses much less memory).

1. Your query fails with `HIVE_PARTITION_SCHEMA_MISMATCH`. You discovered that for the partition year=2023, the `user_id` column is an `INT`. But for the new partition year=2024, the developer changed user_id to `STRING` (uuid). Athena cannot read both. How do you solve this without deleting data?
    - The Answer: This is Schema Evolution conflict.
    - The Problem: Athena generally expects all partitions to have the same schema (unless using Iceberg).
    - The Fix: You must use a 'Common Denominator' schema.
    - Update the Table Definition to use `STRING` for `user_id` (since `String` can hold both 123 and abc).
    - Crucial Step: Run `MSCK REPAIR TABLE` or manually drop and re-add the old partitions so they re-register with the new STRING definition.
    - Note: If using AWS Glue, enable 'Update behavior: Update the table definition in the Data Catalog' in the Crawler settings.

1. A Data Scientist tries to download a dataset using `SELECT * FROM huge_table`. After 10 minutes, it fails with Response too large to be returned. Why?
    - The Answer: They are hitting the limit of the Athena Console/API output collection.
    - The Limit: Athena isn't designed to stream gigabytes of data directly to the browser or a standard JDBC connection in one go if the output file is massive and un-split.
    - The Fix: Do not use `SELECT *` to download. Use `UNLOAD`:
        ```
        UNLOAD (SELECT * FROM huge_table)
        TO 's3://my-bucket/export/'
        WITH (format = 'PARQUET')
        ```
    - This tells Athena to write the results directly to S3 in parallel (splitting files) rather than trying to assemble a single response file.

1. Your Athena queries are scanning a 50TB table. The query fails with: `HIVE_CURSOR_ERROR: com.amazonaws.services.s3.model.AmazonS3Exception: Slow Down (Service: Amazon S3; Status Code: 503...)`. You are using S3 Standard. Why is S3 throttling a read?
    - The Answer: You have a Prefix Hot spot.
    - The Cause: Athena spins up thousands of workers. If all those workers try to read files from the same S3 folder (Prefix) simultaneously, you exceed S3's limit of 5,500 GETs/sec per prefix.
    - The Fix:
        - Partitioning: Ensure the query filters by partition so it doesn't scan the whole bucket.
        - File Size: If you have 1 million tiny files (KB size), Athena makes 1 million API calls. Compact them into larger files (e.g., 100MB Parquet) to reduce the number of GET requests.

1. You are using Apache Iceberg on Athena to support updates (`UPDATE users SET...`). You have a job that runs updates every minute. Occasionally, the job fails with `CommitFailedException: Optimistic lock failed`. What does this mean?
    - The Answer: This is a Concurrency Conflict.
    - The Mechanism: Iceberg uses Optimistic Concurrency. When Job A tries to update the table, it checks the current snapshot. If Job B updates the table while Job A is running, the snapshot changes. Job A sees the change, realizes its update is based on old data, and fails.
    - The Fix:
        - Retry Strategy: Implement logic to catch the exception and retry the query (it will pick up the new snapshot and likely succeed).
        - Architecture: Don't run concurrent updates on the exact same rows/partitions if possible.

1. You are running a Federated Query to join S3 data with a DynamoDB table using the Athena DynamoDB Connector. The query works for small tables, but for the main Users table (10GB), it fails with a generic Lambda Timeout. You increased the Lambda timeout to 15 minutes, but it still fails.
    - The Answer: The Lambda is running out of Memory, not just time, or struggling to Spill data.
    - The Bottleneck: The Lambda connector fetches data from DynamoDB. If the result set is larger than the Lambda's RAM, it must 'Spill' (write temporary data) to an S3 bucket.
    - The Fix:
        - Increase RAM: Max out the Lambda memory (10GB).
        - Check Spill Bucket: Ensure the spill_bucket environment variable in the Lambda configuration points to a valid S3 bucket and the Lambda has write access to it.
        - Predicate Pushdown: Ensure your SQL query uses `WHERE` clauses that **match DynamoDB Keys/Indexes** so the Lambda only fetches what is needed.

1. You created a View `v_sales` that does `SELECT * FROM sales_table`. Later, a data engineer dropped the column `customer_email` from the underlying `sales_table` to comply with privacy rules. Now, `SELECT * FROM v_sales` fails with `Column 'customer_email' cannot be resolved`. But the column doesn't exist anymore, so why is the View looking for it?
    - The Answer: Athena Views are **Static** Definitions.
    - The Cause: When you run `CREATE VIEW AS SELECT *`, Athena expands that * into the specific list of columns that existed **at that moment** (e.g., id, amount, customer_email) and saves that list in the definition.
    - The Error: Even though the physical table changed, the View definition still explicitly asks for `customer_email`.
    - The Fix: You must manually Update/Recreate the View (`CREATE OR REPLACE VIEW`) so it re-scans the underlying table schema and removes the deleted column from its definition.

1. You are querying logs stored in JSON format. Most queries work, but one specific day fails with: `HIVE_CURSOR_ERROR: Row is not a valid JSON Object - JSONException: Unterminated string`. How do you find the bad row in a 50GB file?
    - The Answer: The default JSON SerDe (Serializer/Deserializer) is very strict.
    - The Cause: A single log line might have been cut off (network issue) or contain a syntax error (e.g., {msg: Hello w... missing the closing quote).
    - The Debug Strategy:
        - Switch Library: Use the `org.apache.hive.hcatalog.data.JsonSerDe` (OpenX SerDe), which allows `ignore.malformed.json = 'true'`. This skips bad rows instead of crashing the query.
        - Binary Search: If you must fix it, try querying specific partition ranges (Hours 0-12 vs 12-24) to narrow down where the crash happens.

1. You have full admin access. You run a query. It succeeds (Status: SUCCEEDED). But when you try to click 'Download Results' or view the data in the console, you get: `KMS.AccessDeniedException: The ciphertext refers to a customer master key that does not exist...`. You checked the Source Bucket key, and you have access. What is wrong?
    - The Answer: You are blocked on the Result Bucket encryption, not the Source.
    - The Architecture: Athena reads from Source -> Processes -> Writes Results to Output Bucket (S3).
    - The Trap: The Output Bucket (aws-athena-query-results...) might be encrypted with a different KMS key (e.g., an Auto-generated key or a specific Infosec key) than the Source Bucket.
    - The Fix: Check the Athena Workgroup settings to see which Key is used for Query Results Encryption, and ensure your IAM User has `kms:Decrypt` permissions for that specific key.

1. You enabled Partition Projection on your 'Logs' table to avoid using Glue Crawlers. You configured the projection to handle dates from 2020 to 2025. You query: `SELECT * FROM logs WHERE date = '2026-01-01'`. Athena returns 0 records instantly. You checked S3, and the folder date=2026-01-01 definitely exists and has data. Why did Athena ignore it?
    - The Answer: Partition Projection **calculates locations in-memory**, it does not look at S3.
    - The Logic: You told Athena 'Valid dates are 2020 to 2025'.
    - The Execution: When you ask for 2026, Athena checks the rule. It sees 2026 is outside the defined range. It concludes 'This partition cannot exist based on the rules,' and skips the S3 lookup entirely.
    - The Fix: You must update the Table Properties to extend the projection range to include 2026.