## Database Indexing

Database indexing is a method used to improve the speed and efficiency of searching, querying, and sorting data within a database. It involves creating a data structure that maps the values in one or more columns of a table to their physical location on a storage device. This data structure is commonly referred to as an index.

> The index provides a quick way to look up specific data in a table without having to search through every row of data in the table. By creating an index on a column or set of columns that are frequently used in queries or sorting, the database management system can more efficiently locate the relevant rows of data.

An index is created using a specific algorithm that determines the way in which the data is sorted and stored within the index. There are several types of indexes, including:

---
### B-Tree Indexes: 

B-Tree indexes are a type of database index that is commonly used to improve the performance of searches and queries on large datasets. They are a balanced tree data structure that organizes data in a hierarchical manner, allowing for fast searching, sorting, and range queries.

#### What is B-Tree Indexe?

A B-Tree index consists of multiple levels of nodes, with each node containing a certain number of keys and pointers to child nodes or data records. The top-level node of the tree, called the root node, contains pointers to the child nodes below it. The leaf nodes of the tree contain pointers to the data records stored in the table.


#### When to use it?
B-Tree indexes are commonly used when there is a need to search for data in a table using a specific value or range of values. They are especially useful for queries that involve a range of values, such as finding all records within a certain date range or between two prices.

#### How to use it?
To use a B-Tree index, you must first create the index on one or more columns of the table. This can be done using a command in the database management system, such as CREATE INDEX. Once the index is created, the database management system will automatically use it to improve the performance of searches and queries that involve the indexed columns.

> When using a B-Tree index, always try to choose the appropriate column or columns to index. Columns that are frequently used in searches or sorting should be indexed, while columns that are rarely used may not need to be indexed. Additionally, too many indexes can have a negative impact on database performance, as the database management system must maintain and update each index whenever data in the table is added, deleted, or modified.

```
CREATE INDEX idx_customers_last_name
ON customers (last_name);
```
> This code creates a B-Tree index named "idx_customers_last_name" on the "last_name" column of the "customers" table. The database management system will use this index to speed up searches and queries that involve the "last_name" column.
---
### Hash Indexe: 
Hash indexes are used for very fast lookups of data based on a single value. They work by mapping a specific value to a fixed location in the index, allowing for extremely fast access to the data.

#### What is Hash Indexe?
A hash index consists of an array of buckets, where each bucket contains a linked list of data records that map to the same hash value. The hash function used to map values to the buckets is designed to minimize collisions, which occur when two different values map to the same bucket.

#### When to use it? 
Hash indexes are commonly used when there is a need to perform fast lookups of data based on a specific value. They are especially useful for equality comparisons, such as finding all records with a specific ID or name.

#### How to use it?
To use a hash index, you must first create the index on the column of the table that you want to index. This can be done using a command in the database management system, such as CREATE INDEX. Once the index is created, the database management system will automatically use it to speed up searches and queries that involve the indexed column.

Here's an example of how to create a hash index in SQL for a table called `employees` with a column called `employee_id`:
```
CREATE INDEX idx_employees_employee_id
ON employees USING HASH (employee_id);
```

> This code creates a hash index named `idx_employees_employee_id` on the `employee_id` column of the "employees" table. The "USING HASH" keyword tells the database management system to use a hash function to create the index.
---
### Bitmap Indexes: 
> Bitmap indexes are used for columns with a low cardinality, meaning that there are only a few distinct values in the column. They work by creating a bitmap for each value in the column, where each bit in the bitmap represents a row in the table. Bitmap indexes can be very efficient for certain types of queries, such as counting the number of rows with a specific value.
---
### Clustered Indexes: 
> Clustered indexes determine the physical order of data in a table based on the indexed column. This means that data is physically stored on disk in the same order as the index, which can result in improved performance for queries that access data in the order of the clustered index.

