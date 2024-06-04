# SQL_Exam

insert into movies (Title, Runtime, Genre, IMDB_Score, Rating) VALUES
    -> ('Planet Of The APES', 140, 'Action' , 7.6, 'PG-13'),
    -> ('8 Mile', 110, 'Musical Drama' , 7.2, 'R');
Query OK, 2 rows affected (0.15 sec)
Records: 2  Duplicates: 0  Warnings: 0
mysql> select * from movies
    -> ;
+--------------------+---------+---------------+------------+--------+
| Title              | Runtime | Genre         | IMDB_Score | Rating |
+--------------------+---------+---------------+------------+--------+
| Howard the Duck    |     100 | Sci-Fi        |        4.6 | PG     |
| Lavalantula        |      83 | Horror        |        4.7 | TV-14  |
| Starship           |     129 | Sci-Fi        |        7.2 | PG-13  |
| Waltz With Bashir  |      90 | Documentary   |          8 | R      |
| Spaceballs         |      96 | Comedy        |        7.1 | PG     |
| Monster Inc.       |      92 | Animation     |        8.1 | G      |
| Planet Of The APES |     140 | Action        |        7.6 | PG-13  |
| 8 Mile             |     110 | Musical Drama |        7.2 | R      |
+--------------------+---------+---------------+------------+--------+
8 rows in set (0.00 sec)


mysql> select * from movies where Genre='Sci-Fi';
+-----------------+---------+--------+------------+--------+
| Title           | Runtime | Genre  | IMDB_Score | Rating |
+-----------------+---------+--------+------------+--------+
| Howard the Duck |     100 | Sci-Fi |        4.6 | PG     |
| Starship        |     129 | Sci-Fi |        7.2 | PG-13  |
+-----------------+---------+--------+------------+--------+
2 rows in set (0.01 sec)


mysql> select * from movies where IMDB_Score > 6.5;
+--------------------+---------+---------------+------------+--------+
| Title              | Runtime | Genre         | IMDB_Score | Rating |
+--------------------+---------+---------------+------------+--------+
| Starship           |     129 | Sci-Fi        |        7.2 | PG-13  |
| Waltz With Bashir  |      90 | Documentary   |          8 | R      |
| Spaceballs         |      96 | Comedy        |        7.1 | PG     |
| Monster Inc.       |      92 | Animation     |        8.1 | G      |
| Planet Of The APES |     140 | Action        |        7.6 | PG-13  |
| 8 Mile             |     110 | Musical Drama |        7.2 | R      |
+--------------------+---------+---------------+------------+--------+
6 rows in set (0.03 sec)


select AVG(Runtime) from movies;
+--------------+
| AVG(Runtime) |
+--------------+
|     105.0000 |
+--------------+
1 row in set (0.03 sec)


mysql> update movies Set Rating = 'R' where Title ='Starship';
Query OK, 1 row affected (0.07 sec)
Rows matched: 1  Changed: 1  Warnings: 0
mysql> select * from movies;
+--------------------+---------+---------------+------------+--------+
| Title              | Runtime | Genre         | IMDB_Score | Rating |
+--------------------+---------+---------------+------------+--------+
| Howard the Duck    |     100 | Sci-Fi        |        4.6 | PG     |
| Lavalantula        |      83 | Horror        |        4.7 | TV-14  |
| Starship           |     129 | Sci-Fi        |        7.2 | R      |
| Waltz With Bashir  |      90 | Documentary   |          8 | R      |
| Spaceballs         |      96 | Comedy        |        7.1 | PG     |
| Monster Inc.       |      92 | Animation     |        8.1 | G      |
| Planet Of The APES |     140 | Action        |        7.6 | PG-13  |
| 8 Mile             |     110 | Musical Drama |        7.2 | R      |
+--------------------+---------+---------------+------------+--------+
8 rows in set (0.00 sec)


mysql> select AVG(Runtime)
    -> FROM movies
    -> GROUP BY Genre;
+--------------+
| AVG(Runtime) |
+--------------+
|     114.5000 |
|      83.0000 |
|      90.0000 |
|      96.0000 |
|      92.0000 |
|     140.0000 |
|     110.0000 |
+--------------+
7 rows in set (0.05 sec)


