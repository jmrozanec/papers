# [Riak & distributed systems](http://nosqltapes.com/video/justin-sheehy-on-riak-distributed-systems)

Originally we just developed web applications and built Riak predecessor to support our applications.

Key value store inspired on Dynamo, but quite different since there are multiple components not described on the [original paper](http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf).

Riak, the product, is a distributed database, focused on HA, linear scalability and ease of use. Can be used as key value store, though supports mapreduce, link walking and some other features.

**Ideal case for Riak?**

When you need to grow at linear rate.

Behaviour and specially failure behaviour of machines is different at different at different scales. Sometimes abstracting over those levels is convenient, but sometimes not.

Riak is a distributed network, and all hosts are equal: every host can accept a write and contributes to the storage pool. Adding a node you contribute throughput and capacity. When a requests hits any node in a Riak cluster uses consistent hashing and virtual node techniques to figure out which other nodes would be involved in the request.

It is very easy to have load balancers, since there is no central point in the cluster.

Riak core does not know anything about key value store, but just about protocols, gossip, the ring. Just around that you have the dynamo like key value pairs that do not know anything about protocols and up to that you expose APIs (http, etc)

Quorums require to ensure n writes were performed before agreeing a transaction was performed; or before returning a value read to ensure the value is the correct one.

By building a general purpose distributed system that supports HA, we can look at usual problems and create new layers on top of it to satisfy those needs.

**Interesting points**

- NoSQL models are being researched for geographical data
- In some cases the line between online querying and warehousing is blurring, since there are cases where a single database does good enough of both to consider separate solutions for each case.
