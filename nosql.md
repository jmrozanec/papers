# NoSQL

## [NoSQL Cloud computing and fast IP](http://nosqltapes.com/video/benjamin-black-on-nosql-cloud-computing-and-fast_ip)

How to best build infrastructure to be efficient to build and operate? Once you recognize it, implies a bunch of things how software can operate on it knowing those boundaries.

Lots of software gets built ignoring undelying infrastructure constraints and not embracing them at all. Constraints should be considered when architecting.

Abstractions are not good or bad, but should embrace underlying reality, not deny it. 

We tend to judge quality of a product by who does use it: ex.: Google, Facebook, etc. We should not judge a product as a failure if dropped by the creators: running it three years in production is a great win. Changes may refer to different needs. Published papers are not roadmaps for development, and are years behind current state.

Need dictates how do you implement. Incremental failures make that users do not distinguish failures from normal operations.
Papers are interesting and instructive, but no roadmaps and years behind current state.

Have good defaults to avoid anyone being hurt by them.

The real power of NoSQL is the flexibility rather than scalability. There is no one thing known as NoSQL: if you pick a project that is well suited to what you are trying to achieve, you can get a great a spectacular behavior. If there is a mismatch in the data model, you will deal with a lot of pain. NoSQL is not a remedy for performance: usually people perceive performance problems, and want to try NoSQL but did not perform any tunning on current platform before.

Benchmarks ...
It is hard to do benchmarking, if you want to compare objectively. For marketing purposes, is easy. For objective benchmarks you need to compare tools that are comparable, have correct settings, and use cases are comparable.
By making something purpose built, you get orders of magnitude performance improvements.

Most problems solved by NoSQL stores have to do with scalability.

*Misc*
Redis vs. Memcached: redis is for single client, while memcached was thought to deal with multiple clients. Single client, Redis wins, multiple clients, Memcached is best.
