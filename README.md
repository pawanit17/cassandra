# cassandra

# Introduction
- Developed at Facebook and is a Columnar Database.
- Has its own version of SQL called CQL and is a NOSL database.
- Apache Cassandra is an open source, distributed NoSQL database that began internally at Facebook and was released as an open-source project in July 2008. Cassandra delivers continuous availability (zero downtime), high performance, and linear scalability that modern applications require, while also offering operational simplicity and effortless replication across data centers and geographies. Cassandra can handle petabytes of information and thousands of concurrent operations per second, enabling organizations to manage large amounts of data across hybrid cloud and multi cloud environments.

# Trivia
- Apache Cassandra was developed by Avinash Lakshman and Prashant Malik when both were working as engineers at Facebook. The database was designed to power Facebook’s inbox search feature, making it easy for users to quickly find the conversations and other content they were looking for. The architecture combined the distribution model proposed in Amazon’s Dynamo paper to allow horizontal scaling across multiple nodes with the log-structured storage engine described in Google’s BigTable paper. The result was a highly scalable database that could address the most data-rich and performance-intensive use cases.
- https://www.datastax.com/cassandra

# What does Cassandra offer
:question: How each of the below are achieved?.
- Replication
- Scalability ( Linear scale )
- Zero-downtime
- High performance
- Fault tolerant
- Masterless Architecture
- Tunable consistency
- Column oriented database
- No single point of failure
- Very fast WRITES ( micro to milli seconds ) and READS ( milli seconds )
- Vendor Agnostic

# When to use Cassandra
- Applications where data is heavy - petabytes
- When data is columnar - different fields for different products

# When not to use Cassandra
- Cassandra provides tunable consistency.
  - Configuration parameter.
  - :question: Try this!.
- When data is to be instantly read
- Data managed on a single system
- Ideal for catalog management system and not for order management system.

# Usecases


# How is it different from MongoDB

# How are different databases placed in terms of speed, availability and scalability & replication?.
- https://www.datastax.com/nosql

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

https://www.youtube.com/watch?v=fKV_j7i8KCI
https://www.youtube.com/watch?v=YjYWsN1vek8&list=PL2g2h-wyI4SqCdxdiyi8enEyWvACcUa9R

- 1000s of operations per core.
- Each Node has a full installation of Cassandra.
- Each code has a capacity of 2-4TB.
- All the Nodes are connected and together form a Datacenter.
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
in writing, the WRITE request succeeds otherwise, it fails.
![image](https://user-images.githubusercontent.com/42272776/134802669-e5dcf8cb-1879-4523-9424-ae9ae5ac2efe.png)
- The same is the case with READs.
![image](https://user-images.githubusercontent.com/42272776/134802680-0e86631c-448d-4cc0-9c21-37b0676a2f94.png)

- Geographic distribution works well with Cassandra. So is cloud scheme.
![image](https://user-images.githubusercontent.com/42272776/134802786-d15dfb47-d891-47e9-9549-7c8b7ff7ef85.png)

# How is data stored
| Element      | Description |
| ----------- | ----------- |
| Keyspace      | Similar to schema in RDBMS       |
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






