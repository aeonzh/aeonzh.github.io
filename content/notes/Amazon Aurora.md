---
aliases: 
date: 2020-07-15
description: 
published: true
keywords: 
layout: note
title: Amazon Aurora
---
# Why?
Disaster recovery

[Aurora PostgreSQL Disaster Recovery solutions using Amazon Aurora Global Database | Amazon Web Services](https://aws.amazon.com/blogs/database/aurora-postgresql-disaster-recovery-solutions-using-amazon-aurora-global-database/)

Takeaway from above: *PostgreSQL logical replication* and the *storage-based replication* that Aurora Global Database uses have a few key differences. Logical replication uses native PostgreSQL replication slots to record data-modifying statements or row changes on the replication source (primary) and reapply them on the replication target (replica). The primary and replica databases are separate and independent and can contain different datasets.

# What Aurora offers
- MySQL and PostgreSQL compatibility
- Involves **clusters** instead of single instances. This potentially allows different roles on different instances
- Connect to it via **endpoints**

> storage costs are based on the storage "high water mark" (the maximum amount that was allocated for the Aurora cluster at any point in time)

# Aurora Global Database for disaster recovery
[Amazon Aurora Global Database](https://aws.amazon.com/rds/aurora/global-database/)

[Working with Amazon Aurora Global Database](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database.html)

# Security
[Security with Amazon Aurora PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.Security.html)

# Aurora serverless
Use cases: Infrequent/Variable/Unpredictable/Development and testing: e.g. new application; same application, many tenants

# So far, from my understanding:
- You have Postgres instances based on a **snapshots** for each replica across AZs and regions
- In case one AZ/region goes down you can promote the replica to read-write
- You would need to manually point to each RDS instance host

# The takeaways with Aurora:
- Computing and storage are separated
- **By default the data is shared across AZs**
- Idk, I guess this helps with performance across AZs? I assume spinning up just an instance with a process to make it read from some volume is a little bit faster to spin up an instance with a postgres process and the data
- I learned there exist **physical replicas** (storage layer) and **logical replicas** (db engine). Logical replicas basically re-applies the database modifications to a new database. Physical replicas are sort of literally the same database. Aurora does the former, I assume because of the storage nature? There is **Aurora Global Database** for cross-region replicas.
- "You can typically promote a secondary cluster and make it available for writes in under a minute."
- With **endpoints** you don't have to point to the single hostnames, AWS does it for you, hence a little bit of management relief (I believe)

# Question I still have
- A part from the fact that Aurora, due the infrastructure is faster than traditional RDS. Conceptually, having cross-region RDS replicas and using Aurora Global Database are the same?  
*Update after some months of use:* the result would be very similar, the gains would be in terms of performance (storage-only clones VS creating entire instance replicas)
