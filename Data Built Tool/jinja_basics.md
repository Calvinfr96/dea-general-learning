# Jinja Basics

## Introduction
- Jinja is a python-based templating language that allows incorporating functional aspects of programming into SQL code. This enables better collaboration and more concise and performant SQL code.
- Basic Syntax:
  - `{% %}` is used for statements. These perform any function programming such as setting a variable or starting a for loop.
  - `{{ }}` is used for expressions. These will print text to the rendered file. In most cases in dbt, this will compile your Jinja to pure SQL.
  - `{# #}` is used for comments. This allows us to document our code inline. This will not be rendered in the pure SQL that you create when you run dbt compile or dbt run.
- Setting a Variable:
  - `{% set temperature = 80.0 %}`
- If Statements:
  ```
  {% if temperature > 70 %}
  # refreshing lemon sorbet

  {% else %}
  #d decadent chocolate cake

  (% endif %)
  ```
- For Loops:
  ```
  {% for j in range(26) %}
    select {{ j }} as number {% if not loop.last %} union all {% endif %}
  {% endfor %}
  ```
  - Creates a select statement ending in `union all` for all except the last iteration.
  - Has the effect of creating a `number` column with numbers from 0 to 25.
- Interacting With Lists and/or Dictionaries
  ```
  {% set cool_string = 'Wow, cool beans!' %} # Sets the variable. This code is not visible to the end user.
  {% set my_second_cool_string = 'This is Jinja!' %}
  {% set my_fav_num = 26 %}

  {{ cool_string }} # Prints the variable. The variable's value is visible to the end user.
  {{ cool_string }} {{ my_second_cool_string }} I want to write Jinja for {{ my_fav_num }} years! # Example of string interpolation using variables. No special method is needed.

  {% set animals = ['lemur', 'dingo', 'rhino', 'dog'] %}
  {{ animals[0] }} # Prints the first value in the animals list.

  {% for animal in animals %}
    my favorite animal is {{ animal }} # Prints the sentence for each animal in the list.
  {% endfor %}
  ```
- Combining For Loops With If Statements:
  ```
  {% set animals = ['radish', 'cucumber', 'chicken nugget', 'avocado'] %}

  {% for animal in animals %}
    {% if animal == 'chicken nugget' %}
      {% set food_type = 'snack' %}
    {% else %}
      {% set food_type = 'vegetable' %}
    {% endif %}

    The delicious (( food )) is my favorite {{ food_type }}.
  {% endfor %}

  {% set jeans_directory = {
      'word': 'data',
      'part_of_speech': 'noun',
      'definition': 'The building block of life'
  } %}

  {{ jeans_directory['word']}} ({{ jeans_directory['part_of_speecch'] }}): defined as "{{ jeans_directory['definition']}}" # Prints 'data (noun): defined as "The building block of life."'.
  ```
- Pivot With Jinja:
```
with payments as (
  select *
  form {{ ref('stg_payments' )}}
  where status = success
),
pivoted as (
  select
    {%- set payment_methods = ['bank_transfer', 'credit_card', 'coupon', 'gift_card'] -%}
    order_id,
    {% for method in payment_methods %}
      sum(case when payment_method == '{{ method }}' then amount else 0 end) as {{ method }}_amount
      {%- if not loop.last -%}
        ,
      {%- endif -%}
    {% endfor %}
  from payments
  group by order_id
)

select * from pivoted
```
The `%-` and `-%` remove the whitespace before and after the expression.

## Macros
- Like functions/methods in any programming language, macros in jinja allow you to write generic logic that can be reused throughout a project.
- Packages allow you to import macros created by other developers and use them in your project.
- In DBT, macros should be created and written as SQL files in the `macros` folder of your project.
- Example Macro:
  ```
  {% macro cents_to_dollars(column_name, decimals = 2) %}
    ROUND({{ column_name }} / 100, {{ decimals }})
  {% endmacro %}
  ```
  - This macro divides the values in the `amount` column by 100. To reference the model in a SQL query, you would use the following syntax: `{{ cents_to_dollars("amount") }}`.
  - `decimals = 2` acts as a parameter with a default value. This means if the variable is omitted when the macro is called, it's value will automatically be set to two.
