# Intro To Postgres

## Interacting with the Database
The connection object creates a client session with the database server that instantiates a persistent client to speak with. 
To issue commands against the database, you will also need to create a Cursor object using the Connection object. 
The Cursor object is the object we will use to execute our commands, describe tables for us, 
as well as prepare statements that we will eventually issue. Be warned though, whenever you close the connection, 
you will not be able to issue anymore commands with that connection's Cursor object.

To execute commands on the Postgres database, you call the execute method on the Cursor object with a stringified SQL command.
```python
import psycopg2
conn = psycopg2.connect("dbname=postgres user=postgres")
cur = conn.cursor()
cur.execute('SELECT * FROM users')
```

In this command, the cur object calls the execute method and, if it is successful, it will return None.
To get the returned value, or values, you need to call one of the two methods: fetchone() or fetchall(). 
The fetchone() method returns the first result or None and the fetchall() method returns a list of each row in the table or an 
empty list [] if there are no rows.

```python
import psycopg2
conn = psycopg2.connect("dbname=postgres user=postgres")
cur = conn.cursor()
cur.execute('SELECT * FROM users')
one = cur.fetchone()
all = cur.fetchall()
```

###Test
Connect to the dq database as the user dq
Using the Cursor object, create a string query that selects all from the notes table.
Execute the query using the execute method.
Fetch all the results from the table and assign it to the variable notes.
Close the Connection using the close method.

###Answer
```python
import psycopg2
conn = psycopg2.connect("dbname=dq user=dq")
cur = conn.cursor()
cur.execute('SELECT * FROM notes')
notes = cur.fetchall()
conn.close
```
