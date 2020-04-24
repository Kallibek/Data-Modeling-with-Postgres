# Data Modeling with Postgres
by Kallibek Kazbekov

---
# Project summary
## Purpose
The Sparkify startup wants to analyze popularity of songs (based on user activity), streamed via thier new app. For this purpose they have two datasets, 1) logs of user activity and 2) metadata of songs. Both datasets are in JSON format. They want their data engineer to create a database and ETL pipeline using Python and PostgreSQL for analysis.  
## Database Schema
The developed database consists of four dimension tables and a fact table:

<img src="https://github.com/Kallibek/Data-Modeling-with-Postgres/blob/master/supplementary/database_schema.png" alt="alt text" width=800>

## ETL pipeline

1. Rows of `song_id`,`title`,`artist_id`,`year`,`duration` columns of each of the song data in `data/song_data` directory was read, and inserted into a `songs` table. The same procedure was repeated for `artists` table for columns `artist_id`,`artist_name`,`artist_location`,`artist_latitude`,`artist_longitude`.

1. inserting into the `time` table:
the "ts" (in milliseconds) column of each log file in `data/log_data` directory was used to extract  `hour`,`day`,`week_of_year`,`month`,`year`,`weekday` of song playings. Then these time variables were inserted to the `time` table.

1. inserting into the `users` table:
The columns `userId`, `firstName`, `lastName`, `gender`, `level`, were extracted for the log files of the `data/log_data` directory and inserted into the `users` table.

1.  inserting into the `songplays` table:
The `song_id` and `artist_id` of streamed songs were identified by joing `songs` and `artists` tables on `artist_id`, and from this joined table, `song_id` and `artist_id` was found using matching `song_name`, `artist_name` and `duration` columns. The `songplay_id`, `start_time`, `user_id`, `level`, `song_id`, `artist_id`,`session_id`,`location` columns of each log file were inserted into the `songplays` table.
---
# Project instructions on how to run the Python scripts

1. `create_tables.py` should be executed first, since it deletes and recreates the tables;
1. Then `etl.py` script reads data from log files and metadata, to insert extracted data into created tables.

# An explanation of the files in the repository

### `create_tables.py`
Includes functions to 1) delete & creat the sparkify database, 2) connect to the database, 3) remove all tables, 3) create new tables, and 4) close the connection;
```python
    def main():
        """
        - Drops (if exists) and Creates the sparkify database. 

        - Establishes connection with the sparkify database and gets
        cursor to it.  

        - Drops all the tables.  

        - Creates all tables needed. 

        - Finally, closes the connection. 
        """
    def create_database():
        """
        - Creates and connects to the sparkifydb
        - Returns the connection and cursor to sparkifydb
        """
    def drop_tables(cur, conn):
        """
        Drops each table using the queries in `drop_table_queries` list.
        """
    def create_tables(cur, conn):
        """
        Creates each table using the queries in `create_table_queries` list. 
        """
 ```

### `etl.py` 
Has functions to read log files and metadata and insert the extracted data into the tables.
```python
def main():
    """
    - Establishes connection with the sparkify database and gets
    cursor to it;
    
    - Processes song files;
    
    - Processes log files.
    """
def process_song_file(cur, filepath):
    """
    A function to process song file and intest data to the songs table.
    """
def process_log_file(cur, filepath):
    """
    A function to process log file and intest data to the time, users and songplays tables.
    """
def process_data(cur, conn, filepath, func):
    """
    A function to process a specified file type (song vs. log files)
    """
```

### `sql_queries.py`
contains SQL queries to drop and create tables, as well as to find specific song data;

### `test.ipynb`
Used to validate the ETL pipeline. 5 rows of the resulting tables can be viewed;
### `supplementary` directory
Directory for any supplementary data used in `README.md`.
