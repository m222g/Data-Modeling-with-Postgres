## Project Description
The purpose of this database is so Sparkify's analytics team see what songs users are listening to. This database schema and ETL pipeline presents them with exactly what they are looking for. 

## How to run the Python scripts:
1. Connect to the terminal
2. Enter the following:
>For *create_tables.py*:
>>- python create_tables.py
>For *etl.py*:
>>- python etl.py

## Files in the Repository:
#### data/log_data
This is a dataset that contains activity log files in JSON format.

#### data/song_data
This is a dataset that contains song data files in JSON format.

#### etl.ipynb
This Jupyter Notebook is used to read and process a single file from log_data and song_data to work through and test the ETL process.

#### test.ipynb
This Jupyter Notebook is used to confirm the ETL pipeline works and to run sanity tests.

#### create_tables.py
This Python script is used to drop and create the tables before running the ETL scripts. 

#### etl.py
This Python script reads and processes the files from log_data and song_data to load into the tables. 

#### sql_queries.py
This Python script contains all of the SQL queries used to create and drop tables, insert data into the tables, and query a song and artist from provided data. 

## Database Schema and ETL Pipeline
#### I used a star schema:
**Fact Table**
1. songplays - records in log data associated with song plays
- *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

**Dimension Tables**
2. users - users in the app
- *user_id, first_name, last_name, gender, level*
3. songs - songs in music database
- *song_id, title, artist_id, year, duration*
4. artists - artists in music database
- *artist_id, name, location, latitude, longitude*
5. time - timestamps of records in songplays broken down into specific units
- *start_time, hour, day, week, month, year, weekday*

#### ETL Pipeline:
##### Populates the database from the song and log data files
**Extract:**
- Extract the data for the songs and artists tables from song_data. 
- Extract the data for the time and users table from log_data.
- Extract the data for the songplays table from log_data as well as the artists and songs tables.

**Transform:**
- Ensure the data matches the database types
- Example:
>>t = pd.to_datetime(df['ts'], unit='ms')
This converted the timestamp to datetime so it could be processed correctly.

**Load:**
- The dimension tables: users, songs, artists, and time were inserted and populated first
- The fact table songplays, was inserted and populated last because the songs and artists dimension tables were required to populate it



