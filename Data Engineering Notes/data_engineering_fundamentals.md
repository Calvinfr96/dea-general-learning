# Data Engineering Fundamentals

## What is Data Engineering?
- Data engineering is focused on the practical application of data storage, collection, management, and analysis. It involves the design, construction, and maintenance of systems and processes that allow for efficient handling and transformation of data.
  - This includes building **scalable** and reliable data pipelines which transport data from various sources to storage systems and data warehouses, where it can be accessed and used for analysis, and turned into insights.
  - It's especially important for data pipelines to be scalable, since they need to be able handle processing increasing amounts of data quickly, especially with the rapid rise of AI.
- Data can either be structured, semi-structured, or unstructured. Structured data comes in the form of CSV or tabular formats. Semi-structured data comes in the form of XML and JSON. Unstructured data comes in the form of video, images, text, etc.
- Data engineers will start by building a data pipeline to collect data from various sources. Next, they will clean up the data and convert it to a form where it is ready for analysis. The data warehouse is typically the final destination of the data once it has gone through these steps.
- Data engineers work very closely with data scientists to help build the foundation necessary for the data scientist to do their job. This includes:
  - building datasets
  - cleaning up data
  - monitoring data quality
  - building real-time processes
  - scaling to ensure the product can handle large amounts of data.
  - SQL and Python

## Stages of Data Engineering
- The first part of the data engineering flow is gathering business requirements from business personnel or data scientists. Here, engineers ask what kind of data is required and how they plan on using the data. The data engineering project is then planned out based on these requirements.
  - This planning can include how often to collect (batch) data and where to store it.
- The second part of the flow is data discovery and gathering. Here, we look at what kind of data is available and where it should be moved. Within this step, an architecture design is carried out by senior data engineers and solution architects using ETL logic. This design process includes system design, data modeling, etc.
- The third part of the flow involves building the pipeline that will extract the data from its source, such as a database and ingest into the data warehouse.
- The fourth part of the flow involves data transformation, where we filter out data from the database that does not meet the stated requirements.
- The fifth part of the flow involves cleansing and validating the data.
- The sixth part of the flow involves data modeling, where we decide how we want to store the data. Deciding how the data should be stored involves relating dimension and fact tables. In the example of vending machine data, a dimension would be the name of a product being sold, along with the product details and characteristics. A fact would be the quantity of products sold on a daily basis.
- The last part of the flow involves data quality assurance.

## Role of Data Engineer in Data Science and Analytics
- Example of how data engineering relates to data science:
  - There is a retail company that owns 1000s of vending machines spread across various locations. There 10 - 100 items in each vending machine. One of the business requirements for this company is to perform demand forecasting for each item sold in the machines.
  - Demand forecasting involves looking at historical demand data to determine future demand for each product.
  - The vending machine sends data to a transactional database, such as Oracle, each time a product is sold. Once the data is stored in Oracle, it cannot be used for analytics and insights yet. This is because the data stored in the database applies generally to the transactions performed at the vending machine. Not all of the data is applicable to demand forecasting.
  - The data science team uses databricks to perform their analyses. The data engineer comes into the picture here, as they are the ones who are responsible for transporting the required data from the transactional database to databricks.
  - First, the data engineer will extract all of the data from the transactional database. Next, they will transform the transactional data into sales data that can be used for demand forecasting. Finally, they will load the data into databricks. This overall process is call Extract Transform Load (ETL).

## Essential Skills for Success in Senior Data Engineering Roles
- When you hold a senior role in data engineering, your job requires a lot more than just technical expertise. It also requires leadership, innovation, and strategic thinking. Several other skills needed for senior roles include:
  - Strategic Thinking: Aligning technical solutions with business goals to create measurable value.
  - Team Leadership: Managing teams effectively to meet required goals through innovation and collaboration.
  - Stakeholder Management: Presenting technical concepts to non-technical audiences.
  - Delivery Excellence: Ensuring projects are delivered on time and within budget.
  - Technical Expertise: Mastery of modern cloud platforms.
  - Risk Management: Managing risks proactively to avoid project disruptions.
  - Innovation: Developing reuseable accelerators and staying ahead of industry trends.
  - Consumer-Centric Approach: Delivering solutions that exceed client expectations.
  - Project Estimation: Accurately planning timelines and budgets.
  - Continuous Learning: Keeping yourself and your team up to date with emerging tools.

