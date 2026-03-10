# Data Built Tool (DBT) Essentials

# DBT Overview
- DBT is a command-line tool that enables data engineers and data analysts to to transform data in their warehouses more effectively. DBT is mainly used to perform the data transformations in the ELT process. It does not extract data from a source or load it into a data warehouse.
- At its most basic level, DBT has two components, a compiler and a runner. Users write DBT code in their text editor of choice, then invoke DBT from the command line. DBT compiles all code into raw SQL, then executes that code against the configured data warehouse.
- DBT fits nicely into the modern BI stack, coupling with products like Stitch, FiveTran, Redshift, Snowflake, BigQuery, Looker, and Mode
- Major Benefits:
  - Flexibility - DBT supports many popular databases such as Google BigQuery, Snowflake, Redshift, and PostgreSQL. This flexibility makes it versatile across different environments and projects.
  - Real-Time Monitoring - DBT supports real-time monitoring and alert features, which help maintain the health of data pipelines by enabling prompt resolution of issues.
  - Scalability - DBT has a distributed execution model, helping it utilize compute resources effectively. This allows it to quickly scale up or down based on demand and effectively manage large datasets and complex workflows. The compute resources utilized by DBT come from the underlying data warehouse technology, such as BigQuery or Snowflake.
- DBT in Data Engineering:
  - Data Transformation Engine - DBT serves as a powerful engine for transforming raw data into structured data formats for enhanced analysis, giving data engineers full control over transformations by defining complex SQL-based logic directly within the data warehouse.
  - Performance Optimization - DBT enhances performance by supporting incremental builds, enabling it to process only recent changes to data made after the last successful run. This minimizes compute resource usage and processing times.
  - Automated Testing - DBT offers built-in support for automated data testing, which helps ensure data transformations produce quality and accurate outputs, helping maintain data integrity.
  - Data Warehouse Support - DBT enables you to effortlessly integrate, manage, and analyze massive datasets in a centralized environment. Its ability to work with multiple data warehouses makes it the preferred solution for data engineers.
  - Continuous Integration and Deployment - DBT seamlessly integrates with CI/CD pipelines, deployment tools, and version control systems, enabling data engineering teams to automate testing and deployments.
- Key Concepts and Terminology:
  - Models - DBT arranges data transformations into logical units called models. These are SQL queries that transform data into tables or views, forming the backbone of DBT data pipelines.
  - Sources - DBT sources are a way of declaring tables of raw data collected from multiple sources, such as files, databases, or third-party applications.
  - Snapshots - DBT offers incremental tables known as snapshots to capture and store historical changes in source data over time. This is particularly useful for tracking slowly changing dimensions.
  - Seeds - Seeds are DBT models representing static data, typically sourced from CSV files. They are used for data that does not change frequently, such as dimension tables or lookup tables.
  - Profiles - Profiles incorporate data connection configurations, managed in a `profiles.yml` file, which specify how DBT connects to your data warehouse.
  - Packages - DBT packages are reuseable components such as hooks, macros, and models. These extend DBT functionality and optimize data transformation workflows.
  - Tests - In DBT, tests are assertions that check the quality of transformations to prevent errors in data processing. There are multiple types of tests in DBT, including data tests, schema tests, and user-defined tests for custom validations.
  - Documentation - This is the automatically-generated data from DBT metadata. It provides valuable insights into the structure and logic of data pipelines.
  - Projects - DBT projects comprise all components of a DBT workflow. This includes models, tests, configuration data, and all the relevant information for a specific data transformation. They manage all of the data transformation workflows by creating a structured environment.

## DBT Setup With Snowflake
- DBT can easily be integrated with Snowflake using the Partner Connect feature under Admin.
- Switch your account to Developer (Free) version to avoid having your account terminated after 14 days.

## Overview of DBT Cloud
- Most of the work done in DBT is conducted in the Studio, which provides an IDE where you can create models, macros, test cases, etc.
- Under Orchestration, you will mainly create and run jobs to execute models created and tested in the studio.

## Update DBT Default Credential
- The credentials that snowflake creates when it connects you with DBT will have limited permissions, so it's best to create a custom database in snowflake, then update settings in the DBT UI to connect with that database.
  ```
  USE ROLE ACCOUNTADMIN;
  USE WAREHOUSE COMPUTE_WH;
  CREATE OR REPLACE DATABASE DBT_DB;
  ```
- After creating the database in snowflake, go to Credentials in the DBT UI and update the snowflake connection settings. Update the Account to the account ID from snowflake, the database to `DBT_DB`, and the warehouse to `COMPUTE_WH`. Additionally, update the role to `ACCOUNTADMIN`.
- Next, update the DBT credentials, specifically role, database, and warehouse, to match the above snowflake connection settings. After that, update the development credentials to match your snowflake credentials. Update the schema to the `PUBLIC` schema automatically created for the `DBT_DB`.

## DBT Cloud Integration With GitHub
- Create a GitHub repo using your github account so that you don't lose any of your code created in the DBT UI if you lose access to the github account that was created during the snowflake setup.
- After creating the repo, update the linked github account in the DBT UI under Personal profile. Also update the Projects settings to the newly created repo.
- After updating the settings, go back to Studio and restart the IDE so future changes can be committed to the newly created repo. From the studio, you can create and commit changes, create feature branches, and create pull requests to merge changes from feature branches to the main branch.

