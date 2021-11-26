# Learning Spark 2nd Edition
by Jules S. Damji, Brooke Wenig, Tathagata Das, and Denny Lee

- [Chapter 8 Structured Streaming](#chapter-8-structured-streaming)


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
