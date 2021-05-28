# Project: Data Modeling with Cassandra
In order to understand user preferences for Sparkify, collected data from their streaming app were modeled with Apache Cassandra. It was created 3 Tables: 

- **song_library** The PRIMARY KEY in the table consists of two fields sessionId (Partition key) and itemInSession (Clustering key). Partitioning is done by **sessionId**. Withing that partition the rows are ordered by the **itemInSession**. 
- **song_playlist_session** The PRIMARY KEY in the table consists of composite partition keys (**userId** and **sessionId**), and Clustering key **itemInSession**. Partitioning is done by **userId** and **sessionId**. Withing the partition rows are ordered by **itemInSession**.
- **songs_by_users** The PRIMARY KEY in the table consists of two fields song (Partition key) and userId (Clustering key). Partitioning is done by **song**. Withing that partition the rows are ordered by the **userId** 

In order to answer the following questions:

1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4
2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
3. Give me every username (first and last) in my music app history who listened to the song 'All Hands Against His Own'

The corresponding queries:

```
query = "select artist, song, length from song_library WHERE sessionId=338 AND itemInSession=4"
```

```
query = "select userId, sessionId, firstName, lastName, itemInSession, artist, song from song_user_history WHERE userId=10 AND sessionId=182"
```

```
query = "select song, firstName, lastName, artist from songs_by_users WHERE song='All Hands Against His Own' " 
```

# How to run the ETL

Run all cells in the `Project_1B_ETL.ipynb` file. It is assumed that Apache Cassandra is already installed and the `$ nodetool status` shows *Active* status.