## Execution of First DBT Model
- A model is like a blueprint of a table or view that represent entities in the database. Models should always be created in the 'models' folder of a project. When you write code to create models, DBT provides the option to run a model and build a model. Running a model will execute the code within the file. Building a model will execute the code in the model and run the test cases that were created for the model.
- Tests are configured in the `schema.yml` file in the 'models' folder on a per-column basis. DBT provides several default cases in this file, such as unique value tests and null checks.
- The `dbt run` command will execute all models in the 'models' folder sequentially. To run a specific model, you use the command `dbt run --select {model_name}`. Once the run is executed, debug logs are provided that can be helpful with troubleshooting failed runs or builds.
- The `dbt build` command will execute and test all models in the 'models' folder sequentially. To build a specific model, you use the command `dbt build --select {model_name}`.

## Create a DBT Model
```
Snowflake Code
============
USE ROLE ACCOUNTADMIN;
USE WAREHOUSE COMPUTE_WH;
USE SCHEMA DBT_DB.PUBLIC;

CREATE OR REPLACE TABLE DBT_DB.PUBLIC.EMPLOYEE_RAW 
(
EMPID INTEGER,
NAME STRING,
SALARY INTEGER,
HIREDATE DATE,
ADDRESS STRING
);


INSERT INTO DBT_DB.PUBLIC.EMPLOYEE_RAW (EMPID, NAME, SALARY, HIREDATE, ADDRESS) VALUES
(1, 'John Smith', 75000, '2021-03-15', '10 Downing Street, London, UK, SW1A 2AA'),
(2, 'Emily Davis', 82000, '2020-07-22', '350 Bay Street, Toronto, Canada, M5H 2S6'),
(3, 'Michael Johnson', 91000, '2019-11-05', '1 Macquarie Street, Sydney, Australia, 2000'),
(4, 'Rajesh Kumar', 67000, '2022-01-10', 'Gateway of India, Mumbai, India, 400001'),
(5, 'William Taylor', 98000, '2018-09-30', 'Pariser Platz, Berlin, Germany, 10117');


select * from DBT_DB.PUBLIC.EMPLOYEE_RAW ;

select * from DBT_DB.PUBLIC.EMPLOYEE;


DBT Model Code
============

{{
    config
    (
       materialized = 'table' -- Default setting is 'view'.
    )
}}


with employee as -- Transformation logic is written as a CTE.
(
    select
    EMPID as emp_id,
    split_part(NAME,' ',1)  as emp_firstname,
    split_part(NAME,' ',2)  as emp_lastname,
    SALARY as emp_salary,
    HIREDATE as emp_hiredate,
    split_part(ADDRESS,',',1) as emp_street,
    split_part(ADDRESS,',',2) as emp_city,
    split_part(ADDRESS,',',3) as emp_country,
    split_part(ADDRESS,',',4) as emp_zipcode
    from {{source('employee','EMPLOYEE_RAW')}} -- Table which already exists in Snowflake.
)
select * from employee




Yml file code
==========

version: 2


models:
  - name: employee
    description: "Employee DBT model"


sources:
  - name: employee -- custom name of the source.
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
```
- DBT **cannot** be used to import data from an external source. This means any data you want to base your models on needs to exist in your snowflake account before you can create the model that will be used to transform the data. That's why the snowflake code comes before the DBT code.
- When creating a `.yml` file for configuring a model, you can either create one file to configure all models in a folder or create separate files for each model within a folder. Either way, at least one file must exist in each folder.
- By default, DBT will always create an SQL query as a view, not a table. To fix the issue, you specify configuration as shown above.
- `from {{source('employee','EMPLOYEE_RAW')}}` explained:
  - The `source` must be defined in the `.yml` under `sources`, as shown above. This helps to specify where to retrieve the table from without having to write `from DBT_DB.PUBLIC.EMPLOY_RAW`, which can be cumbersome, especially when a table is used in multiple schemas.
  - If the table schema changes, it only needs to be updated in the `.yml` file, not everywhere the table is referenced in the DBT code.

## Create and Execute DBT Default Generic Tests
```
Yml file code
==========

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn -- simply provides a warning instead of failing the test.
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
```
- Documentation: https://docs.getdbt.com/docs/build/data-tests?version=1.12
- DBT provides 4 default test cases out of the box: `unique`, `not_null`, `accepted_values` and `relationships`
  - `unique`: The values in a specified column must be unique.
  - `not_null`: The values in a specified column must not be null.
  - `accepted_values`: The values in a specified column should exist in a list of accepted values (like a Java enum).
  - `relationships`: A certain relationship must exist between two columns. For example, each `customer_id` value in the `orders` model must exist as an `id` in the `customers` model. This is also known as referential integrity.
  - Example Code:
    ```
    models:
      - name: orders
        columns:
          - name: order_id
            data_tests:
              - unique
              - not_null
          - name: status
            data_tests:
              - accepted_values:
                  arguments: # available in v1.10.5 and higher. Older versions can set the <argument_name> as the top-level property.
                    values: ['placed', 'shipped', 'completed', 'returned']
          - name: customer_id
            data_tests:
              - relationships:
                  arguments:
                    to: ref('customers')
                    field: id
    ```
- The `dbt test` command will execute all tests in the 'models' folder sequentially. To build a specific model, you use the command `dbt test --select {model_name}`.

