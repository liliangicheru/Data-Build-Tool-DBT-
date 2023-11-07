# Data-Build-Tool-DBT-
Project to copy the data using SQL to a local PostgreSQL database, move the data from your local database to Snowflake, perform data transformation with DBT (data build tool), and use your preferred data visualization tool to create a report and dashboard.

**Data Build Tool (DBT)**

**Introduction**

Data Build Tool is an open-source command-line tool and modeling framework for data transformation and analytics. Allows you to establish macros and integrate other functions outside of SQL's capabilities for advanced use cases. DBT makes data engineering activities accessible to people with data analyst skills to transform the data in the warehouse using simple select statements, effectively creating your entire transformation process with code. With DBT, anyone who knows how to write SQL SELECT statements has the power to build models, write tests, and schedule jobs to produce reliable, actionable datasets for analytics.

**Data**

The first step is t download the dataset from the link below. (https://www.kaggle.com/datasets/mbaabuharun/craigslist-vehicles)
```python
import pandas as pd

# Download the dataset (replace with the actual data source).
data = pd.read_csv('/kaggle/input/craigslist-vehicles/Craigslist Vehicles .csv')

```

T**he copy the data to local PostgreSQL database.**

You can use the commands below.

```python

# Use psycopg2 to connect to your local PostgreSQL database.
import psycopg2

# Replace with your database credentials.
db_config = {
    "user": "your_user",
    "password": "your_password",
    "host": "localhost",
    "port": "5432",
    "database": "your_db",
}

# Create a connection to the PostgreSQL database.
conn = psycopg2.connect(**db_config)

# Assuming 'your_table' is the name of the table you want to create.
data.to_sql('your_table', conn, if_exists='replace', index=False)

# Close the database connection.
conn.close()

```

**Move data to Snowflake.**

```python
COPY INTO your_snowflake_table
FROM (
  SELECT *
  FROM your_local_postgres_table
)
FILE_FORMAT = (TYPE = 'CSV' SKIP_HEADER = 1)
CREDENTIALS = (AWS_KEY_ID = 'your_aws_key_id' AWS_SECRET_KEY = 'your_aws_secret_key')
ON_ERROR = CONTINUE;

```
After moving data ypy can perform data transformation and make sure you set up your DBT project and define the required model.

Use your data visualization and reporting tools to present your data. Use your preferred data visualization tool to connect to Snowflake and create reports and dashboards, in my case I used Power BI. 

Power BI provides a wide range of visualization options. You can create interactive reports by adding various visualizations such as charts, tables, maps, and more.

•	Open Power BI Desktop.

•	Click on "Get Data" and select "Snowflake" from the list of data sources.

•	Provide your Snowflake connection details, including server, database, username, and password.

•	Use the Power Query Editor to define SQL queries to extract the data.


•	Drag and drop fields from your dataset onto the canvas to create visuals.

•	Customize visuals by formatting, applying filters, and setting interactions between visuals.

Once your reports and dashboards are ready, you can publish them to the Power BI service to share with others.


