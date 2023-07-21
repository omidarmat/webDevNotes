# **PostgreSQL**

## **Concepts**

PostgreSQL is a relational database management system. It means that it is a system for managin data stored in _relations_, and by relations we mean _tables_.

Each table is a named collection of _rows_. Each row of a given table has the same set of named _columns_, and each column is of a specific data type.

Columns have a fixed order in each row, but SQL does not guarantee the order of rows within a table.

Tables are grouped into databases, and a collection of databases managed by a single PostgreSQL server instance consititutes a database _cluster_.

## **Working with PostgreSQL**

### **Creating a new table**

This is the syntax you need to create a new table:

```
CREATE TABLE weather (
    city            varchar(80),
    temp_lo         int,           -- low temperature
    temp_hi         int,           -- high temperature
    prcp            real,          -- precipitation
    date            date
);
```

PostgreSQL supports the standard SQL types:

| Type             | Description                                                        |
| ---------------- | ------------------------------------------------------------------ |
| varchar(N)       | stores arbitrary character strings up to `N` characters in length. |
| char(N)          | -                                                                  |
| int              | the normal integer type.                                           |
| smallint         | -                                                                  |
| real             | stores single precision floating-point numbers.                    |
| double precision | -                                                                  |
| date             | stores date.                                                       |
| point            | A PostgreSQL-specific data type that stores geographical location. |

> PostgreSQL can be customized with an arbitrary number of user-defined data types. Consequently, type names are not key words in the syntax, except where required to support special cases in the SQL standard.

> White space (i.e., spaces, tabs, and new lines) can be used freely in SQL commands.

> Two dashes (--) introduces comments

> SQL is case insensitive about key words and identifiers, except when identifiers are double-quoted to preserve the case.

### **Removing a new table**

If you don't need a table any longer or you want to recreate it differently, you can remove it using the following command:

```
DROP TABLE <tablename>;
```

### **Populating a table with rows**

The `INSERT` statement is used to insert rows into a table:

```
INSERT INTO weather VALUES ('Mashhad', 31, 40, 0.25, '1402-04-30');
```