## Create and Execute DBT Custom Generic Tests
```
Tests folder code (tests/generic/test_salary_check.sql)
=============

{% test salary_check(model,column_name) %} -- Starts the test block.


select * from
{{ model }}
where {{ column_name }} < 10000 -- The test will fail if the value in column_name is below 10000.


{% endtest %} -- Ends the test block.


Yml file code
==========

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check      
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
```
- Documentation: https://docs.getdbt.com/best-practices/writing-custom-generic-tests
- Generic tests are defined in SQL files which can live in two places: `tests/generic/` and `macros/`. Tests should be placed in the `macros/` directory when they depend on complex macro logic. Here, the tests can be defined in the same file as the macros.
- When creating a test file, it's standard practice to prefix the filename with `test_`.
- `{% test salary_check(model,column_name) %}` explained:
  - A test case is typically written to be used across multiple models and column names.

## Materializations in DBT
- Documentation: https://docs.getdbt.com/docs/build/materializations?version=1.12
- Materializations are strategies for persisting DBT models in a warehouse. There are five types of materializations built into DBT: `table`, `view`, `incremental`, `ephemeral`, and `materialized`. Custom materializations can also be built to extend DBT's functionality to fit specific use cases.
- Configuring Materializations:
  - By default, DBT models are materialized as views. Models can be configured with different materializations by supplying the `materialized` configuration parameter.
  - This parameter can be specified in the project's `.yml` file, the model file, or the model's `.yml` file.
- View Materializations:
  - When using this type of materialization, your model is rebuilt as a view on each run, via the `create view as` statement.
  - Pros: No additional data is stored, views built on top of source data will always have the most up-to-date records.
  - Cons: Views that perform a significant transformation, or are stacked on top of other views, suffer from poor performance.
  - Advice:
    - Generally start with views for your models. Only change to another materialization when you notice performance issues.
    - Views are best suited for models that do not perform complex or demanding transformations, such as renaming or recasting columns.
- Table Materializations:
  - When using this type of materialization, your model is rebuilt as a table on each run, via the `create table as ` statement.
  - Pros: Tables are fast to query.
  - Cons:
    - Tables can take a long time to rebuild, especially for complex transformations.
    - New records in the underlying data source are not automatically added to the table.
  - Advice:
    - Use the table materialization for models being queried by BI tools. This gives the end user better performance.
    - Also use this materialization for slower transformations that are used by many downstream models.
- Incremental Materializations:
  - This type of materialization allows DBT to insert or update records into a table since the last time the model was run.
  - Pros: Build time can be significantly reduced by only transforming new records.
  - Cons: Incremental models require extra configuration and are an advanced usage of DBT.
  - Advice:
    - Incremental models are best for event-style data.
    - Only use incremental models when `dbt run` becomes slow.
- Ephemeral Materializations:
  - This type of materialization isn't built directly into the database. Instead, DBT will interpolate the code from an ephemeral model into its depend models using a CTE. You can assign an alias to this CTE, but DBT will always prefix it with the identifier `__dbt__cte__`.
  - Pros:
    - You can still write reuseable logic.
    - Ephemeral models help keep your data warehouse clean by reducing clutter.
  - Cons:
    - You cannot select directly from this model.
    - Operations, such as macros called using `dbt run-operation` cannot `ref()` ephemeral nodes.
    - Overuse of ephemeral materialization can make queries harder to debug.
    - Ephemeral materialization doesn't support model contracts.
  - Advice: Use Ephemeral Materialization For:
    - Very light-weight transformations that occur early in a DAG.
    - Are only used in one or two downstream models.
    - Do not need to be queried directly.
- Materialized View Materializations:
  - This type of materialization allows for the creation and maintenance of materialized views in the target database. Materialized views are combination of a view and a table, and serve use cases similar to incremental models.
  - Pros:
    - These views combine the query performance of a table with the data freshness of a view.
    - These views act much more like incremental materializations. However, they can be refreshed without interference on a regular cadence (depending on the database), forgoing the regular DBT batch refresh required with incremental materializations.
  - Cons:
    - Database platforms tend to have fewer configuration options for these views due to their complexity.
    - These views may not be supported by every database platform.
  - Advice:
    - Consider these views for cases where incremental models are sufficient, but you want incremental logic and refresh to be handled automatically.

