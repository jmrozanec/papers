# [RethinkDB](http://nosqltapes.com/video/slava-akhmechet-and-mike-glukhovsky-on-rethinkdb-modern-hardware-and-nosql-pricing-models)

The product aims to optimize software for storage in SSDs. 

Every SSD behaves differently and you need a different workload for each chip. They capture the user workload and transform it to the optimal workload for the SSD disk. 

The product is an opensource distributed database that stores json documents and also allows to perform joins. Does not affer ACID guarantees: favours consistency over availability (CID). Transactions are considered at document level. Provides a querying language (ReQL) modeled after functional languages. Lambda functions allow complex algorithms to be decomposed into constituent parts and functions compound to perform complex queries.

## Recommended papers
- [Log structured filesystems](http://web.stanford.edu/~ouster/cgi-bin/papers/lfs.pdf)
- [What every programmed should know about memories](http://www.cs.bgu.ac.il/~os142/wiki.files/drepper-2007.pdf)
