# Data Modeling Interview Guidance

## Interview Process
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

## Universal Data Modeling Interview Questions
Below is a list of questions you should ask the interviewer before getting started answering the question and solving the problem:
- Clarify The Business Context:
  - What is the main goal or business problem we’re trying to solve?
  - Who are the end users of this data or metric?
  - How will this data product be used in decision-making?
  - Is this focused on reporting, analytics, or product feature support?
- Define The Metric or Entity:
  - What exactly do we mean by [X metric or entity]?
  - How do we know when an event is considered complete / valid / successful?
  - Are there different versions or interpretations of this metric in the company?
  - Should we count all events or only a subset (e.g., active users, paid users, confirmed transactions)?
- Timeframe & Granularity:
  - Over what time window should this be tracked (daily, weekly, monthly, real-time)?
  - Do we need historical tracking or just the current state?
  - What level of granularity is expected (user, session, event, product, region)?
- Scope & Edge Cases:
  - Are there filters or exclusions we should apply (e.g., test accounts, canceled orders)?
  - How do we handle duplicates, missing data, or errors?
  - Should we track partial progress or only final outcomes?
  - Are there special cases (refunds, retries, multiple devices, timezone differences)?
- Data Sources & Ownership:
  - Which systems or tables contain the relevant data?
  - Are there trusted source-of-truth tables for this entity/metric?
  - Is data generated internally or do we rely on external integrations?
  - Who is the owner/stakeholder for this data if clarification is needed?
- Dimensions & Breakdowns:
  - Should this be segmented by region, platform, product type, customer type?
  - Do we need to support drill-downs (e.g., country → state → city)?
  - Should metrics be attributed to specific dimensions (e.g., revenue by acquisition channel)?
- Frequency & Freshness:
  - How frequently does this need to be updated (real-time, hourly, daily)?
  - What is the acceptable latency for data availability?
  - Do we need to track late-arriving data or updates to past records?
- Outputs & Deliverables:
  - What should the final output look like (dashboard, report, data mart, metric definition)?
  - Who is the consumer — data scientists, executives, operations teams?
  - Should we support ad-hoc queries or just predefined metrics?
- Validation & Success Criteria:
  - How will we validate correctness of the metric or model?
  - Do we have an existing baseline to compare against?
  - What would be considered a wrong or misleading definition?
- Long-Term Considerations:
  - Will this metric need to scale to larger datasets in the future?
  - Do we need to design for historical backfills?
  - Should we anticipate schema changes or versioning of definitions?

## Generic Delivery Company Example Problem
There is a delivery company with customers who place orders at restaurants for pick up or delivery. Once the restaurant receives the order, they can choose to accept or deny the order. If accepted, the restaurant is connected with a nearby delivery driver picks up the order and delivers it to the customer. Design a schema that takes the entire process into account.

- Entities Involved:
  - Restaurant
  - Customer
  - Order
  - Delivery Driver
- Dimension Tables:
  - dim_restaurants
    - Restaurant_id
    - Restaurant_Name
    - Region_Id
    - (Other Relevant Demographic_info_cols)
    - Account_creation_date - life of the restaurant
    - Number_of_orders
    - L7_ Number of_ orders (last 7 days)
    - L28_ Number of_ orders (last 28 days)
    - Menu_items (a json)
    - Opening_Hour
    - Closing_Hour
    - Food_Category (fast_food, healthy, etc)
  - dim_customers
    - Customer_id
    - Full_Name
    - Region_Id
    - (Other Relevant Demographic_info_cols, like address)
    - Account_creation_date - life of the customer
    - Last_login_date
    - Number_of_orders
    - L7_ Number of_ orders (last 7 days)
    - L28_ Number of_ orders (last 28 days)
    - Premium_user (Y or N)
    - Premium_user_start_date (Y or N)
  - dim_orders - This table represents one transaction, with all relevant entities involved and can manly be used for performing joins.
    - Restaurant_id
    - Order_id
    - Deliverer_id
    - Customer_id
    - Region_id
    - places_order_time
    - deliverer_accepted_time
    - deliverer_picks_up_order_time
    - deliverer_drops_off_order_time
  - dim_delivery_drivers
    - Deliverer_id
    - Full Name
    - Region_Id
    - (Other Relevant Demographic_info_cols)
    - Account_creation_date - life of the Deliverer
    - Last_login_date
    - Number_of_trips
    - L7_ Number_of_trips (last 7 days)
    - L28_ Number_of_trips (last 28 days)
