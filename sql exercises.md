one_to_many_assignment=# select * from authors 
one_to_many_assignment-# ;
one_to_many_assignment=# select * from authors where name= 'Kara Melton'
one_to_many_assignment-# ;
one_to_many_assignment=# select id from authors where name= 'Kara Melton'
one_to_many_assignment-# ;
 id 
----
  8
(1 row)

one_to_many_assignment=# select * from articles where authors_id= 8;
ERROR:  column "authors_id" does not exist
LINE 1: select * from articles where authors_id= 8;
                                     ^
HINT:  Perhaps you meant to reference the column "articles.author_id".
one_to_many_assignment=# select * from articles where articles.authors_id= 8;
ERROR:  column articles.authors_id does not exist
LINE 1: select * from articles where articles.authors_id= 8;
                                     ^
HINT:  Perhaps you meant to reference the column "articles.author_id".
one_to_many_assignment=# select * from articles
one_to_many_assignment-# ;
one_to_many_assignment=# select * from articles where author_id= 8;
one_to_many_assignment=# select * from articles where author_id= 8;
one_to_many_assignment=# select id from provinces where name= 'Ontario'
one_to_many_assignment-# ;
 id 
----
 14
(1 row)

one_to_many_assignment=# select * from cities where province_id= 14;
 id |  name   | year_founded | province_id 
----+---------+--------------+-------------
  8 | Toronto |         1793 |          14
 11 | Ottawa  |         1826 |          14
(2 rows)

one_to_many_assignment=# select author_id from articles where title='Coding Bootcamps and Emotional labor';
 author_id 
-----------
(0 rows)

one_to_many_assignment=# \d+ articles
one_to_many_assignment=# \d+ articles
                                                         Table "public.articles"
  Column   |          Type          | Collation | Nullable |               Default                | Storage  | Stats target | Description 
-----------+------------------------+-----------+----------+--------------------------------------+----------+--------------+-------------
 id        | integer                |           | not null | nextval('articles_id_seq'::regclass) | plain    |              | 
 author_id | integer                |           |          |                                      | plain    |              | 
 title     | character varying(255) |           |          |                                      | extended |              | 
 body      | text                   |           |          |                                      | extended |              | 
 date      | date                   |           |          |                                      | plain    |              | 
Indexes:
    "articles_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "articles_author_id_fkey" FOREIGN KEY (author_id) REFERENCES authors(id)

one_to_many_assignment=# select title from articles;
                                              title                                               
--------------------------------------------------------------------------------------------------
 I Can Text You A Pile of Poo, But I Can’t Write My Name
 The Hidden Dangers of AI for Queer and Trans People
 Coding Bootcamps and Emotional Labor
 The Problem With the Zuckerberg Analogy for Youth of Color
 It is Bigger Than Microaggressions
 Side Project Culture: Opportunities and Obstacles for Marginalized People in Tech
 Technology Colonialism
 Making Tech Spaces Safe for Diverse Faces
 How Tech Business Models Come From Marginalized Communities, But Startups Are Still Mostly White
 Confronting the Assumption of Whiteness in Virtual Spaces
(10 rows)

one_to_many_assignment=# select author_id from titles
one_to_many_assignment-# ;
ERROR:  relation "titles" does not exist
LINE 1: select author_id from titles
                              ^
one_to_many_assignment=# select author_id from articles;
 author_id 
-----------
         2
         3
         4
         5
         5
         6
         7
         7
         8
         8
(10 rows)
^C
one_to_many_assignment-# select author_id from articles
one_to_many_assignment-# where title = 'Coding Bootcamps and Emotional Labor'
one_to_many_assignment-# ;
ERROR:  syntax error at or near "select"
LINE 2: select author_id from articles
        ^
one_to_many_assignment=# Select author_id from articles

one_to_many_assignment-# where title = 'Coding Bootcamps and Emotional Labor'
one_to_many_assignment-# ;
 author_id 
-----------
         4
(1 row)

one_to_many_assignment=# select name from author where id= 4
one_to_many_assignment-# ;
ERROR:  relation "author" does not exist
LINE 1: select name from author where id= 4
                         ^
