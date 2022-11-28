# ClickHouse

## A Brief Intro to Primary Keys

Before you go any further, it is important to understand how primary keys work in ClickHouse (the implementation of primary keys might seem unexpected!):

* primary keys in ClickHouse are **not unique** for each row in a table.

The primary key of a ClickHouse table determines how the data is sorted when written to disk. Every 8,192 rows or 10MB of data (referred to as the **index granularity**) creates an entry in the primary key index file. This granularity concept creates a sparse index that can easily fit in memory, and the granules represent a stripe of the smallest amount of column data that gets processed during **`SELECT`** queries.

**Related** :
```
#java #clickhouse #vector
```

**Links** :
```
https://clickhouse.com/docs/en/quick-start#a-brief-intro-to-primary-keys
```
