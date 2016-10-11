## SQL Questions

First create a database called fringe_shows
```
  #terminal
  psql
  create database fringe_shows;
  \q
```

Populate the data using the script - fringeshows.sql
```
  #terminal
  psql -d fringe_shows -f fringeshows.sql
```

Using the SQL Database file given to you as the source of data to answer the questions.  Copy the SQL command you have used to get the answer, and paste it below the question, along with the result they gave.


## Section 1

  Revision of concepts that we've learnt in SQL today

  1. Select the names of all users.

SELECT * FROM users;

id |           name            
----+---------------------------
  1 | Keith Douglas
  2 | Craig Morton
  3 | Sandy McMillan
  4 | Adrian Tuckwell
  5 | Alex Bazlinton
  6 | Bertie Coll
  7 | Bobby Ross
  8 | Carlos Pereira
  9 | Claudia Menting
 10 | Cookie Lacson
 11 | Cyrus Balsara
 12 | David OLeary
 13 | Diana Man
 14 | Euan Ramsay
 15 | Josephine Elder
 16 | Kate Manson
 17 | Kyle Grenell
 18 | Matthew Jeorrett
 19 | Max Veasey
 20 | Paul Milne
 21 | Pavlos MacDonald-Kosmidis
 22 | Ross Loggie
 23 | Thomas Crines
 24 | Tom Benham
(24 rows)

  2. Select the names of all shows that cost less than £15.

  SELECT * FROM shows WHERE "price" < 15;

   id | created_at |             name             | price 
  ----+------------+------------------------------+-------
    1 | 2016-08-23 | Le Haggis                    | 12.99
    5 | 2016-08-23 | Paul Dabek Mischief          | 12.99
    9 | 2016-08-23 | Best of Burlesque            |  7.99
   10 | 2016-08-23 | Two become One               |  8.50
   11 | 2016-08-23 | Urinetown                    |  8.50
   12 | 2016-08-23 | Two girls, one cup of comedy |  6.00
  (6 rows)

  3. Insert a user with the name "Val Gibson" into the users table.

  INSERT INTO users(name) VALUES ('Val Gibson');

  25 | Val Gibson

  4. Insert a record that Val Gibson wants to attend the show "Two girls, one cup of comedy".

  INSERT INTO "shows_users" (show_id, user_id) VALUES (12,25);

  5. Updates the name of the "Val Gibson" user to be "Valerie Gibson".

  INSERT INTO "shows_users" (show_id, user_id) VALUES (12,25);

  25 | Valerie Gibson

  6. Deletes the user with the name 'Valerie Gibson'.

  DELETE from users WHERE name = 'Valerie Gibson';

  7. Deletes the shows for the user you just deleted.

  DELETE from shows_users WHERE user_id = 25;


## Section 2

  This section involves more complex queries.  You will need to go and find out about aggregate funcions in SQL to answer some of the next questions.

  9. Select the names and prices of all shows, ordered by price in ascending order.

  SELECT name, price FROM shows ORDER BY price ASC;

                   name                   | price 
  -----------------------------------------+-------
   Two girls, one cup of comedy            |  6.00
   Best of Burlesque                       |  7.99
   Two become One                          |  8.50
   Urinetown                               |  8.50
   Paul Dabek Mischief                     | 12.99
   Le Haggis                               | 12.99
   Joe Stilgoe: Songs on Film – The Sequel | 16.50
   Game of Thrones - The Musical           | 16.50
   Shitfaced Shakespeare                   | 16.50
   Aaabeduation – A Magic Show             | 17.99
   Camille O'Sullivan                      | 17.99
   Balletronics                            | 32.00
   Edinburgh Royal Tattoo                  | 32.99
  (13 rows)


  10. Select the average price of all shows.

  SELECT AVG(price) FROM shows;

           avg         
  ---------------------
   15.9569230769230769
  (1 row)

  11. Select the price of the least expensive show.

  SELECT MIN(price) FROM shows;

   min  
  ------
   6.00
  (1 row

  12. Select the sum of the price of all shows.

  SELECT SUM(price) FROM shows;

    sum   
  --------
   207.44
  (1 row)

  13. Select the sum of the price of all shows whose prices is less than £20.

  SELECT SUM(price) FROM shows WHERE price < 20;

    sum   
  --------
   142.45
  (1 row)

  14. Select the name and price of the most expensive show.

  SELECT name, price FROM shows ORDER BY price DESC LIMIT 1;

            name          | price 
  ------------------------+-------
   Edinburgh Royal Tattoo | 32.99
  (1 row)

  15. Select the name and price of the second from cheapest show.



  16. Select the names of all users whose names start with the letter "N".

  SELECT * FROM users WHERE name LIKE 'N%';

   id | name 
  ----+------
  (0 rows)

  17. Select the names of users whose names contain "er".

  SELECT * FROM users WHERE name LIKE '%er%';

   id |      name       
  ----+-----------------
    6 | Bertie Coll
    8 | Carlos Pereira
   15 | Josephine Elder
  (3 rows)

## Section 3

  The following questions can be answered by using nested SQL statements but ideally you should learn about JOIN clauses to answer them.

  18. Select the time for the Edinburgh Royal Tattoo.

  SELECT time FROM times INNER JOIN shows ON times.show_id = shows.id where name = 'Edinburgh Royal Tattoo';

   time  
  -------
   22:00
  (1 row

  19. Select the number of users who want to see "Shitfaced Shakespeare".

  SELECT COUNT(shows_users.id) FROM shows_users INNER JOIN shows ON shows.id = shows_users.show_id WHERE name = 'Shitfaced Shakespeare';

   count 
  -------
       7
  (1 row)

  20. Select all of the user names and the count of shows they're going to see.

  SELECT * FROM users INNER JOIN shows_users ON users.id = shows_users.user_id;

  (Doesn't work fully)

  21. SELECT all users who are going to a show at 17:15.
