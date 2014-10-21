# [MillWheel: fault tolerant stream processing at intenet scale](http://static.googleusercontent.com/media/research.google.com/sl//pubs/archive/41378.pdf)
## Abstract
MillWheel is a framework for building low-latency data-processing applications widely used at Google. Users specify a directed computation graph and application code for individual nodes, and the system manages persistent state and the continuous flow of records, all within the envelope of the framework's fault tolerance guarantees.

## 1. Introduction
Contributions are a programming model and implementation for the MillWheel framework:
- designed a programming mode that allosw complex straming systems to be created without distributed systems expertise
- build an efficient implementation of the MillWheel framework that proves its viability as both scalable and fault tolerant system

## 2. Motivations and requirements
- persistent storage: requires short and long term storage
- low watermarks: tracks all pending events in the distributed system. If a low watermark advances past time without queries arriving, then there is confidence queries were not recorded, not just delayed. Out of order streams are the norm.
- duplicate prevention: framework provides the feature. Other requirements for stream processing are:
 - data should be available to consumers as sson is published
 - persistent state abstractions should be available to user code and integrated into systems overall consistency model
 - out of order data should be handled gracefully by the system
 - monotonically increasing low watermark of data timestamps should be computed by the system
 - latency should stay constant as the system scales to more machines
 - should provide once delivery of records

## 3. System overview
MillWheel is a graph of user-defined transformations / computations. Each of these transofrmations can be parallelized across an arbitrary number of machines, such that the users do not need to concern with load balancing.
- Inputs and outputs are represented by tripes: key, value, timestamp.
- Record processing is idempotent: as lng as the applications use the state and communication abstractions, failures and retries are hidden from user code.
- Delivery guarantee: all internal updates resulting from record processing are atomically checkpointed per key and records are delivered once.

## 4. Core concepts
- computations: application logic lives in computations. Is invoked upon receipt of input data, at which point user-defined actions are triggered.
- keys: are the primary abstraction for aggregation and comparison between different records.
- streams: are delivery mechanism between computations. A computation may receive and publish from/to one or more streams.
- persistent state: is an opaque string managed on a per key basis. The user provides seriablization / deserialization routines. Persistent state is backed by a replicated, highly available data store.
- low watermarks: provides a bound on the timestamps of future records arriving at that computation. min(oldest work at A, low watermark of C:C outputs to A). If there are no input streams, the low watermark and oldest work values are equivalent.
- timers: per key programmatic hooks that trigger at a specific wall time or low watermark value.

## 6. Fault tolerance
- delivery guarantees: much of the conceptual ability of MillWheel's programming model hinges upon the ability to take non-idempotent user code and run it as if it were idempotent. By removing this requirement from computation authors, they are relieved from a significant implementation burden.
 - exactly-once delivery:
  - record is checked against record is checked agains deduplication data from previous records. A Bloom filter of know record fingerprints is used for this.
  - user code is run for the input record, possibly resulting in pending changes to timers, state and productions
  - pending changes are committed to the backing store
  - senders are ACKd
  - pending downstream productions are sent
 - strong productions: produced records are checkpointed before delivery in the same atomic write as state modification.
 - weak productions: rather than checkpointing record productions before delivery, we broadcast downstream deliveries optimistically, prior to persisting state.

- state manipulation:
 - requires to ensure the system does not loose data
 - updates to state must obey once semantics
 - all persisted data throughout the system must be consistent at any given point in time
 - low watermarks must reflect all pending state in the system
 - timers must fire in-order for a given key
