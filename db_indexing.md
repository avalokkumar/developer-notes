## Database Indexing

Database indexing is a method used to improve the speed and efficiency of searching, querying, and sorting data within a database. It involves creating a data structure that maps the values in one or more columns of a table to their physical location on a storage device. This data structure is commonly referred to as an index.

> The index provides a quick way to look up specific data in a table without having to search through every row of data in the table. By creating an index on a column or set of columns that are frequently used in queries or sorting, the database management system can more efficiently locate the relevant rows of data.

An index is created using a specific algorithm that determines the way in which the data is sorted and stored within the index. There are several types of indexes, including:

### B-Tree Indexes: 
B-tree indexes are the most commonly used type of index. They are used for fast retrieval of data based on a specific value or range of values. B-tree indexes are organized in a tree-like structure and allow for efficient searching, sorting, and range queries.

### Hash Indexes: 
Hash indexes are used for very fast lookups of data based on a single value. They work by mapping a specific value to a fixed location in the index. However, hash indexes are not as flexible as B-tree indexes, as they are only effective for equality comparisons.

### Bitmap Indexes: 
Bitmap indexes are used for columns with a low cardinality, meaning that there are only a few distinct values in the column. They work by creating a bitmap for each value in the column, where each bit in the bitmap represents a row in the table. Bitmap indexes can be very efficient for certain types of queries, such as counting the number of rows with a specific value.

### Clustered Indexes: 
Clustered indexes determine the physical order of data in a table based on the indexed column. This means that data is physically stored on disk in the same order as the index, which can result in improved performance for queries that access data in the order of the clustered index.