- Macro Documentation:
  - Documentation can be specified for macros in a `macros.yml` file within the `macros` folder of your project, as follows:
    ```
    macros:
      - name: cents_to_dollars
        description: A macro that converts dollars to cents and rounds to the provided number of decimal places. If no amount is specified for decimal places, the number will be rounded to two by default.
        arguments:
          - name: column_name
            type: string
            description: The name of the column you want to convert.
          - name: decimals
            type: integer
            description: number of decimal places to which the result should be rounded. Defaults to two.
    ```

## Packages
- Packages allow you to import models and macros from outside sources into your DBT project.
- Common packages can be found at https://hub.getdbt.com/. Packages can also be imported from github.
- Packages are installed and configured in a DBT project using the `packages.yml` file. For example, the following snippet is used to install the `dbt_utils` package:
  ```
  packages:
    - package: dbt-labs/dbt_utils
      version: 1.3.3
    - git: https://github.com/dbt-labs/dbt-codegen.git
      revision: main
    - local: sub_project
  ```
  - Packages can be installed here using the DBT package name from the DBT hub website, or they can be installed using the HTTPS link from the github repo (assuming you have access).
  - When installing using `package`, you specify the package name and version.
  - When installing using `git`, you provide the HTTPS repo link and the name of the branch.
  - When installing using `local`, you provide the relative path of the project.
  - Once the `packages.yml` file is updated, run `dbt deps` to verify the dependencies are installed correctly.
- Example Usage of Imported Macro:
  ```
  {{ dbt_utils.date_spine(
      datepart="day",
      start_date="cast('2019-01-01' as date)",
      end_date="cast('2020-01-01' as date)"
    )
  }}
  ```

## Advanced Jinja and Macros
- `grant_select` Macro:
  ```
  {% macro grant_select(schema = target.schema, role = target.role) %}
      {% set sql %}
          grant usage on {{ schema }} to role {{ role }};
          grant select on all tables in schema {{ schema }} to role {{ role }};
          grant select on all views in schema {{ schema }} to role {{ role }};
      (% endset %)

      {{ log('Granting select on all tables and views in schema' ~ target.schema ~ 'to role' ~ role, info = true) }}
      {% do run_query(sql)%}
      {{ log('Permissions granted', info = true) }}
  {% endmacro %}
  ```
  - The `dbt run --operation grant_select` can be used to run this macro independently.
    - If we wanted add arguments to the command, we would do so with `-- args '{'paramter': 'value'}'`
  - The `~` character in the log statement is used for string concatenation.
  - `info = true` as the second argument in the `log` macro ensures the log is printed in the terminal output, instead of just the rich logs.
- Instead of configuring the schema, DBT should write to the default schema when building/running models within the connection settings of your profile, you can configure the schema at the folder level within the `dbt_project.yml` file:
  ```
  models:
    project_name:
      folder_name:
        +schema: schema_name
  ```
- This can also be done with a `config` block within a specific model:
  ```
  {{
    config(
      schema = 'schema_name'
    )
  }}
  ```
  - This overrides the schema setting from the `dbt_project.yml` file.
- The `run_query` macro is used in dbt to run SQL queries against the warehouse and return the results, which can then be used within Jinja for further processing.
- The `log` function is used to output messages during the execution of a dbt macro. This is helpful for debugging and understanding the flow of execution within a macro.
- The `target.schema` variable is used to reference the default schema in a dbt project, making it easy to dynamically set the schema when granting permissions or performing other operations in macros.
- The `execute` variable in Jinja is used to check if dbt is in execute mode, which is necessary for running SQL queries during certain stages of the dbt run process. If `execute` is `True`, it means SQL queries can be executed.