## Relational Database Management Systems (RDBMS) Overview
- An RDBMS is a set of software systems designed to handle, store, manage, and retrieve data efficiently. This system helps link multiple data points using primary and foreign keys or relationships.
- The data stored in these systems are stored in a tabular format, with rows and columns. Data integrity is ensured through the use of unique primary keys.
- RDBMS plays an essential role in how ETL pipelines are structured. RDBMS also allows data engineers and analysts to query data quickly and efficiently.

## Overview of Data Warehouses and Data Lakes
- A Data Warehouse is a centralized repository designed to store integrated data from multiple sources. The data in data warehouse is already structured, filtered, and processed to meet specific business requirements. Data warehouses are primarily used by data analysts and data scientists for reporting and analysis.
  - A data warehouse is organized into tables with defined schemas.
  - A data warehouse can either be used for batch processing or real-time processing.
  - In the ETL flow, a data warehouse is where the data is stored after extraction, loading, and transformation are completed.
  - Example: a business intelligence team wants to understand the sales of a particular SKU from the vending machine. This might require SKU-related data in addition to sales-related data.
- A Data Lake is a vast pool of raw data in its native form until it is needed for analysis and reporting.
  - The data stored in a data lake can be unstructured or semi-structured.
  - In the ETL flow, the data lake is where the data is stored after it is extracted and loaded.

## Data Modeling Overview
- Out of the five interview rounds you take in a DE interview, you need to pass at least 3.5/5 to get the job. For a typical company, the five rounds consist of SQL, Python, Behavioral Questions, Data Modeling, and System Design/AWS. Out of these five, the easiest to pass are SQL, Behavioral, and Data Modeling. Data Modeling is the least technical of these three subjects.
- Data Modeling is the process of defining and analyzing data requirements set by businesses and stakeholders in order to give them what they need to solve business problems.
  - The primary concern is defining what data and tables are needed to solve business problems.
  - A secondary concern is designing the tables in a manner that allows the data to be linked efficiently.

### Data Modeling Types
- The three main types of data modeling are Conceptual, Logical, and Physical. The two types most often tested in US interviews are conceptual and logical.
- Conceptual data modeling is the most abstract level and involves listing out the tables you think you'll need to solve the various requirements set by business leaders.
- Logical data modeling is one level lower and involves creating the schemas for these tables.
- Physical (Technical) data modeling is the lowest level and involves the technical aspects of creating the tables and inserting them into a database. This type of data modeling is often tested in the system design interview round, not the data modeling round.

### Data Modeling Facts
- The two main types of tables that data engineers work with are dimension tables and fact tables. Dimension tables typically store characteristics and details, while fact tables typically store measurements of entities stored in the dimension tables.
  - Fact tables are a lot more dynamic than dimension tables.
- Measurements can include measurements such as daily sales, daily activity, etc. Measurements can either be aggregated or non-aggregated; the level to which data is aggregated (daily, weekly, monthly, etc.) is called granularity.

### Data Modeling - SCD
-  Dimension (dim) tables are commonly used to store entities along with their characteristics and details.
  - For example, consider DoorDash. The primary entities for this company include riders, drivers, and restaurants.
- The main reason dimensions and facts are stored in separate tables is to save space. By separating them, you don't have to store an entity's details alongside each fact related to that entity.
- There are three types of Slowly Changing Dimension (SCD) dim tables:
  - Type 1 is the most common allows updating a row to update characteristics and get the most up to date information.
  - Type 2 inserts a new row to update characteristics, instead of updating an existing row. This type of table is ideal when historical data is crucial to business operations.
  - Type 3 inserts a new column to update characteristics, instead of inserting a new row. This type of table should be avoided as it can result in a lot null data, which can complicate data handling logic.