## Create DBT Model (Materialization - Table-View)
```
Snowflake Code
============

CREATE OR REPLACE TABLE DBT_DB.PUBLIC.CUSTOMER_SRC (
    CUSTOMER_ID NUMBER,
    FIRST_NAME STRING,
    LAST_NAME STRING,
    EMAIL STRING,
    PHONE STRING,
    COUNTRY STRING,
    CREATED_AT TIMESTAMP_NTZ
);


INSERT INTO DBT_DB.PUBLIC.CUSTOMER_SRC (
    CUSTOMER_ID,
    FIRST_NAME,
    LAST_NAME,
    EMAIL,
    PHONE,
    COUNTRY,
    CREATED_AT
) VALUES 
(1001, 'John', 'Doe', 'john.doe@example.com', '+1-555-123-4567', 'USA', CURRENT_TIMESTAMP),
(1002, 'Maria', 'Gonzalez', 'maria.g@example.es', '+34-600-123-456', 'Spain', CURRENT_TIMESTAMP),
(1003, 'Kenji', 'Tanaka', 'kenji.t@example.jp', '+81-90-1234-5678', 'Japan', CURRENT_TIMESTAMP),
(1004, 'Amina', 'Ali', 'amina.ali@example.ke', '+254-712-345-678', 'USA', CURRENT_TIMESTAMP),
(1005, 'Liam', 'OConnor', 'liam.oconnor@example.ie', '+353-87-123-4567', 'Ireland', CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.CUSTOMER_SRC order by created_at desc;

SELECT * FROM DBT_DB.PUBLIC.CUSTOMER order by created_at desc;

SELECT * FROM DBT_DB.PUBLIC.CUSTOMER_VW order by created_at desc;


INSERT INTO DBT_DB.PUBLIC.CUSTOMER_SRC (
    CUSTOMER_ID,
    FIRST_NAME,
    LAST_NAME,
    EMAIL,
    PHONE,
    COUNTRY,
    CREATED_AT
) VALUES 
(1006, 'Sam', 'Altman', 'sam.altman@example.com', '+1-222-123-4567', 'USA', CURRENT_TIMESTAMP),
(1007, 'Mathew', 'Norman', 'mathew.norman@example.es', '+78-600-123-456', 'Germany', CURRENT_TIMESTAMP),
(1008, 'Jacob', 'Madison', 'jacob.madison@example.jp', '+1-78-1234-5678', 'USA', CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.CUSTOMER_SRC order by created_at desc;

SELECT * FROM DBT_DB.PUBLIC.CUSTOMER order by created_at desc;

SELECT * FROM DBT_DB.PUBLIC.CUSTOMER_VW order by created_at desc; -- Must manually build the customer table and view before the above insert takes effect.


DBT Code

customer.sql
=========

{{
    config
    (
        materialized = 'table'
    )
}}


with customer_src as
(
    select
    CUSTOMER_ID,
    FIRST_NAME,
    LAST_NAME,
    EMAIL,
    PHONE,
    COUNTRY,
    CREATED_AT,
    CURRENT_TIMESTAMP AS INSERT_DTS
    FROM {{source('customer','CUSTOMER_SRC')}}


)
SELECT * FROM customer_src




customer_vw.sql
=============

{{
    config
    (
        materialized = 'view'
    )
}}
select * from {{ ref('customer') }} -- References customer table created above.
where country= 'USA'



demo.yml
========

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"    
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
```

## Create DBT Model (Materialization - Incremental(append))
```
Snowflake Code
============

CREATE OR REPLACE TABLE DBT_DB.PUBLIC.SALES_SRC (
    SALE_ID INTEGER,
    SALE_DATE DATE,
    CUSTOMER_ID INTEGER,
    PRODUCT_ID INTEGER,
    QUANTITY INTEGER,
    TOTAL_AMOUNT NUMBER(10,2),
    CREATED_AT TIMESTAMP(6)
);



INSERT INTO DBT_DB.PUBLIC.SALES_SRC (SALE_ID, SALE_DATE, CUSTOMER_ID, PRODUCT_ID, QUANTITY, TOTAL_AMOUNT,CREATED_AT)
VALUES 
    (1, CURRENT_DATE, 1001, 501, 2, 49.98,CURRENT_TIMESTAMP),
    (2, CURRENT_DATE, 1001, 502, 1, 24.99,CURRENT_TIMESTAMP),
    (3, CURRENT_DATE, 1002, 501, 3, 74.97,CURRENT_TIMESTAMP),
    (4, CURRENT_DATE, 1003, 502, 5, 124.95,CURRENT_TIMESTAMP),
    (5, CURRENT_DATE, 1003, 503, 4, 99.96,CURRENT_TIMESTAMP);


SELECT * FROM DBT_DB.PUBLIC.SALES_SRC ORDER BY CREATED_AT DESC;

SELECT * FROM DBT_DB.PUBLIC.SALES ORDER BY CREATED_AT DESC;



INSERT INTO DBT_DB.PUBLIC.SALES_SRC (SALE_ID, SALE_DATE, CUSTOMER_ID, PRODUCT_ID, QUANTITY, TOTAL_AMOUNT,CREATED_AT)
VALUES 
    (6, CURRENT_DATE, 1001, 503, 3, 29.98,CURRENT_TIMESTAMP),
    (7, CURRENT_DATE, 1002, 504, 1, 62.97,CURRENT_TIMESTAMP),
    (8, CURRENT_DATE, 1004, 505, 2, 91.95,CURRENT_TIMESTAMP);


SELECT * FROM DBT_DB.PUBLIC.SALES_SRC ORDER BY CREATED_AT DESC;

SELECT * FROM DBT_DB.PUBLIC.SALES ORDER BY CREATED_AT DESC;



DBT Code

sales.sql
======

{{
    config
    (
        materialized = 'incremental',
        incremental_strategy = 'append'
    )
}}


with sales_src as
(
    select
    SALE_ID,
    SALE_DATE,
    CUSTOMER_ID,
    PRODUCT_ID,
    QUANTITY,
    TOTAL_AMOUNT,
    CREATED_AT,
    CURRENT_TIMESTAMP AS INSERT_DTS
    from {{source('sales','SALES_SRC')}}


    {% if is_incremental() %}
    where CREATED_AT > (select max(INSERT_DTS) from {{this}}) -- Limits the amount of new data processed/transformed.
    {% endif %}
)
select * from sales_src


demo.yml
=======

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"
  - name: sales
    description: "DBT model for the sales table"    
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
  - name: sales
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SALES_SRC
```
- Documentation: https://docs.getdbt.com/docs/build/incremental-strategy?version=1.12

