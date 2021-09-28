# cassandra

# Goal
- :target: Get a good idea by 15th of October.

# Resources
| Course      | Description |
| ----------- | ----------- |
| Datastax Cassandra Basic Playlist | https://www.youtube.com/watch?v=YjYWsN1vek8&list=PL2g2h-wyI4SqCdxdiyi8enEyWvACcUa9R |
| Datastax Cassandra Course      | https://www.datastax.com/learn/cassandra-fundamentals/       |
| Cloud Native Workshop - Cassandra Introduction   | https://www.youtube.com/watch?v=VaLwHqAHNtE&list=PLQwtlCoREyoHJDTVHbixHeuJEjXs5E2vO&index=1        |
| Nasser - Discord Movement to Cassandra   | https://www.youtube.com/watch?v=86olupkuLlU |
| Running Apache Cassandra on Docker | https://www.youtube.com/watch?v=fKV_j7i8KCI |
| Cassandra Data Modeling - Consideration @ Netflix | https://www.youtube.com/watch?v=-zyZ35YyT_8 |
| SprintBoot Data + Cassandra | https://www.youtube.com/watch?v=nBoHQOcwPS4 |
| Cassandra: The definitive guide | https://github.com/sunilsoni/Cassandra-Data-Modeling/blob/master/books/Cassandra%20The%20Definitive%20Guide%20Eben%20Hewit.pdf |
| Introduction to Apache Cassandra | https://www.youtube.com/watch?v=B_HTdrTgGNs |


# Introduction
- Developed at Facebook and is a Columnar Database.
- Has its own version of SQL called CQL and is a NOSL database.
- Apache Cassandra is an open source, distributed NoSQL database that began internally at Facebook and was released as an open-source project in July 2008. Cassandra delivers continuous availability (zero downtime), high performance, and linear scalability that modern applications require, while also offering operational simplicity and effortless replication across data centers and geographies. Cassandra can handle petabytes of information and thousands of concurrent operations per second, enabling organizations to manage large amounts of data across hybrid cloud and multi cloud environments.

# Questions
- Read more on columnar storage
- What are tokens
- Are all the records with same partition key stores adjacent in disk space?.
- How to CRUD using API
- What is the concept of Tombstones
- Why are WRITES faster than READS in Cassandra?. How is this dependent on consistency setting?.
- What are commit logs and memtables.
- How do you run Apache Cassandra on Docker?.
- Why is Cassandra fast?.
- Consistency level & Replication Factors dependency
  - All
  - 1
  - Quorum
- If Cassandra uses hashing for identifying where to store data / retrieve data from, then how does it know where to push the data to during replication?.
- What happens if a request reaches a node that does not have the information requested for?. 
- How is it different from MongoDB
- How are different databases placed in terms of speed, availability and scalability & replication?.
  - https://www.datastax.com/nosql
 
# Trivia
- Apache Cassandra was developed by Avinash Lakshman and Prashant Malik when both were working as engineers at Facebook. The database was designed to power Facebook’s inbox search feature, making it easy for users to quickly find the conversations and other content they were looking for. The architecture combined the distribution model proposed in Amazon’s Dynamo paper to allow horizontal scaling across multiple nodes with the log-structured storage engine described in Google’s BigTable paper. The result was a highly scalable database that could address the most data-rich and performance-intensive use cases.
- https://www.datastax.com/cassandra

# What does Cassandra offer
:question: How each of the below are achieved?.
- High Availability
  - Peer to peer architecture with no single point of failure ( masterless architecture )