- Fact Tables:
  - fact_customer_activity
    - Session_id
    - Customer _id
    - Region_id
    - Timestamp
    - Activity_type - login/update_account_info/available_to_order/places_order/Cancels_order/receives_order/rates_driver/tips_driver
  - fact_order_activity
    - Order_id
    - Deliverer_id
    - Customer_id
    - Region_id
    - Timestamp
    - Activity_type - places_order/driver_picks_up_order/driver_drops_off_order
  - fact_delivery_driver_activity
    - Session_id
    - Deliverer _id
    - Region_id
    - Timestamp
    - Activity_type - login/update_account_info/available_to_pickup/accept_order/Cancel_order/arrive_to_restaurant/picks_up_order/drops_off_order

### Explanation
- We went about figuring out which dim tables to include in the schema by looking at which entities are involved in the business flow, regardless of changes to the business. For example, if this food delivery company
decides to charge more, it won’t change the existence of objects needed to run the business, but may change some of their attributes.
- The Menu_items field in the dim_restaurants table is a JSON field, which can contain a value such as `{menu_item_ids: [123, 456, 789, 012, 345]}`. Another menu_items dim table could potentially be created based on these values.
- The fact_order_activity table was created, even though it contains redundant information that already exists in the fact_customer_activity and fact_delivery_driver_activity because the extra storage costs associated with creating this table will ultimately be lower than the compute costs of performing repetitive joins. There is also less
room for error if analysts and scientists incorrectly join columns that cause expensive queries.
- The dim_orders table is simply a "flattened out" version of the fact_order_activity table. There is no timestamp in this table since it already exists in the other related tables.

## DropBox Example Problem
Create a data model to track retention rate among DropBox users and factors affecting the churn rate.
- Step 0: Understand the business model.
- Step 1: Ask a lot clarifying questions
- Step 2: Create tables
- Step 3: Create columns
- Step 4: Create connections
- Step 5: Tie solution back to question/stated goals.

### Asking questions
When asking questions, use the strategy of asking broad questions, then increasingly narrow questions on top of those questions. **Never assume. Always clarify. Also, ask questions throughout the interview, not just the beginning.** This sort of builds a "tree" or mental map you can use to solve the problem. For example:
- What do you mean by retention rate?
  - How do you determine the retention rate?
- What kind of users are we talking about?
  - Are the users customers, employees, reviewers, etc?
    - How do retention/churn rates vary among different types of users?
      - Are you trying to study a particular user type or users in general?
- What do you mean by churn rate?
  - How do you calculate churn rate?
  - Are we talking about sign-ups, accounts, premium services, engagement, etc?
    - Are we looking at churn for a specific type of file?
      - Are these files available to all users or only certain types of users?
    - How far back do you want to look to study the churn rate?
- Are there particular, known factors you want to look at?
  - On what timescale/granularity are we looking at churn/retention? Year-over-year? Month-over-month?
    - Has there been a steady decline or a dramatic drop-off?
- What is the goal? (business value)

### Creating The Tables
- Dimension Tables:
  - dim_users
    - user_id
    - name
    - email_address
    - phone_number
    - age
  - dim_folders
    - folder_id
    - folder_type
  - dim_plan_features
    - user_id
    - feature_id
    - start_date
    - end_date
    - status
- Fact Tables:
  - fact_daily_usage
    - file_id
    - user_id
    - folder_id
    - transfer_id
    - timestamp
    - file_transfer_size