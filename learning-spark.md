# Learning Spark 2nd Edition
by Jules S. Damji, Brooke Wenig, Tathagata Das, and Denny Lee

- [Chapter 4 Spark SQL and DataFrames: Introduction to Built-in Data Sources](#chapter-4-spark-sql-and-dataframes-introduction-to-built-in-data-sources)
- [Chapter 8 Structured Streaming](#chapter-8-structured-streaming)
- [Chapter 9 Building Reliable Data Lakes with Apache Spark](#chapter-9-building-reliable-data-lakes-with-apache-spark)


## Chapter 4 Spark SQL and DataFrames Introduction to Built-in Data Sources
## Chapter 8 Structured Streaming

### Data Transformations

Only the DataFrame operations that can be executed incrementally are supported in Structured Streaming.
Are broadly classified into stateless and stateful operations

#### Incremental Execution and Streaming State

Spark SQL planner recognizes a streaming logical plan that needs to operate on continuous data streams and generates a 
continuous sequence of execution plans.  
The plan processes only a chunk of new data, a micro-batch, called the streaming "state".

#### Stateless Transformations

The following operations do not need any prior input data what makes them stateless operations.
* Projection operations: `select(), explode(), map(), flatMap()`
* Selection operations: `filter(), where()`

#### Stateful Transformations

Simplest example `DataFrame.groupBy().count()`
This state is maintained in the mem‐ ory of the Spark executors and is checkpointed.
The life cycle is automatically managed by Spark SQL, but normally is necessary to control resource usage.

##### Distributed and fault-tolerant state management


## Chapter 9 Building Reliable Data Lakes with Apache Spark

Processing logic only solves half of the end-to-end problem of building a pipeline.
The choice of storage solution determines the end-to-end robustness and performance of the data pipeline.  
In this chapter:
- Key features of a storage solution.
- Discuss two broad classes of storage solutions, data‐ bases and data lakes, and how to use Apache Spark with them.
- Next wave of storage solution, the lakehouses, and explore some 

### The Importance of an Optimal Storage Solution

Properties that are desired in a storage solution:
- Scalability and performance: should be able to scale to the volume and provide the read/write throughput and latency
based on workload.
- Transaction support: support for ACID (atomicity, consistency, isolation, durability) is essential to ensure the
quality.
- Support for diverse data formats: unstructured, semi-structured and structured data.
- Support for diverse workloads: SQL like BI analytics, batch like ETL jobs, Streaming like real-time monitoring and ML 
and AI like recommendations and churn predictions (detecting which customers are likely to leave a service or to cancel 
a subscription to a service).
- Openness: open data formats and standard APIs allows the business to use the most optimal tools.

### Databases

Architecture of databases and their workloads, and how to use Apache Spark for analytics workloads and limitations of 
databases in supporting modern non-SQL workloads.

#### A Brief Introduction to Databases

Store structured data as tables read using SQL queries. Strict schema. 
There are two types of workloads:
- Online transaction processing (OLTP): typically high-concurrency, low-latency, simple queries that read/update.
- Online analytical processing (OLAP): complex queries that require high-throughput scans over many records.

_Apache Spark is a query engine that is primarily designed for OLAP workloads._

#### Reading from and Writing to Databases Using Apache Spark

- JDBC: built-in JDBC data source is available to be used along with driver jars.
- Other modern databases: dedicated connectors that you can invoke using the appropriate format name.

#### Limitations of Databases

Reasons:
- Growth in data sizes: measure and collect everything, so the amount of data has increased from GBs to TBs.
- Growth in the diversity of analytics: need for deeper insights, growth of complex analytics (machine/deep learning).

Limitations:
- Databases are extremely expensive to scale out: most databases are not designed for scaling out to perform distributed
processing. The few industrial database solutions run on specialized hardware so ery expensive to acquire and maintain.
- Databases do not support non–SQL based analytics very well: they store data in complex format optimized for their own
processing engines so other tools like machine/deep learning cannot efficiently access data.
All this led to the development of a completely different approach to storing data, known as _data lakes_.

### Data Lakes

Distributed storage solution that runs on commodity hardware and easily scales out horizontally.

#### A Brief Introduction to Data Lakes

Decouple the distributed storage from the distributed compute allowing each system to scale out as 
needed. It also uses open formats and uses standard APIs.

Organizations build their data lakes by independently choosing the following:
- Storage system: HDFS on a cluster or any cloud object store (AWS S3, Azure DL Storage, or GC Storage).
- File format: structured (Parquet, ORC), semi-structured (JSON) or unstructured data (text, images, etc)
- Processing engine(s): batch processing engine (Spark, Presto, Apache Hive) or stream processing engine (Spark, Apache 
Flink) or a machine learning library (Spark MLlib, scikit-learn, R).

This flexibility is the biggest advantage of data lakes, which gives same performance characteristics, much cheaper than
databases.

#### Reading from and Writing to Data Lakes using Apache Spark

Apache Spark because it provides key features for DLs:
- Support for diverse workloads: provides batch processing, ETL operations, SQL workloads, stream processing, and 
machine learning.
- Support for diverse workloads: unstructured, semi-structured, and structured file formats. (see [Chapter 4](#chapter-4-spark-sql-and-dataframes-introduction-to-built-in-data-sources))
- Support for diverse filesystems:

#### Limitations of Data Lakes
### Lakehouses: The Next Step in the Evolution of Storage Solutions
#### Apache Hudi
#### Apache Iceberg
#### Delta Lake
### Building Lakehouses with Apache Spark and Delta Lake
#### Configuring Apache Spark with Delta Lake
#### Loading Data into a Delta Lake Table
#### Loading Data Streams into a Delta Lake Table
#### Enforcing Schema on Write to Prevent Data Corruption
#### Evolving Schemas to Accommodate Changing Data
#### Transforming Existing Data
#### Auditing Data Changes with Operation History
#### Querying Previous Snapshots of a Table with Time Travel
### Summary