- Scalability ( Linear scale )
![image](https://user-images.githubusercontent.com/42272776/134966576-1fb82e77-79fb-4f02-9f43-7e0565bb0406.png)
- Zero-downtime
- High performance
- Fault tolerant
  - Via Replication and Tunable consistency
- Column oriented database
- Very fast WRITES ( micro to milli seconds ) and READS ( milli seconds ) / Single digit millisecond response times at any scale.
- Vendor Agnostic

# When to use Cassandra
- Applications where data is heavy - petabytes
- When data is columnar - different fields for different products

# When not to use Cassandra
- Cassandra provides tunable consistency.
  - Configuration parameter that clients must specify on every operation and that allows you to decide how many replicas in the cluster must acknowledge a write operation or respond to a read operation in order to be considered successful.
  - :question: Try this!.
- When data is to be instantly read
- Data managed on a single system
- Ideal for catalog management system and not for order management system.

# Usecases
- ![image](https://user-images.githubusercontent.com/42272776/134814315-00981f59-9f3a-43b3-ad1a-13388824f71c.png)


# Architecture
- Cassandra employs distributed processing. It means that there are several nodes over which the data is split using some criteria.
- However, unlike HBASE, there is no master node which tells information on which node has what data. Any node in the Cassandra cluster can work with a request.
- In this sense, because there is no master node, there is no single point of failure. In other words, a decentralized system.
- Data is then updated from this node to the other nodes.
- This also means it is horizontally scalable.
- Data stored in Cassandra is stored in more than one nodes, making it fault-tolerant.
  - :question: Is this by default?.

- Cassandra is column-oriented.


- D:\Development\apache-cassandra-3.11.10\conf\logback.xml




- 1000s of operations per core.
- Each Node has a full installation of Cassandra.
- Each code has a capacity of 2-4TB.
- All the Nodes are connected and together form a Datacenter/Ring.
- Each Node communicates with other nodes using a protocol called Gossip - to get the status of a node.
- These Datacenters can be put whereever they are needed in the world and can be served.
![image](https://user-images.githubusercontent.com/42272776/134802071-c475b74f-924a-46c1-a4ff-ebcd3788fbfc.png)

- Data in a traditional RDBMs is stored in rows in Tables.
- The Data is partitioned in Cassandra using a partition key - nodes with same partition key stay together.
![image](https://user-images.githubusercontent.com/42272776/134802281-205a5463-d69a-48c2-9c67-4ac7b8d027bf.png)
- The result of one such partitioning can be visualized below.
![image](https://user-images.githubusercontent.com/42272776/134802366-097782c9-5122-4f57-a064-07aabf618295.png)
- Each node has a number assigned to it. This also determines token values. The partition key is basically hashed to obtain a token value.
- This helps during storage and retrieval of data from Nodes.
![image](https://user-images.githubusercontent.com/42272776/134802453-41bdee26-0430-416f-969c-566862933752.png)
- To help with fault tolerance, replication is used.
![image](https://user-images.githubusercontent.com/42272776/134802482-b5f8726a-eeb9-4ca4-a798-bdad86be023f.png)
- Availability, Performance and Consistency
![image](https://user-images.githubusercontent.com/42272776/134802494-111b6e67-3e0a-4239-a4a8-ce823725ef5e.png)
- With a Replication Factor of 3, WRITEs are stored in 3 different Nodes. Consistency tuning plays a major role here. With a Quorum consistency, if 2 out of 3 nodes succeed
in writing, the WRITE request succeeds otherwise, it fails. This is **Immediate Consistency**.
![image](https://user-images.githubusercontent.com/42272776/134802669-e5dcf8cb-1879-4523-9424-ae9ae5ac2efe.png)
- The same is the case with READs.
![image](https://user-images.githubusercontent.com/42272776/134802680-0e86631c-448d-4cc0-9c21-37b0676a2f94.png)

- Geographic distribution works well with Cassandra. So is cloud scheme.
![image](https://user-images.githubusercontent.com/42272776/134802786-d15dfb47-d891-47e9-9549-7c8b7ff7ef85.png)

# Architecture Deep Dive
- Mainly used for geographically distributed applications.
- **Racks** are basically Nodes that reside on the same rack and **Data Center** is typically a collection of racks with a single building.
- ![image](https://user-images.githubusercontent.com/42272776/135122617-08768c70-c2a2-4601-9fe9-f87636335ac8.png).
- OOTB Cassandra comes with a default configuration of a single data center ("DC1") containing a single rack ("RAC1").
- To achieve decentralization and partition tolerance, Cassandra uses a **gossip** protocol. This protocol is mainly by each node to keep track of state information about the other nodes in the cluster and runs every second on the timer.
- ![image](https://user-images.githubusercontent.com/42272776/135123849-9939923f-63b9-4078-acf3-87ea50ebf86f.png)
- What are Snitches?
- The data being stored into Cassandra is **hashed** on its partition key ( by **Partitioners** ) and the resulting token determines which node the data gets saved to.
- Once data gets persisted into Cassandra node as hashed out by the Partitioner, the **Replication** aspect comes into picture.
- There are **replication strategies** that determine where the data is supposed to get replicated to. For example, in the **SimpleStrategy**, replicas are placed at consecutive nodes around the ring starting from the node identified by Partitioners.
- **Consistency Levels** determine how many nodes needs to agree on a READ or a WRITE.
- ![image](https://user-images.githubusercontent.com/42272776/135130023-ef6513a0-931a-4de4-a810-e6882b9c3e63.png)
- Consistency Level is per client. Replication factor is per Keyspace.
- ![image](https://user-images.githubusercontent.com/42272776/135132487-d9c267c5-9fd2-4e5a-902c-be815e9e440d.png)
- All WRITES are first done to the **Commit Log**, which is a crash recoverable mechanism. From the **commit log** the data is pushed to **Memtables**. There will be many Memtables for a given Table, but each Memtable content will always belong to a single table. When the number of objects in Memtable reaches a threshold, the data is flushed to a file called an SSTable.
- ![image](https://user-images.githubusercontent.com/42272776/135134760-14c991a2-a4eb-4d36-b9bc-846f8ff01193.png)
- ![image](https://user-images.githubusercontent.com/42272776/135134192-ea098518-c8dd-4803-91c9-cd112a75236f.png)
- ![image](https://user-images.githubusercontent.com/42272776/135134808-ad08498a-8588-496e-90a5-25fff517aa64.png)
- ![image](https://user-images.githubusercontent.com/42272776/135134939-3281d2f8-ed96-4e93-b658-467f4e68fb2a.png)
- **Hinted Handoff** is a feature in Cassandra where the attempt to WRITE some data that is hashed to a node is offline. In this case, instead of not failing the request, the information is pinned by the Coordinator node so that if it detects that the node has come up during Gossip, it would process that WRITE action. The advantage here is that because a node is temporarily down, the requests are not flooded to the other existing servers thereby creating uneven load.
- org.apache.casandra.db.HintedHandOffManager is the class that manages hinted handoffs internally.

- **Tombstones** is a concept in Cassandra whereby the Delete operation does not delete the data - column or row etc.Instead, a marker called **Tombstone** in its place. This tombstone will have a lifetime after which the data gets deleted. This settings is called **Gabage Collection Grace Seconds**. By default it is 864,000 - 10 days. The purpose of this delay is to give a node that is unavailable, some time to recover.
- **Bloom Filters** Very fast way to test if an element is in a given set. Catch here is that they are probabilistic data structures and may give false positives, but never a false negative. Org.apache.cassandra.utils.BloomFilter class implements this data structure. When a query is performed, Bloom filter is checked first to see if the data exists. If it determines that the element does not exist, then disk is not accessed. Otherwise, disk check is done, thereby acting as a cache and reducing READ times. Bloom filters are on SSTables.





# How is data stored
| Element      | Description |
| ----------- | ----------- |
| Keyspace      | Similar to schema in RDBMS, keeps group of tables together       |
| Column Families | Are tables in RDBMS |
| Partitions   | Partitioning        |
| Partition Key   | This field will be how paritioning is done |
| Clustering Columns   | Collections of columns that are unique. A natural sorting is implictly done by Cassandra during WRITE |
| Data Columns   | Every other field other than Clustering Columns |

![image](https://user-images.githubusercontent.com/42272776/134803381-913c141e-28e6-4de9-8573-74095e7f8798.png)
![image](https://user-images.githubusercontent.com/42272776/134803403-416058bc-7cbf-4127-9c82-d624745a81c6.png)

# Rules for a Good Partition
- Store what you want to retrieve together.
  - Primary Key ((video_id), created_at, comment_id);
    - Most usecases are something like retrieve the comments for a specific video. In this case, partitioning by video_id is logical.
- Avoid large partitions
  - 100k rows per partition or 100MB per partition
  - ![image](https://user-images.githubusercontent.com/42272776/134803714-c4fef79b-e3d6-4f32-8de9-ea89df739792.png)
- Avoid unbounded partitions
  - ![image](https://user-images.githubusercontent.com/42272776/134803764-a5f92208-3786-4163-b0b6-3a0699e9e1d9.png)
- Avoid hot partitions
  - ![image](https://user-images.githubusercontent.com/42272776/134803787-9508734d-c0d8-417d-a64c-bf278ed3a2a6.png)

# CQL
- Subset of SQL
- desc KEYSPACES;
- use killrvideo;
- // Users keyed by city
  CREATE TABLE IF NOT EXISTS users_by_city ( 
    city text, 
    last_name text, 
    first_name text, 
    address text, 
    email text, 
    PRIMARY KEY ((city), last_name, first_name, email));

# Data Modelling
- ![image](https://user-images.githubusercontent.com/42272776/134805568-944b61f0-7648-46e2-b85f-ac5451bc6184.png)
- ![image](https://user-images.githubusercontent.com/42272776/134805602-6f364123-9992-47f2-a014-e2a68b763e84.png)
- Convention in Cassandra is to use _x_by_y_.
- ![image](https://user-images.githubusercontent.com/42272776/134805640-e1d4891b-18b8-45d2-8fb2-90f60b740169.png)
- Optimization by combining Time + ID ![image](https://user-images.githubusercontent.com/42272776/134805687-7707be20-2b00-4736-ace8-93cc268162c7.png)
- **You can do a single read to get the data that answers the questions. Cassandra is denormalized to achieve faster reads.**
- ![image](https://user-images.githubusercontent.com/42272776/134805719-37f06c58-820b-47d9-bf90-bed431362392.png)
- The advantage is if we retrieve it, not only we get the relevant partitioned data, but also the ordering is intact.
- **One query per one table**.

# CRUD
- Create
  - CREATE TABLE IF NOT EXISTS comments_by_user (
    userid uuid,
    commentid timeuuid,
    videoid uuid,
    comment text,
    PRIMARY KEY ((userid), commentid)
    ) WITH CLUSTERING ORDER BY (commentid DESC);
    
  - INSERT INTO comments_by_user (
    userid, //uuid: unique id for a user
    commentid, //timeuuid: unique uuid + timestamp
    videoid, //uuid: id for a given video
    comment //text: the comment text
    )
    VALUES (
      11111111-1111-1111-1111-111111111111, 
      NOW(), 
      12345678-1234-1111-1111-111111111111, 
      'I so grew up in the 80''s'
    );
 
- Read
  - SELECT * FROM comments_by_user WHERE userid = 11111111-1111-1111-1111-111111111111;
  - **Note that a straight select * without specifying partion key on a realistic production cluster would cause a full scan and is highly discouraged.**

- Update
  - UPDATE comments_by_video 
    SET comment = 'OMG that guy Patrick is on fleek' 
    WHERE videoid = 12345678-1234-1111-1111-111111111111 AND commentid = 494a3f00-e966-11ea-84bf-83e48ffdc8ac;

- Delete
  - DELETE FROM comments_by_video 
    WHERE videoid = 12345678-1234-1111-1111-111111111111 AND commentid = 494a3f00-e966-11ea-84bf-83e48ffdc8ac;
  - In Cassandra, Delete actually uses Insert as it creates a Delete Marker called Tombstone.





