# [Scality](http://nosqltapes.com/video/jerome-lecat-on-scality)

Scality was started when they realized multiple email companies had a problem with storage not scaling into the next few years. Email is near realtime since the users want to se the email and related emails on single page, and be able to retrieve it in matter of milliseconds. Requires strong consistency, since no email can be lost.

In a future people will build utility computing: storage power, computing power, etc. which requires to create economies of scale. Notions of virtualization, SaaS and cloud computing move in that direction and are the start of that curve.

The product was original designed for large email service providers that manage more than one million inboxes. Among the requirements were:
- stateless storage system, so that server could hit storage without having notion of volume
- handle the notion of backup without a special application for backup
- application to decide level of security for email (ex.: spam is not worth, one copy is enough; not same for people email)

For key space Scality uses [RING](http://www.scality.com/products/what-is-ring/), so you can have multiple instances and tiers of storage.

**Features and assets**

- Different people have different habits, that is why scality offers a web page and a console to access the database. 
- Everything is flashed to the disc. 
- Object stores are different to filesystem store since it . The filesystem handles the link between the file and the path to it. Some people will have an algorithm that allows to find data without knowing initially where it is. Filesystems handle protection of data against concurrent writes; Scality does the at application level.
- The application decides how to use the key space.
- Metadata

Cloud storage can be enough fast to be used as tier 1 storage.


