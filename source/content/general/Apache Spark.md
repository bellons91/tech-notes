---
title: "Apache Spark"
tags:
  - apache-spark
  - big-data
  - distributed-systems
  - in-memory-computing
  - data-engineering
  - batch-processing
aliases:
  - Spark
---

**Apache Spark** is a unified analytics **engine** for large-scale data processing. It is commonly compared to Hadoop’s [[MapReduce]] layer: both target big distributed workloads, but Spark emphasizes **in-memory** execution and a richer API surface. This note distills that contrast and ecosystem fit using the same comparative source as [[Hadoop]].

## Summary

- Spark performs **in-memory processing** for many operations, avoiding repeated disk writes of intermediate data between stages; sources mention its **order-of-magnitude speedups** over MapReduce for suitable jobs (treat as workload-dependent).
- **Fault tolerance** uses [[RDD|RDDs]] (Resilient Distributed Datasets) and **lineage**: the graph of transformations is recorded so lost partitions can be **recomputed** instead of relying only on persisted intermediates.
- Spark is **more flexible** than classic Hadoop MapReduce for **batch**, **micro-batch** (near-real-time), streaming-style workloads, **SQL** (`Spark SQL`), and **machine learning** (`MLlib`), among other libraries.
- Spark is **not a full storage platform** by itself: deployments often use [[HDFS]] for data and [[YARN]] (or other cluster managers) for resources—i.e. Spark can sit **on top of** the [[Hadoop]] ecosystem as a faster execution layer.
- **Cost trade-off**: Spark generally needs **more RAM**; RAM is costlier than disk, so total cost depends on workload, cluster sizing, and how much data fits in memory.
- **Key takeaway** from the source: Spark does not necessarily **replace** Hadoop wholesale; it often **replaces or augments MapReduce** while still using Hadoop-era storage and scheduling.

## Details

### Processing modes (from the article’s taxonomy)

The article situates Spark relative to several processing styles:

| Style | Idea |
| --- | --- |
| Batch | Large chunks on a schedule (hourly/daily) |
| Micro-batch | Very small time windows (seconds), hybrid of batch and stream |
| Stream | Continuous flows, often with windowing |
| Real-time | Very low latency decisions on incoming events |
| Interactive | Ad-hoc queries returning in seconds |

Spark is highlighted as supporting **batch** and **micro-batch** particularly well through its engine and related libraries; always validate latency requirements against your cluster and APIs.

## Related

- [[Hadoop]]
- [[Apache Cassandra]]

## Sources

- [Mastering Distributed Systems: A Deep Dive into Hadoop vs. Apache Spark](https://medium.com/@iclalaca.ai/mastering-distributed-systems-a-deep-dive-into-hadoop-vs-apache-spark-8ef8e9ee17f1)
