# Comparing Databases

Databases types can be classified into two types:
-	Relational databases 
-	NOSQL databases 
There are also other special databases such as: object oriented databases and time series databases. 
NOSQL databases are generally categorised into four types:
- key value databases
- document databases 
- graph oriented databases
- column oriented databases
Each database categorie has its own advantages and disadvantages. 

Relational databases are generally used in applications where the data is complex, but the size is relatively small or medium. When we say the data is complex, we mean that there are many relationships (which are called associations in the entity-association model) between different entities, and join queries are frequently used to access the data.

The data used in these databases is structured, and the values are atomic. Additionally, these databases support ACID transactions.

Advantages :
-	The relational data model uses the relational algebra to access data which facilitate querying complex data. For example SQL is a very rich query language that supports most operations needed for data analysis, especially joins and aggregations..
-	ACID Transaction support
-	Data validation using constrains such as uniqueness, primary and foreign keys


Disadvantages :
-	Does not scale much. It’s not suitable for internet scale data. (Some solutions like Teradata exist for solving the volume problem but it’s not enough)
-	Steep learning curve for SQL

NOSQL databases are ,in the other hand, used with unstructured, semi structured data. It can store huge volumes of data ranging from terabytes to petabytes and beyond. But they support a more relaxed transaction model called BASE 
Key value databases store data stored and access it as a key-value pair: a Key is a unique identifier and a value stores complex data (like text) or binary data.  An example of a key-value database is DynamoDB.

Advantages :
-	Efficient index on data: very fast data access (access on key for highly distributed data)
-	Simple data model


Disadvantages :
-	Limited access API (generally only support get, set and sometimes filter. The API support for operators depend on the vendor). This limited access is not suitable for most use cases 

Document-oriented databases store aggregated data, such as JSON, as documents. An example of such a database is MongoDB.
Advantages :
-	Enables complex queries like aggregations
-	Supports Rich filters


Disadvantages: 
-	Slow writes and lack of consistency 
-	Doesn’t support join operator

The spelling and grammar in the given text are correct. However, there are a few changes that can be made to improve the clarity and readability of the text:

In column-oriented database, data is organized as columns, where each column stores aggregates and is grouped into column families. An example of a column-oriented database is Cassandra.

Advantages:
-	Evolving data schema
-	Efficient column oriented storage


Disadvantages :
-	Slow writes 
-	bad performance with small data and row based access 
-	doesn’t support generally join and aggregate (in some solutions the only way to aggregate data is to use mapreduce)

Graph oriented databases Store the data as a graph and represents the connexions between data records.

Advantages : 
-	Graph algorithms for efficient connected data querying


Disadvantages :
-	Doesn’t support well distribution


The choice of database in a particular system architecture generally depends on the use case. Some classic use cases include :
Relational databases : financial data like in banks
Key-value datastores : store data collected in real time for future processing like smart meters data collected from the smart grid
Document datastore : store blog data which is generally structured as a document. Clients profile data
Column oriented datastore : store data where use cases are to aggregate a limited number of columns such as data warehouse who aggregate certain number of column values
Graph datastores are suitable for social networks who have lots of connected data and are applied in industry for Fraud detection. 