- There are also three types of fact tables:
  - Transaction: Records user transactions, such as purchases on an e-commerce website.
  - Periodic Snapshot: Contains data aggregated over a certain time period, such as daily, weekly, or monthly.
  - Accumulating Snapshot: Contains rows that are updated with new columns that represent a period of time. For example, for a row that is meant to represent a week worth of data, each column could represent a day's worth of aggregated data.

### Data Modeling - OLTP vs. OLAP
- The two main types of fact tables/databases used in data engineering are Online Transactional Processing (OLTP) and Online Analytical Processing (OLAP) databases. In an OLTP table, one row represents one transaction.
- OLAP tables typically store aggregated data related to the OLTP tables. OLAP databases are typically much more efficient at performing aggregations on columns of non-aggregated data than an OLTP database. Similarly, OLTP databases are much more efficient at pulling singular rows of data than OLAP databases.
- Postgres is a commonly-used type of OLTP database while Redshift is a commonly-used type of OLAP database.

### Data Modeling Techniques
- One of the most important techniques in data modeling is relational modeling, where you determine how all of your tables relate to one another, so that they all have a defined purpose.
- Relational modeling typically involves using the star schema to relate tables, where you have several dim tables "surrounding" one or more related fact tables.
- Normalization is the process of organizing and modeling data to reduce redundancy, save storage space, and eliminate undesirable characteristics, such as insertion, update, and delete anomalies. An example of data normalization is using a foreign key to represent a related entity in a table, instead of including all of that entity's characteristics in the table.
- Denormalization is the opposite of normalization, where you intentionally include redundant data in a table. Denormalized data is typically used in machine learning applications. It also might be used in situations where you need to deal with real-time data or very large amounts of data, since it can help prevent needing to repetitively join tables.

### Data Modeling - Real-World Example
- Data Modeling > Data Modeling Practice Questions > Supply Demand Dynamics (Uber):
  - What does supply/demand look like per city where rider and driver are not on trip? The data has to update every 10 minutes and give 24 hour view.
- What NOT to do when answering a question like this during an interview:
  - Recommend data science models.
  - Recommend system design approaches.
- Since this will be asked during a **data engineering** interview, the only thing you need to be concerned with is creating the tables, the rows/columns within those tables, and the connections between the tables.
- Step 0: Ask The Interview Questions
  - The interviewer will give you a vague question on purpose. The first step is not to start thinking of ways to solve the problem. The first step is actually to ask clarifying questions.
  - How do we define supply?
  - How do we define demand?
  - What do you mean by 'not on a trip'?
  - Is the driver active? How do we define active?
  - Why is data updated every 10 minutes? Why do we need a 24 hour view?
  - In order to properly develop this skill, you need utilize the product(s) and understand the business model for the company you're interviewing for.
- Step 1: Define The Goal
    - What problem are we trying to solve?
- Step 2: Define The Metric
  - Once we know the problem, we can generate metrics to determine when we've succeeded in solving it.
- Step 3: Create the tables
- Step 4: Double-Check Your Work / Tie Solution Back to Question
- Time Management (60 Minute Interview):
  - 10 -15 minutes asking clarifying questions.
  - 5 minutes defining the goals and metrics.
  - 15 minutes creating the tables.
  - 5 minutes double-checking your work.
  - 5 minutes iterating/improving on your solution
  - 5 minutes asking questions about the position/company.