## Create DBT Model (Materialization - Incremental(Delete+Insert))
```
Snowflake Code
============

CREATE OR REPLACE TABLE DBT_DB.PUBLIC.PRODUCT_SRC (
    PRODUCT_ID INT PRIMARY KEY,
    PRODUCT_NAME VARCHAR(100),
    PRODUCT_PRICE DECIMAL(10, 2),
    CREATED_AT TIMESTAMP
);


INSERT INTO DBT_DB.PUBLIC.PRODUCT_SRC (PRODUCT_ID, PRODUCT_NAME, PRODUCT_PRICE, CREATED_AT) VALUES
(101, 'Wireless Mouse', 25.99, CURRENT_TIMESTAMP),
(102, 'Bluetooth Keyboard', 45.50, CURRENT_TIMESTAMP),
(103, 'HD Monitor', 199.99, CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.PRODUCT_SRC ORDER BY PRODUCT_ID ASC,CREATED_AT DESC;

SELECT * FROM DBT_DB.PUBLIC.PRODUCT ORDER BY PRODUCT_ID ASC,CREATED_AT DESC;


INSERT INTO DBT_DB.PUBLIC.PRODUCT_SRC (PRODUCT_ID, PRODUCT_NAME, PRODUCT_PRICE, CREATED_AT) VALUES
(103, '4K Gaming Monitor', 199.99, CURRENT_TIMESTAMP),
(104, 'Wireless Earbuds', 69.50, CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.PRODUCT_SRC ORDER BY PRODUCT_ID ASC,CREATED_AT DESC;

SELECT * FROM DBT_DB.PUBLIC.PRODUCT ORDER BY PRODUCT_ID ASC,CREATED_AT DESC;



DBT Code
=======

product.sql
========

{{
    config
    (
        materialized = 'incremental',
        incremental_strategy = 'delete+insert',
        unique_key = 'PRODUCT_ID'
    )
}}


with product_src as
(
    select
    PRODUCT_ID,
    PRODUCT_NAME,
    PRODUCT_PRICE,
    CREATED_AT,
    CURRENT_TIMESTAMP AS INSERT_DTS
    from {{source('product','PRODUCT_SRC')}}


    {% if is_incremental() %}
    where CREATED_AT > (select max(INSERT_DTS) from {{this}})
    {% endif %}
)


select * from product_src


demo.yml
=======

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"
  - name: sales
    description: "DBT model for the sales table"
  - name: product
    description: "DBT Model for the product table"    
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
  - name: sales
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SALES_SRC
  - name: product
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PRODUCT_SRC
```
- For SCD type 1 source tables, DBT supports a 'delete+insert' strategy and a 'merge' (update+insert) strategy for updating rows based on changing data.
- When choosing between the two, it's usually best to pick 'delete+insert' because a delete operation is faster than an update operation.

## Create DBT Model (Materialization - Incremental(Merge))
```
Snowflake Code
============

CREATE OR REPLACE TABLE DBT_DB.PUBLIC.PURCHASE_SRC (
    PURCHASE_ID INT,
    PURCHASE_DATE DATE,
    PURCHASE_STATUS VARCHAR(50),
    CREATED_AT TIMESTAMP
);


INSERT INTO DBT_DB.PUBLIC.PURCHASE_SRC (PURCHASE_ID, PURCHASE_DATE, PURCHASE_STATUS, CREATED_AT)
VALUES 
(101, CURRENT_DATE, 'PROCESSING',CURRENT_TIMESTAMP),
(102, CURRENT_DATE, 'SHIPPED',CURRENT_TIMESTAMP),
(103, CURRENT_DATE, 'DELIVERED',CURRENT_TIMESTAMP);


SELECT * FROM DBT_DB.PUBLIC.PURCHASE_SRC ORDER BY CREATED_AT DESC;

SELECT * FROM DBT_DB.PUBLIC.PURCHASE ORDER BY PURCHASE_ID,CREATED_AT DESC;


INSERT INTO DBT_DB.PUBLIC.PURCHASE_SRC (PURCHASE_ID, PURCHASE_DATE, PURCHASE_STATUS, CREATED_AT)
VALUES 
(101, CURRENT_DATE, 'SHIPPED',CURRENT_TIMESTAMP),
(102, CURRENT_DATE, 'DELIVERED',CURRENT_TIMESTAMP),
(104, CURRENT_DATE, 'PROCESSING',CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.PURCHASE_SRC ORDER BY CREATED_AT DESC;

SELECT * FROM DBT_DB.PUBLIC.PURCHASE ORDER BY PURCHASE_ID,CREATED_AT DESC;



DBT Code
========

purchase.sql
=========

{{
    config
    (
        materialized = 'incremental',
        incremental_strategy = 'merge', -- update+insert strategy.
        unique_key = 'PURCHASE_ID', -- Column used to decide if an update+insert is necessary.
        merge_exclude_columns = ['INSERT_DTS'] -- List of columns that should not be updated.
    )
}}
with purchase_src as
(
    select
    PURCHASE_ID,
    PURCHASE_DATE,
    PURCHASE_STATUS,
    CREATED_AT,
    CURRENT_TIMESTAMP as INSERT_DTS, -- When the data was first inserted.
    CURRENT_TIMESTAMP as UPDATE_DTS -- When the data updated.
    from {{source('purchase','PURCHASE_SRC')}}


    {% if is_incremental() %}
    where CREATED_AT > (select max(UPDATE_DTS) from {{this}})
    {% endif %}
)
select * from purchase_src




demo.yml
=======

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"
  - name: sales
    description: "DBT model for the sales table"
  - name: product
    description: "DBT Model for the product table"
  - name: purchase
    description: "DBT model for the purchase table"    
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
  - name: sales
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SALES_SRC
  - name: product
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PRODUCT_SRC
  - name: purchase
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PURCHASE_SRC
```

