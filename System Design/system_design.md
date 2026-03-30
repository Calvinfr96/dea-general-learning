# System Design

## System Design Introduction and Principles
- In data engineering, system design involves planning and architecting the infrastructure and services required for effective data collection, storage, processing, and analysis. This includes considerations for data pipelines, databases, data lakes, data warehouses, ETL processes, and analytics platforms.
- Good system design is crucial in data engineering because it ensures that data flows smoothly and efficiently from source to insight, regardless of the volume, velocity, or variety of data. Well-designed systems can handle spikes in data, scale as data grows, and provide reliable and timely insights, which are crucial for making informed business decisions.

### CAP Theorem
- CAP stands for Consistency, Availability, and Partitions. A distributed system generally produces two out of three of these properties simultaneously and characterizes the compromise between consistency and availability when a partition exists. This theorem is also known as Brewer’s theorem since it was first conveyed by Eric Brewer, a computer science professor from U.C. Berkley.
- Data engineers often work with distributed data systems, such as distributed databases, data lakes, and big processing frameworks. The CAP theorem informs the design choices and trade-offs that need to be made when building these systems.
- **Consistency:**
  - Consistency ensures all copies of data across a distributed system are the same. This is crucial for applications where data accuracy is important, such as financial transactions or inventory management. A system that is consistent ensures that a read operation returns the most recent write operation across all nodes. This can be very challenging in a distributed environment where data is replicated across many locations.
  - For example, Goldman Sachs ensures all transactions across its global trading platform are consistent, meaning every read operation returns the most recent transaction record.
- **Availability:**
  - Availability ensures systems are always operational and can handle parallel read and/or write operations at the same time. This is particularly important for customer-facing applications or services that require constant data access, such as real-time data processing. High availability ensures that system failures do not disrupt the service, but it can be challenging to maintain in conjunction with strong consistency guarantees.
  - For example, Netflix prioritizes high availability to ensure that its customers can access movies and TV shows anytime without interruption, even during peak traffic or server maintenance events.
- **Partition Tolerance:**
  - A network partition occurs when parts of a distributed system lose connectivity with one another due to network errors. Data engineering systems must be designed to handle these partitions gracefully, ensuring all systems can still operate when a subset of nodes is not available.
  - Network partitions don't correlate to database partitions. Network partitioning simply refers to the practice of making the same service available in multiple network locations. For example, if a system relies on AWS and there is a system outage in the us-east-1 region, that system should be able to fallback on the us-west-2 or another nearby AWS region in the US.
  - For example, Google's Search Engine is designed to handle network partitions gracefully, ensuring that search queries can still be processed and return relevant results, even if some of its data centers are temporarily disconnected due to network issues.

### CAP Theorem Architecture
- Amazon S3 (AP) - Designed to offer high availability and durability of data across multiple facilities. It's built to be partition-tolerant, ensuring that data is accessible even in the event of network or hardware failures. While S3 provides eventual consistency for overwrite PUTS and DELETES in all regions, it offers read-after-write consistency for PUTS of new objects in all regions, striking a balance that primarily aligns with AP characteristics.
- AWS Lambda (A) - AWS Lambda's serverless architecture ensures that functions are available to execute as needed. While consistency and partition tolerance are not directly applicable attributes (since Lambda is a compute service rather than a data store), its design supports high availability of processing capabilities.
- AWS Glue (AP) - Focuses on processing data across distributed systems. It's designed to manage data workflows that are resilient to failures (partition tolerance) and ensures that ETL jobs can run with high availability. The consistency aspect in Glue is managed at the level of individual ETL jobs, which can be designed to ensure data consistency within the bounds of the specific ETL logic implemented.
- Amazon Redshift (CP) - Provides strong consistency within its distributed architecture for query processing and storage. Being a data warehouse, consistency of data for analytics and reporting is a key requirement. Redshift is designed to handle partition tolerance internally through its distributed architecture, ensuring data is consistently accessible across nodes. While Redshift aims for high availability, the focus on providing consistent, accurate query results can place it more in the CP category for the purposes of this analysis.

### CAP Theorem Applications in Data Engineering
- Database Selection:
  - Data engineers must choose the right type of database based on the application's requirements. A relational database might offer strong consistency (CP), but might struggle with partition tolerance, making it less suitable for global applications that require high availability across distributed regions. Conversely, NoSQL databases often favor AP, offering availability and partition tolerance with eventual consistency, making them ideal for distributed applications where slight delays in data consistency are acceptable.
  - An example of using a relational database would be Airbnb, which uses databases such as PostgreSQL for transactional data where strong consistency is crucial, such as booking information. Ensuring that data is consistent across all nodes helps maintain integrity in user transactions.
  - An example of using a NoSQL database would be Twitter, which utilizes databases such as Cassandra for its timeline feature, prioritizing availability and partition tolerance to handle the massive, distributed nature of tweet data. This approach allows for slight delays in data consistency, which is acceptable in the context of displaying tweets.
