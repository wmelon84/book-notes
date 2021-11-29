# Learning Spark 2nd Edition
by Jules S. Damji, Brooke Wenig, Tathagata Das, and Denny Lee

- [Chapter 8 Structured Streaming](#chapter-8-structured-streaming)
- [Chapter 9 Building Reliable Data Lakes with Apache Spark](#chapter-9-building-reliable-data-lakes-with-apache-spark)


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
#### Reading from and Writing to Databases Using Apache Spark
#### Limitations of Databases
### Data Lakes
#### A Brief Introduction to Data Lakes
#### Reading from and Writing to Data Lakes using Apache Spark
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
