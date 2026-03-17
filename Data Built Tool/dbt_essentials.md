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

## Analytics Development Lifecycle (ADLC)
- The key difference between ETL and ELT is where the data transformation takes place. In ETL, data is transformed before being loaded into a data warehouse/lake. In ELT, data is transformed after being loaded into a data warehouse/lake.
- In ETL workflows, most meaningful data transformation occurs outside this primary pipeline in a downstream business intelligence (BI) platform. Transformations can include renaming, casting, joining or enriching values within columns.
- In ELT workflows, data is extracted and loaded into a data warehouse first, allowing the data to be transformed using the warehouse’s computing power. ELT has emerged as a paradigm for how to manage information flows in a modern data warehouse. This represents a fundamental shift from how data previously was handled when ETL was the data workflow most companies implemented.
- Primary Benefits of ELT:
  - ELT aligns with the scalability and flexibility of modern data stacks, enabling organizations to work with large datasets more efficiently.
  - Leverages Cloud Infrastructure: ELT takes advantage of the massive processing power of cloud-native data warehouses like Snowflake, BigQuery, and Redshift. By loading raw data into the warehouse first, ELT enables these systems to handle transformations at scale, which is particularly valuable when working with large volumes of data.
  - Faster Data Availability: With ELT, raw data is loaded into the warehouse immediately, making it accessible for analysis more quickly. This reduces the delay often seen in ETL processes, where data must be transformed before it’s available for querying​.
  - Cost Savings: ELT reduces the need for expensive on-premises hardware or complex ETL tools. Instead, it capitalizes on the inherent processing capabilities of cloud data warehouses, optimizing both performance and cost. In modern data stacks, offloading transformation tasks to cloud services can lead to significant cost savings​.
  - Flexible, Iterative Transformation: ELT allows for more flexible data transformations. Since the raw data is already in the warehouse, analysts and data engineers can transform data iteratively, applying changes and optimizations without having to reload or reprocess the entire dataset. This flexibility makes it easier to adapt to evolving business needs and ensures that teams can always work with the latest data​.
  - Data Democratization: By loading raw data into the warehouse first, ELT supports a more self-service data model. Analysts and data teams can access and transform data as needed without being bottle-necked by upstream ETL processes. This democratization fosters greater agility and collaboration across teams​.
- DBT plays a crucial role in the ELT process by serving as the transformation layer within the data warehouse. While ELT relies on loading raw data into the warehouse, DBT empowers teams to manage and automate their transformations, ensuring the data is clean and analytics-ready.
- Data Team Roles:
  - Data Engineer:
    - Builds systems to collect and process data. Data engineers create the foundation for all data-related work by building reliable, scalable data pipelines.
    - Design data infrastructure and architecture.
    - Create and maintain data pipelines.
    - Ensure data quality and availability.
    - Connect different data sources seamlessly and automate data collection.
  - Analytics Engineer:
    - Explore data already ingested into data platforms in response to stakeholder questions and needs.
    - Clean and prepare data for analytical use cases.
    - Transform prepared datasets into objects that can serve organizational objectives, such as a super-table that can serve as a base for multiple applications.
    - Document the objects they find and create in the data warehouse, ensuring other users can see, understand, and use them. Documentation also helps to optimize storage utilization by ensuring data doesn't sit idle in storage unused and/or misunderstood.
    - Respond to stakeholder needs, ensuring data engineers have more time to focus on critical maintenance and infrastructure updates.
  - Data Analyst:
    - Evaluate transformed data and turn it into business insights.
    - Answer questions and solve business problems using data analysis methods.
    - Interpret data to find trends.
    - Create reports and visualizations.
    - Work closely with business stakeholders.
    - Provide value through actionable insights, helping businesses make informed decisions and drive strategic business outcomes.
    - Translate complex findings into clear recommendations.
- How DBT fits into the data pipeline:
  - Data Source --> Loader (FiveTran, Stytch, AirByte) --> Data Platform (Snowflake, BigQuery, DataBricks) --> **DBT** --> Downstream Operational and Analytics Tools.