## Create DBT Model (Materialization - Ephemeral)
```
Snowflake Code
============

CREATE OR REPLACE TABLE DBT_DB.PUBLIC.BASE_ORDERS
(
ORDER_ID INTEGER,
ORDER_DATE DATE,
CUSTOMER_ID INTEGER,
CUSTOMER_NAME STRING,
CREATED_AT TIMESTAMP(6)
);

INSERT INTO DBT_DB.PUBLIC.BASE_ORDERS (ORDER_ID,ORDER_DATE,CUSTOMER_ID,CUSTOMER_NAME,CREATED_AT)
VALUES
(101,CURRENT_DATE,1001,'maRk',CURRENT_TIMESTAMP),
(102,NULL,2001,'JOHn',CURRENT_TIMESTAMP),
(102,CURRENT_DATE,2001,'JOHn',CURRENT_TIMESTAMP),
(103,CURRENT_DATE,3001,'TOm',CURRENT_TIMESTAMP),
(104,CURRENT_DATE,4001,NULL,CURRENT_TIMESTAMP),
(105,CURRENT_DATE,5001,'sAm',CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.BASE_ORDERS;

SELECT * FROM DBT_DB.PUBLIC.CLEAN_ORDERS; -- Doesn't exist since it was based on an ephemeral model.

SELECT * FROM DBT_DB.PUBLIC.FINAL_ORDERS;


DBT Code
=======

clean_orders.sql
=============


{{
    config
    (
        materialized = 'ephemeral'
    )
}}


with base_orders as
(
    select
    ORDER_ID,
    ORDER_DATE,
    CUSTOMER_ID,
    case when CUSTOMER_NAME is null then 'NA' else upper(CUSTOMER_NAME) end as CUSTOMER_NAME,
    CREATED_AT
    from {{source('orders','BASE_ORDERS')}}
    where ORDER_DATE is not null
)
select * from base_orders




final_orders.sql
============

{{
    config
    (
        materialized = 'table'
    )
}}
with clean_orders as
(
    select
    ORDER_ID,
    ORDER_DATE,
    CUSTOMER_ID,
    CUSTOMER_NAME,
    CREATED_AT,
    CURRENT_TIMESTAMP as INSERT_DTS
    from {{ ref('clean_orders') }} -- 'clean_orders' is created in DBT, not Snowflake, which is why we use 'ref' instead of 'source'.
)
select * from clean_orders




demo.yml
=======

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"
  - name: sales
    description: "DBT model for the sales table"
  - name: product
    description: "DBT Model for the product table"
  - name: purchase
    description: "DBT model for the purchase table"
  - name: clean_orders
    description: "DBT ephermeral model for the clean order"  
  - name: final_orders
    description: "DBT model for the finale orders model"
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
  - name: sales
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SALES_SRC
  - name: product
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PRODUCT_SRC
  - name: purchase
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PURCHASE_SRC
  - name: orders
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: BASE_ORDERS
```
- Documentation: https://docs.getdbt.com/docs/build/materializations?version=1.12
- Ephemeral models are best used to perform data cleansing, where you want to transform the data, but you don't want to store the results of those transformations in a separate table. You only want the clean data.

