# ETL Operations on Country-GDP Data

This project demonstrates an **ETL (Extract, Transform, Load)** pipeline to fetch, process, and store data on the largest banks in the world based on market capitalization. The pipeline extracts data from a webpage, transforms it by adding exchange rate conversions, and finally loads the transformed data into both a CSV file and a database.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Technologies Used](#technologies-used)
3. [Setup Instructions](#setup-instructions)
4. [ETL Pipeline Stages](#etl-pipeline-stages)
    - [Extraction](#1-extraction)
    - [Transformation](#2-transformation)
    - [Loading](#3-loading)
5. [Query Execution](#query-execution)
6. [Logging](#logging)
7. [Usage](#usage)
8. [Conclusion](#conclusion)

## Project Overview

This project focuses on performing ETL operations on **Country-GDP data** by following these steps:

- **Extraction**: Scrapes a webpage for data on the market capitalization of the largest banks.
- **Transformation**: Adds new columns to convert the market capitalization from USD to GBP, EUR, and INR using exchange rates.
- **Loading**: Stores the transformed data in both a CSV file and a SQLite database.

## Technologies Used

- **Python 3.x**
- **Pandas** for data manipulation.
- **BeautifulSoup** for web scraping.
- **SQLite** for database operations.
- **Requests** for HTTP requests.

## Setup Instructions

1. Clone the repository:
    ```bash
    git clone <repository_url>
    cd <repository_directory>
    ```

2. Install the required dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3. Ensure that the `exchange_rate.csv` file is present in the project directory with the following format:
    ```
    Currency,Rate
    GBP,0.74
    EUR,0.85
    INR,74.58
    ```

4. You will also need a SQLite database. This project creates one automatically when executed.

## ETL Pipeline Stages

### 1. Extraction

The `extract()` function scrapes the list of largest banks by market capitalization from a Wikipedia webpage. It parses the page using **BeautifulSoup** and stores the relevant data in a Pandas DataFrame.

```python
df = extract(url, table_attribs)
```
### 2. Transformation
The transform() function adds three new columns to the DataFrame, converting the market capitalization from USD to GBP, EUR, and INR using exchange rates from a provided CSV file.

```python
df = transform(df, csv_path)
```

### 3. Loading
CSV Loading: The load_to_csv() function saves the transformed DataFrame to a CSV file.

```python
load_to_csv(df, output_path)
Database Loading: The load_to_db() function stores the transformed data in a SQLite database table.
```

```python
load_to_db(df, sql_connection, table_name)
```

### Query Execution
After loading the data into the SQLite database, the project runs some predefined SQL queries using the run_query() function. Example queries include fetching all records, calculating the average market cap in GBP, and retrieving the names of the first five banks.

```python
query_statement = f"SELECT * from {table_name}"
run_query(query_statement, sql_connection)
```

### Logging
The project implements logging for each key stage of the ETL process. The log_progress() function logs messages with timestamps to a code_log.txt file.

```python
log_progress('Data extraction complete.')
```

### Usage
Run the script to execute the entire ETL process:

```bash
python etl_script.py
```
The logs will be saved in code_log.txt, the transformed data in Largest_banks_data.csv, and the database in Banks.db.

### Conclusion
This ETL pipeline project is a simple demonstration of how to extract data from the web, transform it by adding new features, and load the result into both CSV and database formats. The logging and query execution steps help in monitoring and analyzing the entire pipeline.