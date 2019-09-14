# Crreating a table

## How to create

```SQL
CREATE TABLE tableName(
   column1 dataType1 PRIMARY KEY,
   column2 dataType2,
   column3 dataType3,
   ...
);
```
## Dropping a table

Here's how to drop a table and how to check if it exists:
```python
conn = psycopg2.connect("dbname=dq user=dq")
cur = conn.cursor()
cur.execute("DROP TABLE IF EXISTS example")
cur.execute("CREATE TABLE example(count INTEGER)")
```

### Test
Connect to the dq database as the user dq
Write a SQL query that creates a table called users in the dq database, with the following columns and data types:
id -- integer data type, and is a primary key.
email -- text data type.
name -- text data type.
address -- text data type.
Execute the query using the execute method.
Don't close the connection.

### Answer
```python
import psycopg2
conn = psycopg2.connect("dbname =dq user=dq")
cur = conn.cursor()
#Execute
cur.execute('CREATE TABLE users(id integer PRIMARY KEY,email text,name text, address text)')
```