one_to_many_assignment=# select name from authors where id= 4
;
       name        
-------------------
 Tilde Ann Thurium
(1 row)

one_to_many_assignment=# \d+ provinces
                                                           Table "public.provinces"
    Column    |          Type          | Collation | Nullable |                Default                | Storage  | Stats target | Description 
--------------+------------------------+-----------+----------+---------------------------------------+----------+--------------+-------------
 id           | integer                |           | not null | nextval('provinces_id_seq'::regclass) | plain    |              | 
 name         | character varying(255) |           |          |                                       | extended |              | 
 year_founded | integer                |           |          |                                       | plain    |              | 
 country_id   | integer                |           |          |                                       | plain    |              | 
Indexes:
    "provinces_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "provinces_country_id_fkey" FOREIGN KEY (country_id) REFERENCES countries(id)
Referenced by:
    TABLE "cities" CONSTRAINT "cities_province_id_fkey" FOREIGN KEY (province_id) REFERENCES provinces(id)

one_to_many_assignment=# select id from countries where name= 'Canada'
one_to_many_assignment-# ;
 id 
----
  1
(1 row)

one_to_many_assignment=# select Count(provinces) where country_id= 1;
ERROR:  column "provinces" does not exist
LINE 1: select Count(provinces) where country_id= 1;
                     ^
one_to_many_assignment=# select Count(name) from provinces where country_id= 1;
 count 
-------
    14
(1 row)

one_to_many_assignment=# \d+ provinces
                                                           Table "public.provinces"
    Column    |          Type          | Collation | Nullable |                Default                | Storage  | Stats target | Description 
--------------+------------------------+-----------+----------+---------------------------------------+----------+--------------+-------------
 id           | integer                |           | not null | nextval('provinces_id_seq'::regclass) | plain    |              | 
 name         | character varying(255) |           |          |                                       | extended |              | 
 year_founded | integer                |           |          |                                       | plain    |              | 
 country_id   | integer                |           |          |                                       | plain    |              | 
Indexes:
    "provinces_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "provinces_country_id_fkey" FOREIGN KEY (country_id) REFERENCES countries(id)
Referenced by:
    TABLE "cities" CONSTRAINT "cities_province_id_fkey" FOREIGN KEY (province_id) REFERENCES provinces(id)

one_to_many_assignment=# select name from provinces;
           name            
---------------------------
 Ontario
 Quebec
 New Brunswick
 New Brunswick
 Nova Scotia
 Manitoba
 Northwest Territories
 British Columbia
 Prince Edward Island
 Yukon Territory
 Alberta
 Saskatchewan
 Newfoundland and Labrador
 Nunavut
(14 rows)

one_to_many_assignment=# \d+ residences
                                                          Table "public.residences"
   Column   |          Type          | Collation | Nullable |                Default                 | Storage  | Stats target | Description 
------------+------------------------+-----------+----------+----------------------------------------+----------+--------------+-------------
 id         | integer                |           | not null | nextval('residences_id_seq'::regclass) | plain    |              | 
 address    | character varying(255) |           |          |                                        | extended |              | 
 year_built | integer                |           |          |                                        | plain    |              | 
 city_id    | integer                |           |          |                                        | plain    |              | 
Indexes:
    "residences_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "residences_city_id_fkey" FOREIGN KEY (city_id) REFERENCES cities(id)
Referenced by:
    TABLE "persons" CONSTRAINT "persons_residence_id_fkey" FOREIGN KEY (residence_id) REFERENCES residences(id)

one_to_many_assignment=# select id from residences
one_to_many_assignment-# where address='4740 McDermott Street';
 id 
----
  9
one_to_many_assignment=# sel
one_to_many_assignment-# select id from residences where address= '4740 McDermot 
one_to_many_assignment-# select count(name) from persons where residence_id= 9;
ERROR:  syntax error at or near "sel"
LINE 1: sel
        ^
one_to_many_assignment=#    
select count(name) from persons where residence_id= 9;
 count 
-------
     2
(1 row)

one_to_many_assignment=# select name from provinces where residence_id= 9;
ERROR:  column "residence_id" does not exist
LINE 1: select name from provinces where residence_id= 9;
                                         ^
