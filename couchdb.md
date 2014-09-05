CouchDB & BigCouch

BigCouch
First C in Couch means cluster. Looking at objectives, started by getting involved on its scalability. BigCouch is available as a fork at Github and in a future will be merged back into CouchDB.

Cloudant offers shared, multitenant clusters where users can start for free.

*Design goals when creating Cloudant*
Create a platform where you would be able to put your date from an application.
The sweatpot are applications where data changes quickly but queries remain the same. Example: sensor data, where there is a lot of incoming data, but queries for aggregations are the same over time.
Everything is append only: always data is added to the files, never deleted, so no locks are needed and reading is never interrupted. MVCC is implemented, so never locks.
There is no need to implement database journals, since the journal is the databa
se itself. After a crash, you just pick the file. For corruption, we rely on har
dware.
Is implemented in Erlang, which provides a good support for concurrency and provides a good distribution mechanism. Processes living in different machines have same code as if run on single machine, allowing to build complex distributed systems without the need to deal with TCP/IP complexity.
If you want to do more than key-value storage, you can create map reduce jobs in JavaScript.
Is adding support for multiple document edit branches, what means that knows how to handle conflicting versions and store them to present them to the user. CouchDB replication can synchronize document versions to a crashed node once is up again.

*The feature that you are proudest for?*
Stability. Is not a feature, but a badge. The system has builtin fault tolerance and redundandy, keeping data always safe.

*Cool use cases they have seen:*
- replicating on cloudant a local couchDB store
- use cloudant to replicate couchDB data to each user instance


