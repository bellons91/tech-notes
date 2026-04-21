---
title: "Hadoop"
tags:
  - hadoop
  - big-data
  - distributed-systems
  - hdfs
  - mapreduce
  - batch-processing
aliases:
  - Apache Hadoop
---

**Hadoop** is an open-source stack for storing and processing very large datasets across a cluster.  

## Summary

- Hadoop is often described as a **full platform**: [[HDFS]] for distributed storage, [[YARN]] for resource management, and [[MapReduce]] as a classic batch processing model.
- **MapReduce** persists **intermediate results to disk** between map and reduce phases, which favors durability and recovery but increases **disk I/O** and latency compared with in-memory engines.
- **Fault tolerance** is characterized as strong for disk-oriented pipelines because work is materialized on disk, so failed steps can be recovered from persisted stages.
- For **cost**, disk is typically cheaper than RAM at scale; Hadoop is often framed as more **budget-friendly** when the workload fits heavy disk use and large sequential batch jobs.
- **Batch processing** (high volume, higher latency) is the primary sweet spot; it is less flexible than Spark for near-real-time or interactive workloads.
- Spark is frequently deployed **alongside** Hadoop (same HDFS/YARN), replacing or complementing MapReduce rather than the whole ecosystem.

## Details

### Ecosystem components

| Piece | Role |
| --- | --- |
| HDFS | Distributed file system for huge files across nodes |
| YARN | Schedules cluster resources for applications |
| MapReduce | Programming model for parallel batch jobs with map/shuffle/reduce stages |

### Comparison axis (vs Spark)

Disk-centric MapReduce favors **durability** and straightforward replay from persisted intermediates. [[Apache Spark]] emphasizes **in-memory** computation and lineage-based recovery, which the same source positions as much faster for many workloads but more RAM-intensive.

## Related

- [[Apache Spark]]
- [[Apache Cassandra]]

## Sources

- [Mastering Distributed Systems: A Deep Dive into Hadoop vs. Apache Spark](https://medium.com/@iclalaca.ai/mastering-distributed-systems-a-deep-dive-into-hadoop-vs-apache-spark-8ef8e9ee17f1)
