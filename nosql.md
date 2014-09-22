# NoSQL

## [NoSQL Cloud computing and fast IP](http://nosqltapes.com/video/benjamin-black-on-nosql-cloud-computing-and-fast_ip)

How to best build infrastructure to be efficient to build and operate? Once you recognize it, implies a bunch of things how software can operate on it knowing those boundaries.

Lots of software gets built ignoring undelying infrastructure constraints and not embracing them at all. Constraints should be considered when architecting.

Abstractions are not good or bad, but should embrace underlying reality, not deny it. Need dictates how do you implement. 

We tend to judge quality of a product by who does use it: ex.: Google, Facebook, etc. We should not judge a product as a failure if dropped by the creators: not using it anymore does not mean a product failure: running it three years in production means a great win. Changes may refer to different needs. Published papers are interesting and instructive but not roadmaps for development; and are years behind current state.

**Tuning: is one of most important NoSQL features the default performance achieved?**

Is important to have good defaults in the product. Default settings should not consider just one aspect: ex.: performance disgregarding security. 

The real power of NoSQL is the flexibility rather than scalability? There is no one thing known as NoSQL: if you pick a database that is well suited to what you are trying to achieve, you can get a great a spectacular behavior. If there is a *mismatch in the data model, you will deal with a lot of pain*. By making something purpose built, you get orders of magnitude performance improvements.

NoSQL is not a remedy for performance: usually people perceive performance problems, and want to try NoSQL but did not perform any tunning on current platform before and any tunning concepts are alien to them. Hitting a bottleneck with default settings and not performing any tunning, does not justify changing the database: in a future, when you deal with another bottleneck, you will need to perform tunning. In those cases, the solution is not to change the database, but to learn how to deal with it in depth.

**Benchmarks ...**

It is hard to do benchmarking, if you want to compare objectively. For marketing purposes, is easy. For objective benchmarks you need to compare tools that are comparable, have correct settings, and use cases are comparable.
By making something purpose built, you get orders of magnitude performance improvements.

**Why NoSQL?**

People feel threatened and need to have everything distributed. Concepts are simple, but complexity is in scale.

Marketing features is a problem: ex.: replication checkbox does not reflect how that replication is built, which makes whole difference on the system.

Sharding and replica sets show that the distributed mode is not inherent to the database. On the opposite side, you have databases as Riak, where you just specify the amount of copies required, you have a leader election and once you come back from a network partition, you have a clearly defined behavior.

**Lack of standarization**

People came to notice that makes no sense to have same query language for graph and document databases, but makes sense ex.: to have a standard for document databases, and a standard for graph databases.

People tend to have an utilitarian understanding of things, and not do not even bother to understand how it really works; the underpinnings of a language and system.

First important thing is to understand own platform and see what can be tuned.

An indicator that you are doing something really interesting, is that you need to be using more than a database.

## [NoSQL at Fermilab](http://nosqltapes.com/video/nosql-at-fermilab)

NoSQL technologies at Fermilab and LHC