one_to_many_assignment=# select id from cities where residence_id= 9;
ERROR:  column "residence_id" does not exist
LINE 1: select id from cities where residence_id= 9;
                                    ^
one_to_many_assignment=# \d+ cities
                                                           Table "public.cities"
    Column    |          Type          | Collation | Nullable |              Default               | Storage  | Stats target | Description 
--------------+------------------------+-----------+----------+------------------------------------+----------+--------------+-------------
 id           | integer                |           | not null | nextval('cities_id_seq'::regclass) | plain    |              | 
 name         | character varying(255) |           |          |                                    | extended |              | 
 year_founded | integer                |           |          |                                    | plain    |              | 
 province_id  | integer                |           |          |                                    | plain    |              | 
Indexes:
    "cities_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "cities_province_id_fkey" FOREIGN KEY (province_id) REFERENCES provinces(id)
Referenced by:
    TABLE "residences" CONSTRAINT "residences_city_id_fkey" FOREIGN KEY (city_id) REFERENCES cities(id)

one_to_many_assignment=# \d+ provinces
                                                           Table "public.provinces"
    Column    |          Type          | Collation | Nullable |                Default                | Storage  | Stats target | Description 
--------------+------------------------+-----------+----------+---------------------------------------+----------+--------------+-------------
 id           | integer                |           | not null | nextval('provinces_id_seq'::regclass) | plain    |              | 
 name         | character varying(255) |           |          |                                       | extended |              | 
 year_founded | integer                |           |          |                                       | plain    |              | 
 country_id   | integer                |           |          |                                       | plain    |              | 
Indexes:
    "provinces_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "provinces_country_id_fkey" FOREIGN KEY (country_id) REFERENCES countries(id)
Referenced by:
    TABLE "cities" CONSTRAINT "cities_province_id_fkey" FOREIGN KEY (province_id) REFERENCES provinces(id)

one_to_many_assignment=# \d+ countries
one_to_many_assignment=# \d+ persons
                                                           Table "public.persons"
    Column    |          Type          | Collation | Nullable |               Default               | Storage  | Stats target | Description 
--------------+------------------------+-----------+----------+-------------------------------------+----------+--------------+-------------
 id           | integer                |           | not null | nextval('persons_id_seq'::regclass) | plain    |              | 
 name         | character varying(255) |           |          |                                     | extended |              | 
 age          | integer                |           |          |                                     | plain    |              | 
 residence_id | integer                |           |          |                                     | plain    |              | 
Indexes:
    "persons_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "persons_residence_id_fkey" FOREIGN KEY (residence_id) REFERENCES residences(id)

one_to_many_assignment=# \d+ residences
                                                          Table "public.residences"
   Column   |          Type          | Collation | Nullable |                Default                 | Storage  | Stats target | Description 
------------+------------------------+-----------+----------+----------------------------------------+----------+--------------+-------------
 id         | integer                |           | not null | nextval('residences_id_seq'::regclass) | plain    |              | 
 address    | character varying(255) |           |          |                                        | extended |              | 
 year_built | integer                |           |          |                                        | plain    |              | 
 city_id    | integer                |           |          |                                        | plain    |              | 
Indexes:
    "residences_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "residences_city_id_fkey" FOREIGN KEY (city_id) REFERENCES cities(id)
Referenced by:
    TABLE "persons" CONSTRAINT "persons_residence_id_fkey" FOREIGN KEY (residence_id) REFERENCES residences(id)

one_to_many_assignment=# \d+ residences
                                                          Table "public.residences"
   Column   |          Type          | Collation | Nullable |                Default                 | Storage  | Stats target | Description 
------------+------------------------+-----------+----------+----------------------------------------+----------+--------------+-------------
 id         | integer                |           | not null | nextval('residences_id_seq'::regclass) | plain    |              | 
 address    | character varying(255) |           |          |                                        | extended |              | 
 year_built | integer                |           |          |                                        | plain    |              | 
 city_id    | integer                |           |          |                                        | plain    |              | 
Indexes:
    "residences_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "residences_city_id_fkey" FOREIGN KEY (city_id) REFERENCES cities(id)