select AVG(Runtime)
    -> from movies
    -> WHERE IMDB_Score < 7.5
    -> GROUP BY Genre;
+--------------+
| AVG(Runtime) |
+--------------+
|     114.5000 |
|      83.0000 |
|      96.0000 |
|     110.0000 |
+--------------+
4 rows in set (0.00 sec)


 Select AVG(IMDB_Score) AND MAX(IMDB_Score) AND MIN(IMDB_Score) from movies;
+---------------------------------------------------------+
| AVG(IMDB_Score) AND MAX(IMDB_Score) AND MIN(IMDB_Score) |
+---------------------------------------------------------+
|                                                       1 |
+---------------------------------------------------------+
1 row in set (0.03 sec)


 ALTER TABLE movies ADD ID int AUTO_INCREMENT PRIMARY KEY;
Query OK, 0 rows affected (1.41 sec)
Records: 0  Duplicates: 0  Warnings: 0
select * from movies
    -> ;
+--------------------+---------+---------------+------------+--------+----+
| Title              | Runtime | Genre         | IMDB_Score | Rating | ID |
+--------------------+---------+---------------+------------+--------+----+
| Howard the Duck    |     100 | Sci-Fi        |        4.6 | PG     |  1 |
| Lavalantula        |      83 | Horror        |        4.7 | TV-14  |  2 |
| Starship           |     129 | Sci-Fi        |        7.2 | R      |  3 |
| Waltz With Bashir  |      90 | Documentary   |          8 | R      |  4 |
| Spaceballs         |      96 | Comedy        |        7.1 | PG     |  5 |
| Monster Inc.       |      92 | Animation     |        8.1 | G      |  6 |
| Planet Of The APES |     140 | Action        |        7.6 | PG-13  |  7 |
| 8 Mile             |     110 | Musical Drama |        7.2 | R      |  8 |
+--------------------+---------+---------------+------------+--------+----+
8 rows in set (0.00 sec)


select ID, Rating FROM movies WHERE Genre IN ('Horror','Documentary');
+----+--------+
| ID | Rating |
+----+--------+
|  2 | TV-14  |
|  4 | R      |
+----+--------+
2 rows in set (0.00 sec)


 select * from movies WHERE (Rating ='G' OR Rating = 'PG') AND Runtime < 100;
+--------------+---------+-----------+------------+--------+----+
| Title        | Runtime | Genre     | IMDB_Score | Rating | ID |
+--------------+---------+-----------+------------+--------+----+
| Spaceballs   |      96 | Comedy    |        7.1 | PG     |  5 |
| Monster Inc. |      92 | Animation |        8.1 | G      |  6 |
+--------------+---------+-----------+------------+--------+----+
2 rows in set (0.00 sec)


Select IMDB_Score FROM movies GROUP BY IMDB_Score HAVING COUNT(*) > 1;
+------------+
| IMDB_Score |
+------------+
|        7.2 |
+------------+
1 row in set (0.01 sec)


 DELETE FROM movies where Rating ='R';
Query OK, 3 rows affected (0.07 sec)
 select * from movies;
+--------------------+---------+-----------+------------+--------+----+
| Title              | Runtime | Genre     | IMDB_Score | Rating | ID |
+--------------------+---------+-----------+------------+--------+----+
| Howard the Duck    |     100 | Sci-Fi    |        4.6 | PG     |  1 |
| Lavalantula        |      83 | Horror    |        4.7 | TV-14  |  2 |
| Spaceballs         |      96 | Comedy    |        7.1 | PG     |  5 |
| Monster Inc.       |      92 | Animation |        8.1 | G      |  6 |
| Planet Of The APES |     140 | Action    |        7.6 | PG-13  |  7 |
+--------------------+---------+-----------+------------+--------+----+
5 rows in set (0.00 sec)


Drop table movies;
Query OK, 0 rows affected (1.31 sec)
mysql> show tables;
Empty set (0.00 sec)
 Drop database movies_db;
Query OK, 0 rows affected (0.26 sec)
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| products           |
| sakila             |
| sys                |
| world              |
+--------------------+
7 rows in set (0.00 sec)
