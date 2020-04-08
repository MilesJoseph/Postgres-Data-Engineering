
## Sparkify Postgres ETL

This submission is for the first project of the Data Engineering Nanodegree on Udacity. This project has included

* Data Modeling with Postgres
* Star Schema
* ETL

Snyopsis

A startup called Sparkify wants to analyze the data they have been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

We have been tasked with creating a database schema and ETL pipeline for analysis.

All data pertaining to the songs are in json files within subdirectories under /data/song_data.

The log data or transactional data is included in log datasets. These are also nested and included in /data/log_data.

## Database Schema

In this first section we learned about Postgres and under which circumstances Postgres and SQL data would be most appropriate. Some of the reasons we know that this is an appropriate situation for sql is that;

* The data types are structured.
* Small data
* SQL is robust enough
* We can model the data using a star schema.

Now that we have contextualized the problem and the question being asked we can display the tables themselves;

## Fact Table

songplays
* songplay_id (INT) PRIMARY KEY (which implies not null and distinct)
* start_time (DATE) NOT NULL (beginning of activity for user in question)
* user_id (INT) NOT NULL (this is the user id, or person playing the song)
* level (TEXT) (indicates whether a user is using paid service or not)
* song_id (TEXT) NOT NULL (Song)
* artist_id (TEXT) NOT NULL (ID of artist of song)
* session_id (INT) (id of the user session)
* location (Text) (geographical user location)
* user_agent(TEXT) (agent used by user to acess sparkify)

To remember, there is only one fact table, the rest are dimension tables.

## Dimension Tables

users
* user_id (INT) PRIMARY KEY (id of the user)
* first_name (TEXT) NOT NULL (name of the user)
* last_name (TEXT) NOT NULL (Last name)
* gender (TEXT) (M,F)
* level (TEXT) (paid, free)

songs
* song_id (TEXT) PRIMARY KEY (id of song)
* title (TEXT) NOT NULL (title)
* artist_id (TEXT) NOT NULL (id of song artist)
* year (INT) (year of song release)
* duration (FLOAT) NOT NULL (ms)

artists
* arist_id(TEXT) PRIMARY KEY (id of artist)
* name (TEXT) NOT NULL (name of artist)
* location (TEXT) (name of the artist's city)
* latitude (FLOAT)
* longitude (FLOAT)

time
* start_time (DATE) PRIMARY KEY
* hour (INT)
* day (INT)
* week(INT)
* month (INT)
* year (INT)
* weekday (TEXT)

## Provided Files
* The data has been provided for us in nested json files.
* sql_queries.py contains the framework for creating the tables in our database.
* create_tables.py drops and creates table, we can run this each time before running our etl script to clear duplicates, etc.
* test.ipynb, here we can test our ETL work
* etl.ipynb processes a single file and loads.
* etl.py reads and processes all files and loads.
* read.me this is where I have outlined the stepds.

I took the following steps to complete the pipeline

* I wrote all of the sql required in sql_queries.py to inititate drop and create tables from create_tables.py
* I completed the create tables script provided.
* I ran the create tables in test to make sure that they worked.
* I completed the etl.ipynb notebook for creating pipeline.
* I verified in test are that the records were coming through correctly from the etl.ipynb
* Using etl.py I made sure that the connection was working. I also defined data to be inserted by their column names for each row in the respective dataframe, songs, artists, time, etc.
* Then we define how we will insert the data from the json files into the database.
* Next, we loaded the data into our user table.
* Next, we use the song_select query for selecting data to insert into our songplay table and finally we insert all data into this fact table.