## Create DBT Snapshot
```
Snowflake Code
============

CREATE OR REPLACE TABLE DBT_DB.PUBLIC.PATIENT_SRC
(
PATIENT_ID INTEGER,
PATIENT_NAME STRING,
PATIENT_CONTACT_NUMBER STRING,
PATIENT_EMAIL_ID STRING,
PATIENT_ADDRESS STRING,
CREATED_AT TIMESTAMP(6)
);

INSERT INTO DBT_DB.PUBLIC.PATIENT_SRC (PATIENT_ID,PATIENT_NAME,PATIENT_CONTACT_NUMBER,PATIENT_EMAIL_ID,PATIENT_ADDRESS,CREATED_AT)
VALUES
(1,'Alice Thompson','555-123-4567','alice.thompson@email.com','123 Maple St',CURRENT_TIMESTAMP),
(2,'Brian Lee','555-234-5678','brian.lee@email.com','456 Oak Rd',CURRENT_TIMESTAMP),
(3,'Carla Martinez','555-345-6789','carla.m@email.com','789 Pine Ave',CURRENT_TIMESTAMP),
(4,'Daniel Connor','555-456-7890','doconnor@email.com','321 Birch Blvd',CURRENT_TIMESTAMP),
(5,'Eva Zhang','555-567-8901','eva.zhang@email.com','654 Cedar Ln',CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.PATIENT_SRC ORDER BY PATIENT_ID;

SELECT * FROM DBT_DB.PUBLIC.PATIENT_SNAPSHOT ORDER BY PATIENT_ID;

select * from DBT_DB.PUBLIC.PATIENT_SNAPSHOT where patient_id=1 and dbt_valid_to is null;

INSERT INTO DBT_DB.PUBLIC.PATIENT_SRC (PATIENT_ID,PATIENT_NAME,PATIENT_CONTACT_NUMBER,PATIENT_EMAIL_ID,PATIENT_ADDRESS,CREATED_AT)
VALUES
(1,'Alice Thompson','555-123-9999','alice.thompson@email.com','123 Maple St',CURRENT_TIMESTAMP),
(2,'Brian Lee','555-234-5678','brian.lee123@email.com','456 Oak Rd',CURRENT_TIMESTAMP),
(5,'Eva Zhang','555-567-8901','eva.zhang@email.com','820 Cedar Ln',CURRENT_TIMESTAMP);

SELECT * FROM DBT_DB.PUBLIC.PATIENT_SRC ORDER BY PATIENT_ID;

SELECT * FROM DBT_DB.PUBLIC.PATIENT_SNAPSHOT ORDER BY PATIENT_ID;

select * from DBT_DB.PUBLIC.PATIENT_SNAPSHOT where patient_id=1 and dbt_valid_to is null;


DBT Code
========

patient_snapshot.sql
================


{% snapshot patient_snapshot %}


{{
    config
    (
        strategy = 'check',
        unique_key = 'PATIENT_ID',
        check_cols = ['PATIENT_NAME','PATIENT_CONTACT_NUMBER','PATIENT_EMAIL_ID','PATIENT_ADDRESS'] -- All non-primary keys.
    )
}}


select * from {{source('patient','PATIENT_SRC')}}




{% endsnapshot %}


demo.yml
========

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"
  - name: sales
    description: "DBT model for the sales table"
  - name: product
    description: "DBT Model for the product table"
  - name: purchase
    description: "DBT model for the purchase table"
  - name: clean_orders
    description: "DBT ephermeral model for the clean order"  
  - name: final_orders
    description: "DBT model for the finale orders model"
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
  - name: sales
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SALES_SRC
  - name: product
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PRODUCT_SRC
  - name: purchase
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PURCHASE_SRC
  - name: orders
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: BASE_ORDERS
  - name: patient
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PATIENT_SRC
```
- Documentation: https://docs.getdbt.com/docs/build/snapshots?version=1.12
- Snapshots are used to implement SCD type 2 source tables, where rows are added instead of updated when one or more attributes a dimension change. Snapshots help to build this kind of table by recording changes in dimensions over time.
- SQL files containing snapshots should be stored in a 'snapshots' directory within your DBT project.
- To execute a snapshot, you use the command `dbt snapshot`. This runs all of the snapshots in the 'snapshots' folder. This creates a separate table where changes in dimensions are tracked by DBT.

## Create DBT Seed
```
Seed Data
========

country_code.csv
=============

country_code,country_name,continent
US,United States,North America
CA,Canada,North America
BR,Brazil,South America
FR,France,Europe
CN,China,Asia
IN,India,Asia
NG,Nigeria,Africa
AU,Australia,Oceania
RU,Russia,Europe/Asia
JP,Japan,Asia



country_code,country_name,continent,currency -- This data replaces the above data to simulate adding a column. The file doesn't contain two tables.
US,United States,North America,USD
CA,Canada,North America,CAD
BR,Brazil,South America,BRL
FR,France,Europe,EUR
CN,China,Asia,CNY
IN,India,Asia,INR
NG,Nigeria,Africa,NGN
AU,Australia,Oceania,AUD
RU,Russia,Europe/Asia,RUB
JP,Japan,Asia,JPY


Snowflake Code
============

SELECT * FROM DBT_DB.PUBLIC.COUNTRY_CODE;

CREATE TABLE DBT_DB.PUBLIC.SESSION_SRC (
    SESSION_ID VARCHAR(10),
    USER_ID VARCHAR(10),
    BROWSER VARCHAR(20),
    DEVICE_TYPE VARCHAR(20),
    COUNTRY_CODE CHAR(2),
    START_TIME TIMESTAMP,
    END_TIME TIMESTAMP,
    PAGES_VISITED INT
);


INSERT INTO DBT_DB.PUBLIC.SESSION_SRC (
    SESSION_ID, USER_ID, BROWSER, DEVICE_TYPE, COUNTRY_CODE, START_TIME, END_TIME, PAGES_VISITED
) VALUES
('S001', 'U1001', 'CHROME', 'DESKTOP', 'US', '2025-04-14 09:12:00', '2025-04-14 09:35:00', 5),
('S002', 'U1002', 'FIREFOX', 'LAPTOP', 'CA', '2025-04-14 10:00:00', '2025-04-14 10:18:00', 3),
('S003', 'U1003', 'SAFARI', 'MOBILE', 'JP', '2025-04-14 10:45:00', '2025-04-14 11:10:00', 7),
('S004', 'U1004', 'EDGE', 'TABLET', 'FR', '2025-04-14 11:15:00', '2025-04-14 11:30:00', 4),
('S005', 'U1005', 'CHROME', 'MOBILE', 'IN', '2025-04-14 12:00:00', '2025-04-14 12:25:00', 6),
('S006', 'U1006', 'OPERA', 'DESKTOP', 'BR', '2025-04-14 12:30:00', '2025-04-14 12:45:00', 2),
('S007', 'U1007', 'CHROME', 'LAPTOP', 'AU', '2025-04-14 13:00:00', '2025-04-14 13:40:00', 8),
('S008', 'U1008', 'SAFARI', 'TABLET', 'RU', '2025-04-14 13:50:00', '2025-04-14 14:05:00', 3),
('S009', 'U1009', 'EDGE', 'MOBILE', 'NG', '2025-04-14 14:10:00', '2025-04-14 14:30:00', 5),
('S010', 'U1010', 'FIREFOX', 'DESKTOP', 'CN', '2025-04-14 14:45:00', '2025-04-14 15:00:00', 4);

SELECT * FROM DBT_DB.PUBLIC.SESSION_SRC ORDER BY SESSION_ID;


SELECT * FROM DBT_DB.PUBLIC.SESSION ORDER BY SESSION_ID;



DBT Code
========

session.sql
========

{{
    config
    (
        materialized = 'table'
    )
}}
with session_src as
(
    select
    SESSION_ID,
    USER_ID,
    BROWSER,
    DEVICE_TYPE,
    b.country_name as country_name,
    b.continent as continent,
    b.currency as currency,
    START_TIME,
    END_TIME,
    PAGES_VISITED,
    CURRENT_TIMESTAMP as INSERT_DTS
    from {{source('session','SESSION_SRC')}} a
    left join {{ref('country_code')}} b
    on a.COUNTRY_CODE = b.COUNTRY_CODE
)
select * from session_src



demo.yml
=======

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"
  - name: sales
    description: "DBT model for the sales table"
  - name: product
    description: "DBT Model for the product table"
  - name: purchase
    description: "DBT model for the purchase table"
  - name: clean_orders
    description: "DBT ephermeral model for the clean order"  
  - name: final_orders
    description: "DBT model for the finale orders model"
  - name: session
    description: :DBT Model for the session table"
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
  - name: sales
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SALES_SRC
  - name: product
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PRODUCT_SRC
  - name: purchase
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PURCHASE_SRC
  - name: orders
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: BASE_ORDERS
  - name: patient
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PATIENT_SRC
  - name: session
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SESSION_SRC
```
- In DBT, seeds are used to upload static data to a data warehouse.
- When creating a seed, you must first upload the CSV data file to the 'seeds' folder in the project directory. In this case, `country_code.csv`. Once the file is uploaded, running the `dbt seed --select country_code` command will upload the data to your data warehouse.
  - When you want to modify a seed file by adding an extra column, running `dbt seed --select country_code` will fail because the current table schema does not contain the additional column. To add the column, you must run `dbt seed --select country_code --full-refresh`, which deletes and re-creates the table with the new schema.

