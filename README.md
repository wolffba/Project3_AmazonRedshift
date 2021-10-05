Udacity Data Engineering Nanodegree - Project 3 Cloud Data Warehouses

For this project in we are utilizing Amazon Redshift to create a data warehouse from data files saved on S3 buckets in the cloud. The data in the S3 buckets were from a subset of data from the "Million Song Dataset" along with an application event similator (see github page for a description: https://github.com/Interana/eventsim) for users that download songs from the music database.

The goal was to create an AWS user and role that possessed permissions to create database clusters in Redshift and read data stored in S3 buckets. Once the clusters were created, the raw data should be loaded to staging tables, then transformed to a more efficient table schema (in this case a star schema). After the star schema is created then queries can be made on the data - in this case just total counts of songs, users, songplays, times, and artists.


The star schema was as follows:
A central fact table called "songplays_fact": This table has all of the relevant event data associated with song plays.

Attached the fact table were 4 dimension tables:

"user_dim" - user information  (user_id, first_name, last_name, gender, level)

"songs_dim" - song information in music database (song_id, title, artist_id, year, duration)

"artist_dim" - artist information in music database artist_id, name, location, lattitude, longitude

"time_dim" - timestamps of records in songplays (start_time, hour, day, week, month, year, weekday)


Files used for this project:

S3 buckets located in the cloud:
Similated log data (json files) = 's3://udacity-dend/log_data'
Labels of th json log data files = 's3://udacity-dend/log_json_path.json'
Subset of data from Million Song Dataset = 's3://udacity-dend/song_data'

dwh.cfg:
This file stores the configuration needed to log into AWS, create users/roles using IAM, and create Redshift Clusters

sql_queries.py:
This file contains all of the code for creating tables, and inserting data into tables in postgreSQL.

create_tables.py:
This file imports queries from sql_queries.py and connects to postrgreSQL to create tables

etl.py:
This file extracts the raw data in S3, transforms the data by importing in the created tables, and the loads the data into Amazon Redshift.

redshift.test.ipynb:
This is a notebook that goes through all of the steps of configuring the Amazon account (logging in, connecting to the region of choice, assigning roles), creating an Amazon Redshift cluster, and then testing if data loaded by doing some queries on the cluster.
# Project3_AmazonRedshift
