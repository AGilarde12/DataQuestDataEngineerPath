If you checked the dq database now, you would notice that there actually isn't a users table inside it. 
This isn't a bug -- it's because of a concept called SQL transactions. 
With SQLite, every query we made that modified the data was executed and immediately changed the database.

With Postgres, we're dealing with multiple users who could be changing the database at the same time. 
Let's imagine a simple scenario where we're keeping track of accounts for different customers of a bank. 
We could write a simple query to create a table for this:

```sql
CREATE TABLE accounts(
   id integer PRIMARY KEY,
   name text,
   balance float
);
```

Let's say we have the following two rows in the table:
id    name    balance
1     Jim     100
2     Sue     200

```sql
UPDATE accounts SET balance=200 WHERE name="Jim";

UPDATE accounts SET balance=100 WHERE name="Sue";
```

In the above example, we remove 100 dollars from Sue, and add 100 dollars to Jim. 
Let's say either the second UPDATE statement has an error in it, the database fails, or another user has a conflicting query. 
The first query would run properly, but the second would fail. That would result in the following:

Whenever we open a Connection in psycopg2, a new transaction will automatically be created. 
All queries run up until the commit method is called. When a commit is called, 
the PostgreSQL engine will run all the queries at once.

If we don't want to apply the changes in the transaction block,
we can call the rollback method to remove the transaction.
Not calling either commit or rollback will cause the transaction to stay in a pending state, 
and will result in the changes not being applied to the database.

## Test
Connect to the dq database as the user dq.
Write a SQL query that creates a table called users in the dq database, with the following columns and data types:
id -- integer data type, and is a primary key.
email -- text data type.
name -- text data type.
address -- text data type.
Execute the query using the execute method.
Use the commit method on the Connection object to apply the changes in the transaction to the database.
Close the Connection.

## Answer
