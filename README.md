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
- Scalability
- Zero-downtime
- High performance
- Fault tolerant
- Masterless Architecture
- Tunable consistency
- Column oriented database
- No single point of failure.

# When to use Cassandra


# How is it different from MongoDB

# How are different databases placed in terms of speed, availability and scalability & replication?.
- https://www.datastax.com/nosql

# Architecture
- Cassandra employs distributed processing. It means that there are several nodes over which the data is split using some criteria.
- However, unlike HBASE, there is no master node which tells information on which node has what data. Any node in the Cassandra cluster can work with a request.
- In this sense, because there is no master node, there is no single point of failure. In other words, a decentralized system.
- This also means it is horizontally scalable.
- Data stored in Cassandra is stored in more than one nodes, making it fault-tolerant.
  - :question: Is this by default?.

- Cassandra is column-oriented.