## What is a Data Warehouse?
- A data warehouse is used to store data after it has been extracted from its origin, transformed, and loaded. It is **not** used to store raw data.
- A data warehouse is not the same thing as a database. A database is a platform used to store data. The data warehouse is the component that's built on top of this platform.
- Data isn't typically created in a data warehouse. Data is moved from a source, such as OLTP database, to a data warehouse after some intermediate processing.
- Rules for Building a Data Warehouse:
  - Should be subjective.
  - Should be organized into subject-based categories.
  - Should contain current and historical data.
  - Should be non-volatile (Data shouldn't change).
  - Should be used for data-driven decision making and problem solving.

### Why Data Warehouse?
- The main reason companies build data warehouses is to streamline business operations.
  - Data warehouses help streamline operations by combining data from multiple sources into one repository that can be used for analytical purposes.

## What is ETL?
- ETL stands for Extract, Transform, Load, which are the three main phases by which data is moved from a data source, such as an OLTP database, to a data warehouse.
  - Extraction Phase: Raw data is read and collected from various sources, including databases, files SaaS applications, etc.
  - Transform Phase: Extracted data is cleaned and standardized in a staging area. In this stage, raw data goes through transformations such as aggregation. It can also include converting data from JSON or XML into a tabular format.
  - Load Phase: Standardized data is encrypted and loaded into loaded into a large data store, such as data lake or data warehouse.
- ETL offers several business advantages beyond the basics of extracting, cleaning, standardizing, and delivering data from source to destination. For example:
  - ETL helps businesses obtain deep historical context with data.
  - It provides a consolidated view of data, which allows for easier analysis and reporting.
  - It improves productivity with repeatable processes that don't require a lot of manual coding.
  - It improves data accuracy and audit capabilities that a lot of businesses require for compliance with regulations and standards.
- Several ETL tools available on the market today include: Informatica Powercenter, Microsoft SQL Server, Microsoft Azure Data Factory, AWS Glue, AWS Data Pipeline, Google Cloud Data Flow.

### Extract Phase
- Extraction is the initial phase of the ETL process, which involves pulling raw data from a variety of sources and storing it in a staging area, rather than directly into a data warehouse or data lake. This ensures data can be easily reverted to its initial state if any issues arise during this phase.
- There are three types of extraction that can be performed in ETL:
  - Full Extraction: Certain systems are incapable of determining when data has been modified. In this case, the only way to pull data from a source is to perform a full extraction. This requires having a backup of the previous extraction _in the same format_ on hand to identify changes that have occurred.
  - Partial Extraction (with update notification): Not all systems can deliver a notification when data has been modified, but they can identify records that have been modified and provide extraction of those records only. This typically requires some kind of timestamp to be attached to the records in the data source.
  - Partial Extraction (without update notification): If the source system is capable of providing update alerts when data is modified, this is the simplest way data can be extracted.

### Transform Phase
- Transformation is the second phase of the ETL process is crucial for data integration. After extraction from various sources, data is placed in a staging area. Once in the staging area, the data undergoes a series of predefined rules or functions to convert it to a single, unified format.
- This transformation process is essential to ensuring compatibility and consistency across different data sets. Some common tasks performed during transformation include: cleaning, joining, filtering, auditing, compliance, and formatting.
  - Cleaning data involves identifying and correcting inconsistencies, errors and inaccuracies within the data. This process typically involves data validation, filling null or missing values, standardizing different formats of specific data, deduplication, and removing anomalies.
  - Joining data involves linking data from multiple sources.
  - Filtering data involves selecting specific rows or columns needed to meet business requirements.
  - Aggregation involves aggregating data from multiple sources.
  - Derivation involves applying business rules to data so it can be used to calculate new values from existing data. 

### Load Phase
 - Loading is the final phase of the ETL process, where the transformed data is loaded into a data warehouse. There are several types of loading that can occur during this phase:
  - Initial loading is filling all of the tables in the data warehouse.
  - Full refresh is clearing the contents of one or more tables and reloading those tables with fresh data.
  - Incremental loading is implementing ongoing modifications as needed on a regular basis. This is typically associated with batch processing jobs, where new data is added to the warehouse on a regular basis.

### ETL vs. ELT
- ELT stands for Extract, Load, Transform and is a similar process compared to ETL.
- As with ETL, extraction is the first phase of ELT, where raw data is extracted from various sources.
- Unlike ETL, the second phase of ELT is the load phase, where data is loaded without being cleansed or standardized.
- The final phase of ELT is the transformation phase, where data is cleansed and standardized _in the data store_, rather than in a separate staging area. There are several layers of transformation that occur here. Layer one contains the raw data. Layer two transforms the data according to business requirements. Layer three creates a view on top of the second layer that will be used for analysis by downstream teams.
- Comparing ETL and ELT:
  - Flexibility:
    - ETL requires more upfront planning to ensure all relevant data is being integrated.
    - ELT is more flexible when it comes to regularly adding extracted data.
  - End Users:
    - ETL is used by SQL coders and users who read reports.
    - ELT is used by data scientists and for advanced analytical purposes.
  - Skills:
    - ETL requires additional training and skills needed to effectively use the toolset that performs the extraction, transformation, and loading.
    - ELT relies mostly on database management system functionality, so existing skills can be used in most cases.
  - Maturity:
    - ETL is a mature practice that has existed since the 1990's. There are many skilled technicians, established best practices, and useful ETL tools on the market.
    - ELT is a relatively new practice, where there is less expertise and best practices available to rely on. Companies are trending more towards using ELT for because of this.
  - Use Cases:
    - ETL is best used with relational and structured data. Better for small to medium amounts of data.
    - ELT is best used with unstructured and nonrelational data. It is ideally used when working with data lakes. ELT can also be used with homogenous relational data and is well-suited for working with very large amounts of data.

## Types of Data
- Data is a collection of distinct, small units of information that can be used in a variety of forms, such as text, numbers, media, bytes, etc. Data can be stored on pieces of paper or in electronic memory.
- In computing, data is information that can be translated into a form that is efficient for moving and processing.
- The three main types of data include structured, semi-structured, and unstructured:
  - Structured data is stored in a standardized format, such as rows and columns, that can be more easily understood than its original, raw format. Examples include SQL databases and Excel files.
  - Semi-structured data is that which uses tags or markers to define elements, fields, and records within itself. Examples include XML and JSON.
  - Unstructured data is not organized as well and does not work within a defined data model. Examples include No-SQL databases, audio files, video files, PDF documents, and images. Specific programs/scripts must be written to derive information from unstructured data.

## Types of Databases
- A database is an organized collection of data stored in a computer system and typically managed using a Database Management System (DBMS). The most commonly used types of databases are relational databases and nonrelational (No-SQL) databases.
  - The data in relational databases is modeled using tables, allowing for efficient processing and querying. Examples of relational databases include MySQL, SQL Server, PostgreSQL, and Oracle.
  - The data in a nonrelational database is modeled using key-value pairs. Examples of nonrelational databases include MongoDB, AWS DynamoDB, and Cassandra.
- Databases have limited storage capacity compared to data warehouses.

## Data Warehouse
- A data warehouse is a relational database that can compile and store multiple structured datasets in one place. This is typically where you perform your data modelling.
- Data warehousing supports business decision-making by allowing for analysis of various data sources and reporting them in an informational format. Unlike a primary database, a data warehouse can handle exabytes of data and usually starts at one terabyte capacity.
- Data warehouses provide several key benefits to businesses:
  - Flexible and Powerful Data Delivery Capabilities:
    - Easily integrates with OLAP and end-user access tools.
  - Integrated View of Data:
    - Easily integrates with external data systems to provide enhanced informational value.
  - Improved Data Quality and Consistency:
    - Enables reconciliation of data between multiple sources.
    - Enables verification and correction of erroneous data.
    - Enables the use of standardized naming schemas across multiple systems.
  - Decoupling From Transactional Systems:
    - Reduces the impact of source system changes.
    - Reduces load on source systems.
  - Allows for historical reporting capabilities.
- Examples of data warehouses used today include: Snowflake, Amazon Redshift, Google Big Query, Microsoft Azure Synapse Analytics, Teradata, and Oracle Autonomous Data Warehouse Cloud.
  - Of these technologies, AWS, Google, and Microsoft can only be used within there specific cloud platform. However, technologies like Snowflake, DataBricks, and Teradata are cloud agnostic and can be used on any of these platforms.
  - Snowflake is easier to use for people who have good knowledge of legacy systems and mainly requires a good foundation in SQL.
  - Databricks is more complicated and requires knowledge of PySpark.
- Some drawbacks of data warehouses include:
  - High initial setup costs.
  - Involves complex implementation.
  - Has a rigid schema that is difficult to change. This is why effective data modeling is very important.

## Data Mart
- A data mart is a database that holds a limited amount of structured data for a single purpose in a single line of business. For example, a data mart can be a database of organized data, used by a sales and marketing team, that does not exceed 100GB.
- Data from a data mart typically comes from a data warehouse, which is why they are widely considered a subset of data warehousing. Data marts help to split the data stored in a data warehouse into multiple controlled segments, which can each have their own schema. This helps better control access and increase security.

## Data Lake
- A data lake is a data storage strategy whereby a centralized repository holds all of an organization's structured and unstructured data. It employs a flat architecture that allows you to store raw data at scale without the need to perform data modeling.
  - The ability to store unstructured data alongside structured data makes performing various types of data analytics easier. It also makes it more flexible than a data warehouse since data can be structured dynamically according to business needs.
- Some of the top data lake solutions on the market include: Snowflake, Microsoft Azure Data Lake, Data Bricks, Google Big Query, and AWS S3.
- Data lakes are important for business operations because they are a centralized repository that allow storage, processing, and analysis of large amounts of data from various sources. This includes unstructured, semi-structured, and structured data. Advantages of data lakes include:
  - Centralized Data Storage:
    - Data lakes consolidate data from multiple sources into one repository, which eliminates the need for data silos and ensures all data is accessible in one place.
  - Scalability:
    - Data lakes are built using scalable, cloud-based platforms that can adjust to a business's increasing data needs. This allows organizations to handle large amounts of data efficiently.
  - Cost Effectiveness:
    - Unlike traditional data warehouses, which require significant upfront investment and maintenance costs, data lakes use cost-efficient storage systems that support pay-as-you-go models, especially when hosted in the cloud.
  - Flexibility:
    - Data lakes can store data in its raw format, meaning businesses can capture all data types without the need for predefined schemas. This flexibility supports diverse analytics use cases.
  - Advanced Analytics:
    - Data lakes enable advanced analytics, including:
      - Training of machine learning and AI models, using raw data to provide predictive insights.
      - Big data processing using tools such as Apache Spark or Hadoop for large-scale processing.
      - Real-time analytics to provide insights from streaming data.
- Several real-world examples of businesses using data lake platforms to optimize their growth include:
  - Streaming Media: Subscription-based streaming companies collect and process insights on customer behavior, which they can use to improve recommendations.
  - Finance: Investment firms use the most recent market data, which is collected and stored in real time, to conduct effective portfolio management.
  - Healthcare: Healthcare organizations rely on big data to improve quality of care. Hospitals use large amounts of historical data to streamline patient pathways, resulting in better outcomes and reduced costs.
  - Sales: Data scientists and sales engineers often build predictive models to help determine customer behavior and reduce churn.
- Data lake architecture refers to the design framework for building and maintaining a data lake, ensuring it can store, process, and analyze large amounts of structured, semi-structured, and unstructured data.
- A robust data lake architecture typically includes the following components:
  - Data Sources: Incudes structured, semi-structured, and unstructured data.
  - Data Ingestion: Batch data processing, where real-time data such as streaming data is regularly collated and sent to a storage facility. You can also stream real-time data to a data lake continuously, instead of in batches.
  - Data Storage and Processing: Raw data is stored in a data lake and ELT tools are used to transform the data into a structured format.
  - Data Consumption: Where analytics and reporting based on structured data occurs.
- Comparisons to a Data Warehouse:
  - Both store large amounts of data for analytics and business intelligence.
  - Both store current and historical data.
  - Data warehouses can only store structured data.
  - Data lakes store data using a flat architecture instead of a structured database environment.
  - Data warehousing focuses on transforming raw data into information that can be used for business decision making. Warehouse data is the core of business intelligence, relying on data analysis and reporting techniques to derive meaningful insights from operations data.
  - Data lakes form the core of big data, AI, and ML applications for the vast amounts of data they hold.