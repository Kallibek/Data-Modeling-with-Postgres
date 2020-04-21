# Project name: Data Modeling with Postgres
# Author: Kallibek Kazbekov
# Date: 4/20/2020
###########################################
# First step: create_tables.py

# This file has SQL commnands to create tables, insert rows and search.
# the search statement  first joind songs and artists tables on artist id and 
# finds a song_id and artist_id by song_name, artist_name, and duration of a songs

###########################################
# Second step: ETL pipeline

# 1. This part starts from a connection to created database.

# 2. Then rows of specific columns ("song_id","title","artist_id","year","duration") 
# of each of the song data in "data/song_data" directory was read, and 
# inserted into a "songs" collection of a database.

# The same procedure was repeated for artists collections
# for columns:"artist_id","artist_name","artist_location","artist_latitude","artist_longitude"

# 3. inserting into the 'time' collection:
# the "ts" (in milliseconds) column of each log file in
# "data/log_data" directory was used to extract 
# "hour","day","week_of_year","month","year","weekday" of song playings.
# Then these time variables were inserted to the "time" collection.

# 4. inserting into the 'users' collection:
# The following columns, "userId", "firstName", "lastName", "gender", 
# "level", were extracted for the log files of the "data/log_data" 
# directory and inserted into the 'users' collection.

# 5.  inserting into the 'songplays' collection:
# the song_id and artist_id was song_playing was identified by
# joing songs and artists collections by artist_id,
# and from this joined table, song_id and artist_id was found using matching song_name, artist_name and duration of songs.

# The "songplay_id", "start_time", "user_id", "level", "song_id", 
# "artist_id","session_id","location" columns of each log file were inserted into the songplay collection