- ADLC:
  - Plan: Teams determine the what needs to be done, clarify priorities, get shared expectations.
  - Develop: Write code to transform data into something useful. In DBT, that typically means creating SQL models.
  - Testing: Test data to ensure high data quality.
  - Deploy: Push changes to a production environment. This typically means building automated pipelines that test and deploy code after its been reviewed.
  - Operate: Running deployed code consistently in a data pipeline. In DBT, this typically means scheduling jobs, monitoring runtimes, and configuring alerts for when things go wrong.
  - Observe: Observing data pipelines, looking to see if models were executed correctly and tests passed.
  - Discover: Explore models, understand logic, and find answers.
  - Analyze: Analyze data and make insights that can potentially lead to further planning, starting the cycle over again.
- Data Control Plane Components:
  - Like air traffic control, the control plane doesn't move data itself, it orchestrates. governs, and observes the data. This gives a data team insights into what's running, what's changed, and what's breaking.
  - DBT Mesh (Design): Enables domain-level data ownership without compromising governance or creating silos.
  - DBT Catalog (Discover): Navigate, understand, and improve DBT cloud projects.
  - DBT Semantic Layer (Align): Deliver consistent metrics wherever downstream teams work.
  - DBT Studio, DBT Canvas, and VS Code (Build): Get the flexibility to build where you want.
  - Scheduler and CI (Deploy): Automate how and when jobs are run, whether they are run in a staging environment or production.
  - Testing and Alerts (Observe): Proactively enforce data quality and resolve issues quickly.

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
- The `dbt run` command will execute all models in the 'models' folder sequentially. This materializes the model(s) into the data warehouse. To run a specific model, you use the command `dbt run --select {model_name}`. Once the run is executed, debug logs are provided that can be helpful with troubleshooting failed runs or builds.
- The `dbt build` command will execute and test all models in the 'models' folder sequentially. To build a specific model, you use the command `dbt build --select {model_name}`.
  - The command will first run tests on your sources.
  - Next, if those tests pass, the command will start to run, then immediately test each of your staging models.
  - As models are successfully ran and tested, the build command progressively moves in a logical order to the next layer of models.
  - If any test fails during this process, it is immediately halted and the command fails. This ensures erroneous data never makes it to downstream models.
  - Overall, the `build` command is four commands in one:
    - `dbt run` - Transforms and builds models in your warehouse.
    - `dbt test` - Validates data for quality issues.
    - `dbt seed` - Loads CSV data into warehouse tables.
    - `dbt snapshot` - Tracks slowly changing dimensions in your data.

## Understanding DBT Sources
- A source is simply raw data loaded into DBT from a database platform such as snowflake. Sources tell DBT the pre-existing data that needs to be queried from data platform. In DBT, a source needs to be referenced using the `database.schema.table` format. This can become cumbersome if data is moved to another database or schema.
- In DBT, this is resolved by referencing the database, schema, and name of a table in a `.yml` file, then giving this reference an alias that can be used in models. This means the table details only need to be updated in the `.yml` file if the details change.
- When the `.yml` file is properly configured, `database.schema.table` can be replaced with `{{ source('source_alias', 'table_name') }}`.
- Sources and staging models should have a one-to-one relationship.

### Source Freshness
```
sources:
  - name: jaffle_shop
    database: raw
    schema: jaffle_shop
    tables:
      - name: customers -- Customer details don't change frequently and don't need a freshness check.
      - name: orders -- Order details changes more frequently and will cause problems if data becomes stale.
        config:
          freshness:
            warn_after: -- Warning is issued about data becoming stale.
              count: 6
              period: hour
            error_after: -- Error is thrown that data is critically outdated.
              count: 12
              period: hour
          loaded_at_field: _etl_loaded_at -- Column in table that DBT will use to check the last load time.
```
```
sources:
  - name: jaffle_shop
    database: raw
    schema: jaffle_shop
    config: -- Config block moved to sources level to apply to all tables.
      freshness:
        warn_after:
          count: 6
          period: hour
        error_after:
          count: 12
          period: hour
      loaded_at_field: _etl_loaded_at
    tables:
      - name: customers
        config:
          freshness: null -- Customers table excluded from freshness checks
      - name: orders
```
- Source freshness can be configured at the `source` level or the `table` level. When the freshness config is set at the source level, `freshness: null` can be used at the table level to eliminate freshness checks for that table.
- The `period` for freshness can be `minute`, `hour`, or `day`.
- The `dbt source freshness` command checks source freshness and will issue a warning or error based on the above config.