- Data Pipeline Design:
  - The CAP theorem influences how data pipelines are designed, especially when these pipelines process and move data across different systems and locations. Data engineers need to consider how pipeline architecture supports consistency, availability, and partition tolerance. For example, in an event streaming architecture, ensuring partition tolerance and availability might take precedence to ensure real-time data processing and analysis scenarios where slight delays in consistency are acceptable.
  - For example, Uber utilizes event-driven architectures and data pipelines to process real-time location data and match riders with nearby drivers. Systems like Apache Kafka, which favor partition tolerance and high availability, ensure that ride requests are processed efficiently, even in the face of network partitions or server failures.
- Big Data Processing:
  - Systems like Hadoop and Spark are designed to process large datasets across distributed computing environments. The CAP theorem considerations impact how these frameworks manage data distribution, fault tolerance, and processing consistency to balance between performance and data accuracy.
  - For example, Yahoo uses Hadoop to process and analyze vast amounts of web data. The Hadoop Distributed File System (HDFS) and its ecosystem are designed to handle data distribution and fault tolerance, accommodating the CAP theorem's considerations to ensure data processing continues even when some clusters experience failures.
  - Netflix uses Apache Spark for real-time analytics and batch processing jobs across its distributed computing environment. Spark's resilient distributed datasets (RDDs) and data frames are key in managing data distribution, fault tolerance, and processing consistency, allowing Netflix to analyze huge datasets for recommendations, content popularity, and viewing patterns, ensuring a balance between performance and data accuracy.
- In data engineering, the CAP theorem serves as a guiding principle for designing and operating distributed data systems. By understanding and navigating the trade-offs between consistency, availability, and partition tolerance, data engineers can build scalable, resilient, and efficient systems capable of supporting complex data processing and analytics needs. This ensures that data-driven applications can deliver meaningful insights and maintain high performance, even as data volumes and system complexity grow.

### Real World Example
- Consider a company whose architecture uses Talend for data consumption, Amazon S3, and Amazon Redshift for data transformation and warehousing. This architecture suffers from the following problems: excessive resource consumption, absence of data lineage, lack of change data capture, and serialization isolation limitations. These challenges necessitate a strategic solution to move computation away from Redshift, establish data lineage, enable efficient change data capture (SCD 1/2), and overcome the limitations of serialization isolation.
- Data lineage is the process of tracking, recording, and visualizing the entire lifecycle of data—from its origin and transformation to its final destination and usage.
- Serializable isolation is the highest, strictest SQL transaction isolation level, ensuring that concurrent transactions produce the same results as if they were executed sequentially (one after another). It guarantees maximum data consistency, eliminating all concurrency phenomena like dirty reads and non-repeatable reads.
- Using databricks on top of AWS helps to solve the data lineage, change data capture, and serialization isolation issues. The only problem that couldn't be solved is the high resource utilization. In a majority of real-world system design problems, you won't be able to satisfy or solve every single one of a client's issues or requirements. This requires discussing and compromising with the client to figure out which requirements are the highest priority and solving those, while partially mitigating or ignoring lower-priority requirements.

## Relevant Data Engineering Concepts
- Modularity:
  - Modularity involves building data pipelines and components that can be developed, tested, and deployed independently. This approach facilitates easier updates, scalability, and reusability of code and can lead to more resilient data systems that are easier to maintain and scale.
- Encapsulation:
  - Encapsulation involves designing data models that hide the complexities of data transformations and storage details from the end-user. This can simplify data access and manipulation, making it easier for analysts and other stakeholders to utilize data without needing to understand the intricacies of underlying data storage or schema.
- Abstraction:
  - Abstraction involves  providing simplified views of complex data processes, such as abstracting the details of a multi-stage ETL process into a single, high-level operation. This helps manage complexity, especially when dealing with large-scale data infrastructures, and allows data engineers to focus on higher-level system design and optimization.
- Scalability:
  - Scalability is a critical attribute of modern data systems, reflecting their ability to adapt and efficiently handle increasing volumes or complexity of work. It's particularly crucial in data engineering, where systems must accommodate the exponential growth of data while maintaining performance and reliability.
  - Scalability involves designing systems that can efficiently handle increases in data volume. This includes choosing the right storage solutions (e.g., SQL vs. NoSQL databases, data lakes), implementing scalable processing frameworks (e.g., Apache Spark, Apache Flink), and considering both horizontal and vertical scaling strategies based on the data workload characteristics.
- Horizontal Scaling (In/Out):
  - Horizontal scaling involves adding more nodes to a cluster or more instances to a service. In data engineering, this could mean adding more data nodes to a Hadoop cluster or more instances to handle web requests in a load-balanced application. This approach improves fault tolerance through redundancy, ensuring one node doesn't bring down the system.
  - The key to effective horizontal scaling in data systems is efficient data distribution and network partitioning across nodes. 
  - While the initial cost might be lower due to the use of commodity hardware, operational costs and complexity increase with the cluster's size. Automating deployment, monitoring, and management becomes essential.
