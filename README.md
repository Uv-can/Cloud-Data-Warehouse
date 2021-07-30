# Project Cloud Datawarehouse

## Project description

The data is from a new music streaming startup with a growing user base and song database.

Their user activity and songs metadata data resides in json files in S3. The goal of the current project is to build an ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights in what songs their users are listening to. 

## How to run

1. To run this project you will need to fill the following information, and save it as *dwh.cfg* in the project root folder.

```
[CLUSTER]
HOST=''
DB_NAME=''
DB_USER=''
DB_PASSWORD=''
DB_PORT=5439

[IAM_ROLE]
ARN=

[S3]
LOG_DATA='-----S3 location-----log_data'
LOG_JSONPATH='-----S3 JSON Pathlog-----json_path.json'
SONG_DATA='------S3 location-----song_data'

[AWS]
KEY=
SECRET=

[DWH]
DWH_CLUSTER_TYPE       = multi-node
DWH_NUM_NODES          = 4
DWH_NODE_TYPE          = dc2.large
DWH_CLUSTER_IDENTIFIER = 
DWH_DB                 = 
DWH_DB_USER            = 
DWH_DB_PASSWORD        = 
DWH_PORT               = 5439
DWH_IAM_ROLE_NAME      = 
```

2. Create a python environment with the dependencies listed on *requirements.txt*
3. Run the *create_cluster* script to set up the needed infrastructure for this project.

    `$ python create_cluster.py`

4. Run the *create_tables* script to set up the database staging and analytical tables

    `$ python create_tables.py`

5. Finally, run the *etl* script to extract data from the files in S3, stage it in redshift, and finally store it in the dimensional tables.

    `$ python etl.py`


## Database schema design
State and justify your database schema design and ETL pipeline.

#### Staging Tables
- staging_events
- staging_songs

####  Fact Table
- songplays - records in event data associated with song plays i.e. records with page NextSong - 
*songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

#### Dimension Tables
- users - users in the app - 
*user_id, first_name, last_name, gender, level*
- songs - songs in music database - 
*song_id, title, artist_id, year, duration*
- artists - artists in music database - 
*artist_id, name, location, lattitude, longitude*
- time - timestamps of records in songplays broken down into specific units - 
*start_time, hour, day, week, month, year, weekday*


## Queries and Results

Number of rows in each table:

| Table            | rows  |
|---               | --:   |
| staging_events   | 8056  |
| staging_songs    | 14896 |
| artists          | 10025 |
| songplays        | 333   |
| songs            | 14896 |
| time             |  8023 |
| users            |  105  |


### Steps followed on this project

1. Create Table Schemas

2. Build ETL Pipeline

3. Document Process
