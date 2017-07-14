# [NoSQL Tapes - MongoDB - II part](http://nosqltapes.com/video/dwight-merriman-and-eliot-horowitz-on-the-origins-of-mongodb)
2013 September

*Origins and overview*

Worked on an opensource cloud computing stack, where MongoDB was a data layer. We become really excited about this component and made it a standalone project.
Document oriented.

Most popular use case: manipulate and store data for application servers where you need to answer thousands of tiny queries in milliseconds.

*Basic design goals*

Wanted to build an opensource cloud stack. For the data layer was clear a high degree of automation was required for horizontal scale. Did not find nothing that would allow to scale horizonally on commodity hardware. Things that allowed to do this scalability, leaded to decisions as not to have a schema, store in json.
Sharding in MongoDB was influenced and works similar to model described at Google's Big Table. Another influence was datamodel required to build DoubleClick.
There are two main benefits by using MongoDB: scale and ease of development.

*Architecture*

You have documents and collection of documents. This interoperates with entities very well, since you don't need to perform any data normalization.
The problem with SQL was not about the DBs, but about the ORMs to map objects to databases. This is different with Mongo, since you don't need a document layer so much: in most cases you can interact with driver directly.
MongoDB is currently developed in C++.

Data is stored in bjson (binary json) allows data being stored in a format independent of programming languages and also specified in RFC 4627.

*Thoughts on NoSQL*

No joins nor complex transaction semantics supported. Leaving this two things out, scaling becomes feasible.

Synchronicity, collaboration or standarization between projects?

Remembers to origins of databases, when no SQL standard existed. It will be some point, when standarization will come, but NoSQL databases have different purposes and address different problems. Having multiple database products allows better development of creativity.

NoSQL will take share of the relational space, but not replace.

We see porting of SQL applications to NoSQL, but these is because NoSQL is a better solution for that portion of problems.