- Vertical Scaling (Up/Down):
  - Vertical scaling involves upgrading the existing hardware. This could mean adding more CPUs, RAM, or faster storage to a database server. It's often the first step taken to address performance issues due to its simplicity. There are physical and practical limits to how much a single server or instance can be scaled up. Beyond certain points, the cost-to-benefit ratio declines, and the risks associated with single points of failure become significant.
  - Vertical scaling is often used for databases or applications with a single-instance architecture that are not easily distributed across multiple nodes.
- Database Partitioning:
  - Partitioning is a database management technique used to divide a large dataset into smaller, more manageable pieces, called partitions. This approach improves performance, simplifies maintenance, and enhances the manageability of large datasets. Partitioning can be applied to tables, indexes, or databases, depending on the system and the specific needs of the application.
  - Partitioning involves splitting a table into multiple segments that can be stored separately but still be accessed as part of the same logical table. Each partition can be stored on different physical locations (like disks or nodes in a cluster), which allows database systems to manage and access subsets of data more efficiently.

### AWS Data Pipeline Example
- Scenario: A company wants to process user activity logs to generate insights into user behavior on their platform.
- Data Ingestion Module: Amazon S3 + AWS Lambda:
  - Amazon S3 is used as a highly durable storage service to collect and store raw user activity logs. Each log file is uploaded to a specific S3 bucket designated for raw data.
  - AWS Lambda functions are triggered automatically upon new log file uploads to the S3 bucket. Each Lambda function performs preliminary data validation and transformation tasks on the raw logs. Because Lambda functions are independent and can scale automatically, they represent a modular approach where the data ingestion logic can be developed, deployed, and scaled independently from other parts of the pipeline.
- Data Processing Module: AWS Glue:
  - AWS Glue is a managed ETL service that prepares and transforms the validated data for analysis. Glue jobs can be created to process the data stored in S3, performing more complex transformations and preparing the data for analytics.
  - AWS Glue scripts are modular and can be developed and tested independently, allowing data engineers to update the transformation logic without impacting the ingestion or storage components.
- Data Analysis and Storage Module: Amazon Redshift + AWS Lambda:
  - After processing, the transformed data is loaded into Amazon Redshift, a fully managed, petabyte-scale data warehouse service. Redshift serves as the analytical module where complex queries and analyses are performed.
  - Additional AWS Lambda functions can be used to automate the loading of processed data into Redshift. These functions can be triggered by Glue job completion events, ensuring that the data loading component remains decoupled and independently scalable.

### Snowflake Horizontal Scaling Example
- Scenario: A global e-commerce company uses Snowflake to analyze customer data across different regions. They need to handle peak periods of data ingestion and query load during sales events such as Black Friday and holiday seasons.
- Implementation:
  - Multi-Cluster Warehouses - Snowflake supports multi-cluster virtual warehouses which enable horizontal scaling. The e-commerce company configures a multi-cluster warehouse that automatically starts additional clusters when concurrent user loads or complex queries exceed the capacity of the existing clusters.
  - Data Sharing - Although Snowflake automatically manages data distribution across all nodes of a virtual warehouse, it ensures even distribution to optimize query performance and avoid hot spots, which is crucial during high-demand periods.
  - Concurrency Scaling - Snowflake's architecture supports automatic scaling to manage increases in query load without manual intervention, ensuring that performance remains consistent as user and query loads increase.
- Benefits
  - Automatic Elasticity - Snowflake automatically adds compute resources in real-time as needed, which is ideal for handling highly variable data loads.
  - Performance and Isolation - Multi-cluster warehouses not only handle increased loads but also isolate and limit the performance impact of large, complex queries on regular, smaller queries.
  - Cost Efficiency - Users are charged for additional compute resources only when they are actively used, optimizing cost vs performance.

### Snowflake Vertical Scaling Example
- Scenario: A financial analytics firm uses Snowflake for daily risk assessment computations which require high computational power for a limited period each day.
- Implementation:
  - Warehouse Sizing - The firm uses a Snowflake virtual warehouse and scales up the warehouse during the computation window. They switch from a smaller size (e.g., X-Small) to a larger size (e.g., Large or X-Large) to provide additional compute resources.
  - Resource Monitors - To manage cost and avoid unnecessary spend, the firm sets up resource monitors in Snowflake to track and control the compute usage.
  - Scheduled Scaling - Utilizing Snowflake's ability to programmatically scale through SQL statements or through the UI, the firm schedules these scale-up operations to coincide precisely with their daily batch processing window.
- Benefits:
  - Rapid Elasticity - Vertical scaling in Snowflake is almost instantaneous, allowing the firm to rapidly adjust compute resources.
  - Precision Cost Management - By scaling up only during the necessary time frame and scaling down immediately afterward, the firm manages its cloud spend efficiently.
  - High Performance - By scaling up only during the necessary time frame and scaling down immediately afterward, the firm manages its cloud spend efficiently.