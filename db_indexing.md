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

A bitmap index is a data structure used in databases to optimize querying and retrieval of data. It is particularly effective for fields with a low cardinality, where the number of distinct values is relatively small compared to the total number of records. Bitmap indexes store a bitmap for each distinct value in the indexed field, indicating which records contain that value.

#### Here are some key points about bitmap indexes:

1. #### Structure: 
A bitmap index consists of multiple bitmaps, one for each distinct value in the indexed field. Each bitmap has a bit position for every record in the table. The bit is set to 1 if the corresponding record contains the indexed value and 0 otherwise.

2. #### Space Efficiency: 
Bitmap indexes are space-efficient, especially when the number of distinct values is small compared to the number of records. The space required for a bitmap index is proportional to the number of distinct values, not the total number of records.

3. #### Query Performance: 
Bitmap indexes excel at improving query performance for operations involving multiple conditions. They allow for efficient bitwise operations such as AND, OR, and NOT, which can quickly identify the records that satisfy complex queries.

4. #### Suitable Data Types: 
Bitmap indexes are most effective for low-cardinality fields, such as boolean fields (true/false), enumerated types, or categorical variables. They are less efficient for high-cardinality fields with a large number of distinct values.

#### Now let's explore how to use a bitmap index with an example:

Suppose you have a database table called "Employees" with the following columns: "ID", "Name", "Department", and "Salary". Let's say the "Department" column has a limited number of distinct values representing different departments in the company.

To create a bitmap index on the "Department" column, you can use the following SQL statement:
```
CREATE BITMAP INDEX idx_department ON Employees(Department);
```

Once the index is created, it allows for efficient querying and retrieval of data based on department. For example:

- Query 1: Retrieve all employees in the "Sales" department:
```
SELECT * FROM Employees WHERE Department = 'Sales';
```

- Query 2: Retrieve all employees in the "Sales" or "Marketing" department:

```
SELECT * FROM Employees WHERE Department IN ('Sales', 'Marketing');
```

- Query 3: Retrieve all employees not in the "HR" department:

```
SELECT * FROM Employees WHERE Department != 'HR';
```

In each of these queries, the bitmap index on the "Department" column helps quickly identify the relevant records by performing bitwise operations on the bitmaps associated with the respective values.

The decision to use a bitmap index should be based on the characteristics of your data and the queries you frequently run. Bitmap indexes are most beneficial for fields with a low number of distinct values and when the queries involve multiple conditions or logical operations.

> Bitmap indexes incur some overhead during data modification operations (inserts, updates, deletes), as the index needs to be updated accordingly. Therefore, it's recommended to evaluate the trade-offs and consider the specific requirements of your database before implementing bitmap indexes.

---
### Clustered Indexes: 

> A clustered index is a type of index used in databases to physically order the data in a table based on the values of one or more columns. The rows of the table are stored in the same order as the clustered index, which determines the physical organization of the data on disk. Here's some information about clustered indexes:

1. #### Data Organization: 
A clustered index determines the physical order of the data rows in a table. In other words, it defines how the data is stored on disk. Each table can have only one clustered index.

2. #### Sorting and Retrieval: 
The clustered index enables efficient sorting and retrieval of data based on the indexed column(s). When a query filters or sorts data using the clustered index column(s), the database can access the data in the sorted order, leading to improved query performance.

3. #### Impact on Inserts and Updates: 
Because the data is physically ordered based on the clustered index, inserting new rows or updating existing rows may require rearranging the data to maintain the sorted order. This can impact the performance of insert and update operations compared to non-clustered indexes.

4. #### Primary Key: 
By default, a primary key constraint in a table is implemented using a clustered index. The primary key uniquely identifies each row in the table and determines the physical order of the data.

Using a clustered index with an example:

Suppose you have a database table called "Customers" with columns such as "CustomerID", "Name", "Email", and "Address". To create a clustered index on the "CustomerID" column, you can use the following SQL statement:

```
CREATE CLUSTERED INDEX idx_customerid ON Customers(CustomerID);
```

After creating the clustered index, the rows in the "Customers" table will be physically ordered based on the values in the "CustomerID" column. This means that queries that filter or sort based on the "CustomerID" column will benefit from the sorted data organization.

For example, consider the following query to retrieve customer details based on their IDs:
```
SELECT * FROM Customers WHERE CustomerID BETWEEN 100 AND 200;
```

> With a clustered index on the "CustomerID" column, the database engine can quickly locate the range of rows that satisfy the condition because the data is stored in the sorted order of the index. This leads to improved query performance.

It's important to consider the following factors when deciding to use a clustered index:

* Data Distribution: Clustered indexes work best when the data is evenly distributed across the index key values. Uneven distribution or frequent updates to the indexed column(s) can result in data fragmentation and performance degradation.

* Primary Key or Natural Order: Clustered indexes are commonly used on primary key columns because primary keys are unique and typically ordered sequentially. If your table has a column that naturally orders the data, using a clustered index on that column can be beneficial.

* Query Patterns: Evaluate the queries frequently performed on the table and identify the columns used for filtering or sorting. If a particular column is frequently used in such operations, creating a clustered index on that column can improve query performance.

* Insert and Update Frequency: Consider the frequency of insert and update operations on the table. Inserting new rows or updating the indexed column(s) in a table with a clustered index can incur overhead due to the need to rearrange the data.

Not all tables require a clustered index. In some cases, a non-clustered index or a combination of indexes may be more suitable based on the query patterns and specific requirements of the database.
