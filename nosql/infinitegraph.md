# [Infinitegraph](http://nosqltapes.com/video/wood-davidson-infinitegraph)

Was built taking a lot of functionality from Objectivity out, focusing on the graph focused API, an indexing package and a navigation package, with rules to navigate the graph. Has a pluggable architecture: offers possibility for people to write own functions to be executed in infinitegraph.

The database is distributed two ways: in storage and computations (for queries).The difficult part is to do the algorithm in a distributed way and assembly the results. The need to distribute is due to algorithms being expensive to compute and also required memory while computation is being done.

APIs are provided in Java. Objects are stored in a binary format, that is optimize to persist into disc.
Language bindings are relatively easy to develop: are thin. Underneath, the database is developed in C++.

Graph databases are new, but problems are not. People are dealing with petabytes of data in a distributed environment. Domains: networks, social data, security attacks (you analyze from where do come and how they spread), people knowledge value: who has the most value in a particular topici, recommendation engines.