Referenced by:
    TABLE "persons" CONSTRAINT "persons_residence_id_fkey" FOREIGN KEY (residence_id) REFERENCES residences(id)

one_to_many_assignment=# select city_id from residences 
one_to_many_assignment-# where address='4740 McDermott Street;
one_to_many_assignment'# ;
one_to_many_assignment'# select city_id from residences
one_to_many_assignment'# where address='4740 McDermott Street'
one_to_many_assignment'# ;
one_to_many_assignment'# q
one_to_many_assignment'# \q
yjacobs@yaels-computer:~/bitmaker/projects/data-modelling-1-many$ psql one_to_many_assignment
psql (10.8 (Ubuntu 10.8-0ubuntu0.18.04.1))
Type "help" for help.

one_to_many_assignment=# select city_id from residences 
one_to_many_assignment-# where address= '4740 McDermott Street'
one_to_many_assignment-# ;
 city_id 
---------
      11
(1 row)

one_to_many_assignment=# select name from cities where id= 11;
  name  
--------
 Ottawa
(1 row)

one_to_many_assignment=# select name from countries where city_id= 11;
ERROR:  column "city_id" does not exist
LINE 1: select name from countries where city_id= 11;
                                         ^
one_to_many_assignment=# select name from provinces where city_id= 11;
ERROR:  column "city_id" does not exist
LINE 1: select name from provinces where city_id= 11;
                                         ^
one_to_many_assignment=# select province_id from cities
where name= 'Ottawa'
;
 province_id 
-------------
          14
(1 row)

one_to_many_assignment=# select name from provinces where id= 14;
  name   
---------
 Ontario
(1 row)

one_to_many_assignment=# select country_id from provinces
where name= 'Ontario'
;
 country_id 
------------
          1
(1 row)

one_to_many_assignment=# select name from country where id= 1;
ERROR:  relation "country" does not exist
LINE 1: select name from country where id= 1;
                         ^
one_to_many_assignment=# select name from countries where id= 1;
  name  
--------
 Canada
(1 row)

one_to_many_assignment=# slect id from persons 
one_to_many_assignment-# where name='Destini Davis';
ERROR:  syntax error at or near "slect"
LINE 1: slect id from persons 
        ^
one_to_many_assignment=# select id from persons 
where name='Destini Davis';
 id 
----
  3
(1 row)

one_to_many_assignment=# select residence_id from persons 
where name='Destini Davis';
 residence_id 
--------------
            2
(1 row)

one_to_many_assignment=# select city_id from residences 
where id = 2;                         
;
 city_id 
---------
       8
(1 row)

one_to_many_assignment=# select province_id from cities
where id= 8       
;
 province_id 
-------------
          14
(1 row)

one_to_many_assignment=# select country_id from provinces
where id = 14        
;
 country_id 
------------
          1
(1 row)

one_to_many_assignment=# select name from countries where id= 1;
  name  
--------
 Canada
(1 row)

one_to_many_assignment=# select id from authors where name 
one_to_many_assignment-# = 'Aditya Mukerjee';
 id 
----
  2
(1 row)

one_to_many_assignment=# select count(name) from articles 
one_to_many_assignment-# where author_id = 2;
ERROR:  column "name" does not exist
LINE 1: select count(name) from articles 
                     ^
HINT:  Perhaps you meant to reference the column "articles.date".
one_to_many_assignment=# \d+ articles
                                                         Table "public.articles"
  Column   |          Type          | Collation | Nullable |               Default                | Storage  | Stats target | Description 
-----------+------------------------+-----------+----------+--------------------------------------+----------+--------------+-------------
 id        | integer                |           | not null | nextval('articles_id_seq'::regclass) | plain    |              | 
 author_id | integer                |           |          |                                      | plain    |              | 
 title     | character varying(255) |           |          |                                      | extended |              | 
 body      | text                   |           |          |                                      | extended |              | 
 date      | date                   |           |          |                                      | plain    |              | 
Indexes:
    "articles_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "articles_author_id_fkey" FOREIGN KEY (author_id) REFERENCES authors(id)

one_to_many_assignment=# select count(title) from articles 
where author_id = 2;
 count 
-------
     1
(1 row)