### Using the CodeGen Package
- Real-world projects contain 100's to 1000's of tables in your data warehouse that need to be configured in your `.yml` config file. Instead of manually creating this file, the CodeGen package can be used to automate this process.
- Documentation: https://hub.getdbt.com/dbt-labs/codegen/latest/
- Create a `packages.yml` file in your project (no particular folder) and place the following code in it:
  ```
  packages:
    - package: dbt-labs/codegen
      version: 0.14.0
  ```
- Next, run `dbt deps` to install the package.
- Next, open an empty file and place the following code inside of it: `{{ codegen.generate_source(schema_name= 'jaffle_shop', database_name= 'raw') }}`. Then, compile the code to get the generated yml code.
- Example of Using CLI: `dbt run-operation generate_source --args '{"schema_name": "PUBLIC", "database_name": "DBT_DB"}'`
- Example of Using Compile: `{{ codegen.generate_source(schema_name= 'PUBLIC', database_name= 'DBT_DB') }}`. Pass this into an untitled document and press the `Compile` button.
- Either of the above methods produces the code that can be copied and saved into a `.yml` config file.
- Once the config file is created, the `Generate Model` button above the name of each table for each source can be used to create a staging model for that table.
- Once the models are created, they can be styled using this [guide](https://docs.getdbt.com/best-practices/how-we-style/1-how-we-style-our-dbt-models?version=1.12).

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
- When working in a development environment, developers should always be building models on top of their own unique target schema (for demo purposes, we're using the `PUBLIC` schema of the snowflake DB).
- When creating a `.yml` file for configuring a model, you can either create one file to configure all models in a folder or create separate files for each model within a folder. Either way, at least one file must exist in each folder.
- By default, DBT will always create an SQL query as a view, not a table. To fix the issue, you specify configuration as shown above.
- `from {{source('employee','EMPLOYEE_RAW')}}` explained:
  - The `source` must be defined in the `.yml` under `sources`, as shown above. This helps to specify where to retrieve the table from without having to write `from DBT_DB.PUBLIC.EMPLOY_RAW`, which can be cumbersome, especially when a table is used in multiple schemas.
  - If the table schema changes, it only needs to be updated in the `.yml` file, not everywhere the table is referenced in the DBT code.
- `{{ config(materialized='view') }}` explained.
  - Sets the materialization specifically for the model defined within the SQL file. This can also be set in the `.yml` configuration file for the project:
    ```
    models:
      project_name:
        folder_name:
          +materialized: table
    ```
      - The config set at the SQL-file level will override the config set in the `.yml` file.
      - The `+` before `materialized` indicates it's a property, not a subdirectory.

### Model Naming Conventions
- Source (`src`): Tables of raw data loaded into a data warehouse.
- Staging (`stg`): Transforming data based on business needs, which can involve things like renaming and/or recasting columns.
- Intermediate (`int`): Where joins and aggregations occur. These should not depend directly on sources and should depend on staging models instead.
- Fact (`fct`): Data representing real-world processes that have occurred or are occurring. Typically an immutable event stream, such as sessions, transactions, or orders.
- Dimension (`dim`): Data representing people, places, or things. Typically mutable, but slowly-changing (SCD) entities, such as customers, products, or employees.
- Staging model: References upstream models using the `source` macro. Performs light transformations on raw data.
- Marts model: References upstream models using the `ref` macro. Applies business logic for stakeholders.

### Troubleshooting DBT Run
- Sometimes, a DBT run will fail because a model and its dependencies were not built in the proper order, to resolve this, you can use the commands below:
  - `dbt run --select +{model_name}` builds the model and any upstream dependencies.
  `dbt run --select {model_name}+` builds the model and any downstream dependencies.
  - `dbt run --select +{model_name}+` builds the model and any upstream and downstream dependencies.
  - This nomenclature also works for the `dbt build` and `dbt test` commands.

## Create and Execute DBT Default Generic Tests
```
Yml file code
==========

version: 2


models:
  - name: employee -- model name.
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
- `unique` and `not_null` tests should be applied to all primary keys. This will help to prevent breaking joins and other complex queries downstream.
- Testing Best Practices:
  - Sources should be tested to assess the quality of your raw data. These tests should be simple quality checks that are covered by the 4 generic tests mentioned above.
  - Models should be tested to validate the accuracy and validity of your transformations. These can range from the simple generic tests mentioned above to more complex custom-built tests that enforce specific business criteria.

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
- Custom generic tests are used to verify a model or column adheres to specific business rules and validating complex business logic.
- The custom generic test fails if the specified query returns any rows.
- Instead of using Jinja as shown above, you can put a regular `.sql` file in the `tests` directory and run them using `dbt test --select {test_name}`.
  ```
  -- assert_stg_stripe__payment_total_positive.sql

  select
      order_id,
      sum(payment_amount)
  from {{ ref('stg_stripe__payments') }}
  group by order_id
  having sum(payment_amount) < 0 -- The query should be written to return rows that violate the testing criteria.
  ```
- testing is configured the same way for both `models` and `sources` within the config file. To test specific sources, use the command `dbt test --select source:{source_name}`. The `dbt test --select source:*` will test all source data.

### Using DBT Copilot to Generate Tests
- First, ensure copilot is enabled in account settings.
- The 'Generic tests' feature will create a custom, formatted YML file for the specific model that is open when you click the button. The AI will analyze the model and include generic tests it deems appropriate in the file. **Be sure to check its work before committing changes and pushing to a production environment**.

## Documentation Basics
- Documentation is configured in the same YML files as your sources, models, and tests. Documentation helps streamline the development workflow by making data easily understandable to anyone who needs to use it. DBT can also make automatically make a catalog out of your documentation using the YML file.
- The `description` property can be used at the source, model, table, and column level to describe the significance of the entity within the context of the project and/or business.
- Example YML:
  ```
  models:
    - name: stg_jaffle_shop__customers
      description: The grain of this table is one unique customer per row.
      columns:
        - name: customer_id
          description: Primary key for the customers table.
  ```
- Doc blocks are used in place of the `description` property when the description of a source, model, or column is too complex to fit into one or two sentences. These doc blocks are created in markdown files. For example:
  ```
  {% docs order_status %}
  One of the following values:

  | status         | definition                                              |
  |----------------|---------------------------------------------------------|
  | placed         | Order placed, but not shipped yet.                      |
  | shipped        | Order shipped, but not delivered.                       |
  | completed      | Order received by customers.                            |
  | return_pending | Customer indicated they would like to return this item. |
  | returned       | Item returned.                                          |

  {% enddocs %}
  ```
  - The doc block is then referenced in the YML file under the `order_status` column as follows: `description: {{ doc('order_status') }}`.
- As with generating tests, DBT copilot can be used to automatically generate documentation for the specific model that is open by using the 'Documentation' feature. **Be sure to check its work before committing changes and pushing to a production environment**. You can also use the `dbt docs generate` command.

## Deployment
- A deployment in DBT involves running DBT commands (such as `dbt build`) on a schedule so that they are executed on a regular schedule without human intervention. Deployment also involves building all of the models into a production schema that is separate from your personal development schema.
- This separation of schemas allows developers to work on features and bug fixes without interrupting production services used by analysts and business leaders.
- When deploying, DBT uses the `main` branch to build models, which is why your code needs to be merged before being pushed to production. DBT defaults to the `main` branch unless you specify a custom branch in your deployment/production environment.
- To schedule a deployment in DBT, you must first setup the deployment/production environment with the appropriate connection to the data warehouse. Next, you must create a deployment job within the deployment environment.
- **Deployments should use a separate data warehouse account and schema than the one used for development purposes**.
- Commands to run during the job can be added in Execution Settings and the schedule by which to run the job can be configured in Triggers. Jobs can be run based on a schedule or based on the completion of another job.
- During each deployment, the DBT Catalog will be automatically updated. The catalog is a good place to debug and check performance as it offers features such as a unique DAG for each column of each table, performance stats, and the status of recent builds/runs.
- The catalog also offers recommendations such as adding tests or documentation to a column. These recommendations are ranked from low to high based on severity.

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
  - This type of materialization isn't built directly into the database. Instead, DBT will interpolate the code from an ephemeral model into its dependent models using a CTE. You can assign an alias to this CTE, but DBT will always prefix it with the identifier `__dbt__cte__`.
  - If a model's materialization is switched from a table or a view to ephemeral, that table or view won't automatically be dropped when the model is materialized as ephemeral.
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
- Referencing models using the `ref` macro as shown above helps maintain modularity in your DBT project and allows your DAG to clearly show how your models relate to one another.

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