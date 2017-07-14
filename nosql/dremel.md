# [CouchDB & BigCouch](https://static.googleusercontent.com/media/research.google.com/es//pubs/archive/36632.pdf)
1. Introduction
Dremel supports interactive analysis of very large datasets over shared clusters of commodity machines. Can access the data in place and execute queries without translating them to MR jobs, performing in a fraction of time (compared to equivalent MR jobs). Uses the concepts of serving tree (each query gets pushed down and re-written in each step), provides a native SQL like query language and provides a column stripped storage representation that enables to read less data from secondary store and less CPU due to cheap compression.

2. Background
Quickexecution of queries requires interoperation between the query processor and other data management tools. Requires a common storage layer and a shared storage format.

3. Data model
Comprises of atomic types, repeated fields and optional fields.

4. Nested columnar storage
Given two values of a repeated field, we do not know at what ‘level’ the value repeated (e.g., whether these values are from two different records, or two repeated values in the same record). Likewise, given a missing optional field, we do not know which enclosing records were defined explicitly. We define:
- repetition levels: at what repeated field in the field’s path the value has repeated.
- definition levels: how many fields in p that could be undefined (because they are optional or repeated) are actually present in the record
- encoding: each column is stored as a set of blocks. Each block contains the repetition and definition levels (henceforth, simply called levels) and compressed field values. NULLs are not stored explicitly as they are determined by the definition levels.
Assembling records from columnar data efficiently is critical for
record-oriented data processing tools. Given a subset of fields, our goal is to reconstruct the original records as if they contained just the selected fields, with all other fields stripped away. The key idea is this: we create a finite state machine (FSM) that reads the field values and levels for each field, and appends the values sequentially to the output records. 

5. Query language
The language supports nested subqueries, inter and intra-record aggregation, top-k, joins, user-defined functions, etc; some of these features are exemplified in the experimental section.

6. Query execution
- tree architecture: multilevel serving tree: root server receives incoming queries, reads metadata from the tables, and routes the queries to the next level in the serving tree.
- query dispatcher: an execution plan for project-select-aggregate queries consists of a set of iterators that scan input columns in lockstep and emit results of aggregates and scalar functions annotated with the correct repetition and definition levels, bypassing record assembly entirely during query execution. Some Dremel queries, such as top-k and count-distinct, return approximate results using known one-pass algorithms.