## Create DBT Macro
```
DBT Code
========

concat_name.sql
=============

{{ 
    config
    ( 
        materialized='table'
    )
}}

select concat('John','Smith') as name


concat_address.sql
===============

{{ 
    config
    ( 
        materialized='table'
    )
}}

select concat('123Street','Chicago') as address


demo.yml
========

version: 2


models:
  - name: employee
    description: "Employee DBT model"
    columns:
      - name: emp_id
        data_tests:
          - unique
          - not_null
          - accepted_values:
              arguments:
                values: ['1','2','3','4','5']
                config:
                  severity: warn
      - name: emp_salary
        data_tests:
          - salary_check
  - name: customer
    description: "DBT Model for the customer table"  
  - name: customer_vw
    description: "DBT Model for the customer view"
  - name: sales
    description: "DBT model for the sales table"
  - name: product
    description: "DBT Model for the product table"
  - name: purchase
    description: "DBT model for the purchase table"
  - name: clean_orders
    description: "DBT ephermeral model for the clean order"  
  - name: final_orders
    description: "DBT model for the finale orders model"
  - name: session
    description: "DBT Model for the session table"
  - name: concat_name
    description: "DBT Model for the concat name"
  - name: concat_address
    description: "DBT Model for the concat address"
sources:
  - name: employee
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: EMPLOYEE_RAW
  - name: customer
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: CUSTOMER_SRC
  - name: sales
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SALES_SRC
  - name: product
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PRODUCT_SRC
  - name: purchase
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PURCHASE_SRC
  - name: orders
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: BASE_ORDERS
  - name: patient
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: PATIENT_SRC
  - name: session
    database: DBT_DB
    schema: PUBLIC
    tables:
      - name: SESSION_SRC




Macro Code
=========

concat_macro.sql
==============

{% macro concat_macro(value1,value2) %}


concat( '{{value1}}','-', '{{value2}}' ) -- Centralizes concatenation logic, so the logic doesn't need to be updated separately in each model where it is used.


{% endmacro %}



concat_name.sql
=============

{{
    config(
        materialized='table'
    )
}}


select {{ concat_macro('John','Smith') }} as name


concat_address.sql
===============

{{
    config
    (
        materialized = 'table'
    )
}}
select {{ concat_macro('123street','Chicago') }} as address


Snowflake Code
=============

select * from DBT_DB.PUBLIC.CONCAT_ADDRESS;

select * from DBT_DB.PUBLIC.CONCAT_NAME;
```
- A DBT macro is a reuseable piece of code that can be used in different models, just like a function in a library. Macros should be created in the 'macros' folder in the project directory.
- Multiple models can be run at the same time using the `dbt build --select {model_name}` by separating each model with a space.

## Create DBT Environments and Jobs
```
Snowflake Code
============

CREATE OR REPLACE DATABASE DBT_DB_STG;

CREATE OR REPLACE DATABASE DBT_DB_PROD;
```
- The above databases were created for the 'Staging' and 'production' environments in DBT.
- When creating an environment, you must also create a connection profile that links it to your github and snowflake accounts.
- Once the environment is created, you can create jobs within that environment to run and/or build your models so you don't have to do so manually.
- Ideally, a job should only execute commands, such `dbt seed/build/snapshot` on one model.