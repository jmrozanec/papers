# [Marklogic](http://nosqltapes.com/video/eric-bloch-jason-hunter-marklogic)

Marklogic is an enterprise software company building Marklogic server, a purpose built database to handle unstructured information.
Is a document centric database, optimized for xml and freetext documents. Is used for emails and metadata.
Has search and indexes to allow database style queries. Is schemaless, and remembers what it sees and relations between documents. You can load load documents as they are; does not need validations nor DTDs.

Is database, search and application server, all together but not glued together.
Json does not work well for mixed content, example a web page. 
Provides digital content delivery, allowing to present content in specific formats. 

### Industries where already deployed
- publishing/media: ex.: Lexus-Nexus, which has everything lawyers need to do their job (articles, citations, papers, contracts).
- financial services: equities warehousing, to answer complex questions about third parties. 
- social apps

Is closed source and licensed. Built on C++.
Has HTTP admin interfaces, but can be connected directly as a database. Since can be beneficial to run code closer to data, HTTP interfaces provide means to run xquery over data to build your custom tables. Works better for content centric applications and also leverage a rich security model.

Everything is read only, making it easy to cache. MVCC is used. Everything has a creation and deletion time. Versioning APIs allow to store different versions / views of documents over time. You can query documents at a given point in time. You can manage changes as part of a transaction. Marklogic makes sure there are no conflicts on update.

When a query is issues, divides workload into specific backend components, which return the results to be aggregated and presented to the user.

Allows to answer queries not only on content but also on xml elements, which are hasher to be efficient and inverted indexes are kept to be looked up on queries. Each query is decomposed, so that subcomponent conditions can be checked about what conditions require to be true. Allows OLAP queries without cubes and supports range queries.

Is accessible on EC2.

## Some links
- [Marklogic](http://www.marklogic.com/)
- [Marklogic for developers](http://developer.marklogic.com/)
- [MarkMail](http://markmail.org/)
- [Marklogic papers](http://www.marklogic.com/resource-type/whitepapers/)

