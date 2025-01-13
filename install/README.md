# Install

To install and run a Cassandra instance locally we'll use a dockerfile locally,
but for the server we'll go native installation.

## Docker

Following instructions in here;

https://cassandra.apache.org/doc/stable/cassandra/getting_started/installing.html

- Step 1: `docker pull casssandra:latest`
- Step 2: `docker run --name learn-cassandra.install -d -p 9042:9042
  cassandra:latest`
  - :information_source: `-p 9042:9042` to expose port to make it available from
    outside of docker
- Step 3: `docker exec -it learn-cassandra.install cqlsh`
  - Or download DbVisualizer from
    [https://www.dbvis.com/download/](https://www.dbvis.com/download/)

## Ubuntu

...

## Test Installation

Connect to the instance and create a sample keyspace (which is to Cassandra what
schema or a database is to an RDBMS).

```cql
CREATE KEYSPACE my_keyspace WITH
  replication = {
    'class': 'SimpleStrategy',
    'replication_factor': 1
  }
;
```

Switch to that keyspace by `USE my_keyspace;`.

Create a table as below;

```cql
CREATE TABLE user (
  first_name text,
  last_name text,
  PRIMARY KEY (first_name)
);
```

Insert and select a record just like in a SQL database;

```cql
INSERT
  INTO user (first_name, last_name)
  VALUES ('John', 'Doe');

SELECT * FROM user WHERE first_name='John';
```

It allows you to delete a column;

```cql
DELETE last_name
FROM user
WHERE first_name='John';
```

You can also delete a row as you do in SQL;

```cql
DELETE FROM user
WHERE first_name='John';
```
