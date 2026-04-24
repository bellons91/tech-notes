---
title: "Open Data Contracts"
tags:
  - data-contracts
  - data-governance
  - data-quality
  - data-mesh
  - semantics
aliases:
  - ODC
  - Open Data Contract
  - ODCS
---

This page summarizes **Open Data Contracts (ODCs)** as described on [Open Data Contract](https://opendatacontract.com/)—expectations between producers and consumers (meaning, quality, security)—and how they fit into a broader operating model. For a **machine-readable YAML standard** often called **ODCS** (Open Data Contract Standard), see the community specification maintained under Bitol / LF AI & Data (linked in Sources).

## Summary

- **Problem:** Pipelines are fragile; upstream changes often break downstream work; debugging and blame cycles fall heavily on data engineers; lack of visibility into where data flows slows fixes and hurts revenue when critical pipelines fail.
- **Persona tensions:** Producers want freedom to generate rich data quickly; consumers want fast, reliable data aligned to business needs; engineers want fewer ad hoc requests and more systematic flow—without alignment, quality, ownership, and modeling suffer.
- **Solution metaphor:** Treat producer–consumer alignment like **API handshakes**: explicit rules so systems (and teams) can interoperate reliably.
- **What an ODC is:** Documented, declarative **expectations** (not necessarily a full ontology); enforceable at chosen points; “open” means community-driven standards and customization.
- **Four cornerstone areas:** **Schema** (structure/types), **Semantics** (descriptions, tags, integrity checks), **Security** (access and data policies), **Business assertions** (quality checks and cadence).
- **Landscape objects:** **Dataview** (physical bridge to sources), **Contract** (typed expectations a dataview may adhere to), **Entity** (logical business object mapped via dataviews/contracts, with dimensions/measures context).
- **Federated ownership (typical):** Data engineers lean on **Dataviews**; domain teams define **Contracts**; business users define **Entities** (measures, dimensions, relations)—with loose boundaries so others can contribute where needed.
- **DOS framing:** Contracts integrate across the **Data Layer**, **Knowledge Layer**, and **Semantic Layer** so metadata, lineage, classification, and modeling can carry expectations downstream.

## Details

### Why contracts instead of big-bang rewrites

The site argues ODCs can sit as a **compatibility layer** over existing investments: concrete expectations producers and consumers implement for **backward compatibility**, without forcing a full replacement of existing data infrastructure or constraining how raw data is produced.

### Cornerstones (expectation types)

| Area | Role (high level) |
|------|-------------------|
| Schema | Column names, data types |
| Semantics | Descriptions, tags (link to taxonomy/governance), integrity checks |
| Security | Access policies, data policies |
| Business assertions | Quality checks, check cadence |

ODCs are described as **well-structured and templated**, logically representing **one entity** at a time; taxonomy sits above and connects through semantics and tags.

### Landscape and responsibilities

- **Dataview:** Concrete slice of physical data (warehouse table, stream topic, view, federated query, etc.).
- **Contract:** Strongly typed expectations (types, meaning, quality, security) the dataview may satisfy to some degree.
- **Entity:** Logical business object; ties to measures, dimensions, and relations for analysis.

**Right-to-left modeling:** Business-side requirements can be declared before data lands in the store; engineers **map** available data to rich models instead of reverse-engineering domain meaning from weak sources.

### Data Operating System layers (as tabulated on the site)

1. **Data Layer:** Address heterogeneous data, SQL access patterns, cataloging, privacy (e.g. ABAC mentioned on the site).
2. **Knowledge Layer:** Lineage, associations, auto-classification, graph-oriented metadata, APIs for augmentation.
3. **Semantic Layer:** Cross-source business modeling, KPIs, anomaly surfacing; contracts let business users **express and enforce expectations** while modeling entities.

## Related

[[Data Mesh]]

## Sources

- [Open Data Contract (conceptual ODC site)](https://opendatacontract.com/)
- [Open Data Contract Standard — reader-friendly specification (ODCS / YAML)](https://bitol-io.github.io/open-data-contract-standard/latest/home/)
