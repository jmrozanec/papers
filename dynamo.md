# [Dynamo](http://nosqltapes.com/video/understanding-dynamo-with-andy-gross)

Is interesting since it took a wide range of concepts of distributed systems and put it into a single one.

## Consistent hashing
- uses a normal hash function, which space is thought as a circle in which computing resources are placed
- you move clockwise between nodes marked in the circle and any object that maps to segment between A and B, is be put into A
- when you add or remove new nodes to the cluster, the objects will just get mapped to another server

Riak divides each segment between two nodes into partitions of equal width. 

## Vector clocks