> All data types use rather obvious input formats. Constants that are not simple numeric values should usually be surrounded by single quotes ('). The `date` type is actually very flexible in what it accepts.

The syntax mentioned above requires you to remember the order of columns. But you can use the syntax below to list the column order explicitly.

```
INSERT INTO weather (city, temp_lo, temp_hi, prcp, date)
  Values ('Mashhad', 31, 40, 0.25, '1402-04-30')
```

> You may also omit a column, for instance, the 'prcp', if it is unknown data.

You could also use the `COPY` command to load large amounts of data from flat-text files. The COPY command is optimized for this application, although it allows less flexibility than `INSERT`.

```
COPY weather from '/home/user/weather.txt';
```

### **Querying a table**

The `SELECT` statement is used to query a table. The statement is divided into:

1. **Select list:** the part that lists the columns to be returned.
2. **Table list:** the part that lists the tables from which to retrieve data
3. **Optional qualification:** the part that specifies any restrictions

#### **Retrieve all rows**

To retrieve all rows of a table:

```
SELECT * FROM weather;
```

> `*` is a shorthand for 'all columns'. It is widely considered bad code, since adding a column to the table would change the resutl. You could also do it like this:

```
SELECT city, temp_lo, temp_hi, prcp, date FROM weather;
```

In this case, we expect this output:

```
     city      | temp_lo | temp_hi | prcp |    date
---------------+---------+---------+------+------------
 San Francisco |      46 |      50 | 0.25 | 1994-11-27
 San Francisco |      43 |      57 |    0 | 1994-11-29
 Hayward       |      37 |      54 |      | 1994-11-29
(3 rows)
```

You can write **expressions**, not just simple column references, in the select list.

```
SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;
```

In this case, we expect this output:

```
     city      | temp_avg |    date
---------------+----------+------------
 San Francisco |       48 | 1994-11-27
 San Francisco |       50 | 1994-11-29
 Hayward       |       45 | 1994-11-29
(3 rows)
```

#### **Retrieve with qualification**

##### **`SELECT`**

A query can be _qualified_ by adding a `WHERE` caluse that specifies which rows are wanted. The clause contains a Boolean expression, and only rows for which the Boolean expression is true are returned. The usual Boolean operators (`AND`, `OR`, and `NOT`) are allowed in the qualification.

```
SELECT * FROM weather
    WHERE city = 'San Francisco' AND prcp > 0.0;
```

In this case, we expect this output:

```
     city      | temp_lo | temp_hi | prcp |    date
---------------+---------+---------+------+------------
 San Francisco |      46 |      50 | 0.25 | 1994-11-27
(1 row)
```

##### **`ORDER`**

You can request that the results of a query be returned in sorted order.

```
SELECT * FROM weather
    ORDER BY city, temp_lo;
```

##### **`DISTINCT`**

You can request that duplicate rows be removed from the result of the query.

```
SELECT DISTINCT city
    FROM weather;
```

This can be used along with the `ORDER` statement:

```
SELECT DISTINCT city
    FROM weather
    ORDER BY city;
```

#### **Join queryies**

Queries can access multiple tables at once, or access the same table in such a way that multiple rows of the table are being processed at the same time. Queries that access multiple tables or multiple instances of the same table at one time are called _join queries_.

Join queries combine rows from one table with rows from a second table, with an expression specifying which rows are to be paired.

We have two types of joins: **inner joins** and **outer joins**.

```
SELECT * FROM weather JOIN cities ON city = name;
```

> We can also relabel tables in the command:

```
SELECT * FROM weather w JOIN cities c ON w.city = c.name;
```

> This command will ignore any row on the 'weather' table the 'city' column of which does not match any 'name' column on the 'city' table. In the exmple above, the city 'hayward' has its row on the weather table, but not on the cities table. This can be fixed by implementing an outer join.

> We are very likely to receive an output where two columns hold same values. It obviously comes from the matching strategy. But we can fix this by explicitly typing the column names that should be displyed in the result:

```
SELECT city, temp_lo, temp_hi, prcp, date, location
    FROM weather JOIN cities ON city = name;
```

> If there are similar column names in both tables, we can specify which ones we are actually targetting:

```
SELECT weather.city, weather.temp_lo, weather.temp_hi,
       weather.prcp, weather.date, cities.location
    FROM weather JOIN cities ON weather.city = cities.name;
```

> It is considered good coding style to qualify all column names in a join query, so that the query won't fail if a duplicate column name is later added to one of the tables.

Join queries mentioned above can be written in the format below, but it is recommended to use the explicit syntax.

```
SELECT *
    FROM weather, cities
    WHERE city = name;
```

##### **Outer joins**

We have 3 different types of outer join:

1.  Left outer join
2.  Right outer join
3.  Full outer join
4.  Self join

###### **Left outer join**

In this example, we are going to use the left outer join.

```
SELECT *
    FROM weather LEFT OUTER JOIN cities ON weather.city = cities.name;
```

This query, as it is clear from its syntax, is called a _left outer join_. The table mentioned on the left of the join operator will have all of its rows in the output, while the table on the right side of the join operator will only have rows ouput that match a row on the left table. For rows that there was no match, empty (`null`) values are inserted for the table on the right.

###### **Self outer join**

This is used to join a table against itself. Suppose we want to find all the weather records that are in the temperature range of other weather records. We would have to compare the `temp_lo` and `temp_hi` columns of each weather row to the `temp_lo` and `temp_hi` columns of all other weather rows. This is implemented by:

```
SELECT w1.city, w1.temp_lo AS low, w1.temp_hi AS high,
       w2.city, w2.temp_lo AS low, w2.temp_hi AS high
    FROM weather w1 JOIN weather w2
        ON w1.temp_lo < w2.temp_lo AND w1.temp_hi > w2.temp_hi;
```

> Notice how we have relabled the table weather two times, once `w1`, and then `w2` to be able to distinguish the left and ride side of the join.
