# Introduction to SQL

## SQL
Structured Query Language (SQL) is a standard computer language for relational database management and data manipulation. SQL is used to query, insert, update and modify data.


## Intro to Relational Databases
We will be using Postgres for our database and Postico for our client. Keep in mind you can use Postgres with Node.js, SQLite for mobile or MySQL for PHP. SQL is common across all of these different platforms.

Designed to be able to efficiently read and write large amounts of data when properly configured

 - Provides ACID guarantees:
  - Atomicity - each transaction is all or nothing
  - Consistency - each tx brings DB from valid state to a new valid state. All constraints still hold
  - Isolation - concurrent transactions should appear serial to the user, no in progress tx should know about data from another in progress tx
  - Durability - withstand crashes and power failures

## Intro to Postico

- Created our first table

```SQL
CREATE TABLE "songs" (
  "id" SERIAL PRIMARY KEY,
  "rank" INTEGER,
  "artist" VARCHAR(80) NOT NULL,
  "track" VARCHAR(120) NOT NULL,
  "published" date
);
```

### INSERT
Add a new row to the database. Only fields marked as NOT NULL are required. Column names are entered using `""` and values are entered with `''`.

- INSERT a single record

```SQL
INSERT INTO "songs" ("rank", "track", "artist", "published") 
VALUES (357, 'Wonderwall', 'Oasis', '1-1-1996');
```

- INSERT multiple records

```SQL
INSERT INTO "songs" ("rank", "track", "artist", "published") 
VALUES
(357, 'Wonderwall', 'Oasis', '1-1-1996'),
(102, 'Under the Bridge', 'Red Hot Chili Peppers', '1-1-1992');
```

### SELECT
Queries for data in the database. This is how we get data back from our tables.

```SQL
/* Wildcard for select, returns all rows & columns */
SELECT * FROM "songs";

/* Pick specific columns */
SELECT "track", "artist" FROM "songs";

/* LIMIT the number of rows, must be last! */
SELECT * FROM "songs" LIMIT 10; 

/* Items in [] are optional. In summary:
SELECT column
FROM table
[WHERE conditions]
[ORDER BY column [ ASC | DESC ]]
LIMIT number_rows [ OFFSET offset_value ];
*/
```

### UPDATE
Updates an existing record.

```SQL
UPDATE "songs" SET "artist"='Chris Black' WHERE id = 1;
```

   > **DON'T FORGET THE WHERE!** Otherwise all items are updated.


### DELETE
Deletes an existing record.

```SQL
DELETE FROM "songs" WHERE "id" = 6;

/* In summary 
DELETE FROM table
[WHERE conditions];
*/
```

### Drop a table

Completely removes a table and all of its rows/data. **This is Permanent.**

```sql
DROP TABLE songs;
```