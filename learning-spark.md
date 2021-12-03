# Learning Spark 2nd Edition
by Jules S. Damji, Brooke Wenig, Tathagata Das, and Denny Lee

- [Chapter 4](#chapter-4) Spark SQL and DataFrames: Introduction to Built-in Data Sources
- [Chapter 8](#chapter-8) Structured Streaming
- [Chapter 9](#chapter-9) Building Reliable Data Lakes with Apache Spark


## Chapter 4
## Spark SQL and DataFrames Introduction to Built-in Data Sources
- [ ] TODO
## Chapter 8
## Structured Streaming

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

- [ ] TODO

## Chapter 9
## Building Reliable Data Lakes with Apache Spark

Processing logic only solves half of the end-to-end problem of building a pipeline. The choice of storage solution 
determines the end-to-end robustness and performance of the data pipeline.  

### The Importance of an Optimal Storage Solution

Desired properties in a storage solution:
- Scalability and performance: able to scale to the volume and provide the read/write throughput and latency
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
- Support for diverse workloads: unstructured, semi-structured, and structured file formats.
(see [Chapter 4](#chapter-4))
- Support for diverse filesystems: any storage system that supports Hadoop’s FileSystem APIs (de facto standard in the 
big data ecosystem)

#### Limitations of Data Lakes

Data lakes fail to provide ACID guarantees on:
- Atomicity and isolation: data is written in a distributed manner so there's no wat to roll back.
- Consistency: lack of atomicity on failed writes further causes readers to get an inconsistent view of the data.

Work around employed by developers to avoid these limitations have lead to new systems, called _lakehouses_.

### Lakehouses: The Next Step in the Evolution of Storage Solutions

Combines the best elements of data lakes and data warehouses for OLAP workloads
- Transaction support: provide ACID guarantees in the presence of concurrent workloads.
- Schema enforcement and governance: prevent data with an incorrect schema being inserted, table schema can be evolved.
Data integrity, and robust governance and auditing mechanisms.
- Support for diverse data types in open formats: can store, refine, analyze, and access all types of data.
- Support for diverse workloads: variety of tools reading data using open APIs.
- Support for upserts and deletes: allow data to be concurrently deleted and updated with transactional guarantees.
- Data governance: data integrity and audit all the data changes for policy compliance.

Common features:
- Store large volumes of data in structured file formats on scalable filesystems.
- Transaction log to record a timeline of atomic changes to the data.
- Use the log to define versions of the table data and provide snapshot isolation guarantees between readers and writers.
- Support reading/writing using Apache Spark.

#### Apache Hudi

Data storage format that is designed for incremental upserts and deletes over key/value-style data. Combination of 
columnar formats and row-based formats.

#### Apache Iceberg

Open storage format for huge data sets and focuses on general-purpose data storage that scales to petabytes in a single 
table and has schema evolution properties.

#### Delta Lake

Open data storage format that provides transactional guarantees and enables schema enforcement and evolution.

### Building Lakehouses with Apache Spark and Delta Lake

How Delta Lake and Apache Spark can be used to build lakehouses

#### Configuring Apache Spark with Delta Lake

One of the following ways:
- Set up an interactive shell: depending on spark version, specific version of delta lake changes
- Set up a standalone Scala/Java project using Maven coordinates: just add the dependency to `pom.xml` file

#### Loading Data into a Delta Lake Table

Migrate existing workloads to delta is very easy, all you need to do is change all the DataFrame read and write 
operations to use `format("delta")`. 

#### Loading Data Streams into a Delta Lake Table

you can easily modify your existing Structured Streaming jobs to write to and read from a Delta Lake table by setting 
the format to `"delta"`.

Delta Lake has a few additional advantages over traditional formats like JSON, Parquet, or ORC:
- It allows writes from both batch and streaming jobs into the same table: advanced metadata management allows both 
batch and streaming data to be written.
- It allows multiple streaming jobs to append data to the same table: metadata maintains transaction information for 
each streaming query.
- It provides ACID guarantees even under concurrent writes: allows concurrent batch and streaming oper‐ ations to write 
data with ACID guarantees.

#### Enforcing Schema on Write to Prevent Data Corruption

The schema is recorded as table-level metadata, so all writes to a table can verify whether the data being written has a
schema compatible. If it is not compatible, an error is thrown and data is not written.

#### Evolving Schemas to Accommodate Changing Data

It is possible that we might want to add this new column to the table and can be done by setting the option 
`"mergeSchema"` to `"true"`.
In Spark 3.0, you can also use the SQL DDL command ALTER TABLE to add and modify columns.

#### Transforming Existing Data

`UPDATE`, `DELETE`, and `MERGE` commands are supported using either DataFrames or tables and each of these ensures ACID 
guarantees.

Real-world use cases:
- Updating data to fix errors: SQL query or with a Delta Lake table updates can be done programmatically. 
- Deleting user-related data: exactly the same as with updates.
- Upserting change data to a table using `merge()`: can upsert changes using the `DeltaTable.merge()` operation, which 
is based on the MERGE SQL command. If you have a stream, you can continuously apply those changes using a Structured 
Streaming query.
- Deduplicating data while inserting using insert-only merge: merge operation in Delta Lake supports an extended syntax:
delete actions, clause conditions, optional actions and star syntax. For more details and examples see the 
[documentation](https://docs.delta.io/latest/delta-update.html#upsert-into-a-table-using-merge)

#### Auditing Data Changes with Operation History

All the changes to your Delta Lake table are recorded as commits in the table’s transaction log and every operation is 
automatically versioned.

#### Querying Previous Snapshots of a Table with Time Travel

You can query previous versioned snapshots of a table by using theDataFrameReader options `versionAsOf` and 
`timestampAsOf`.