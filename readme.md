# Block-level Possible-World Semantics for Relational & Vector Databases

This project implements **block-level (or cluster-level) possible-world semantics** to handle uncertainty in relational and vector databases. By clustering tuples into **semantic blocks**, we efficiently lift tuple-level uncertainty to the block level, enabling fast aggregate computations with provenance tracking.

---

## Overview

Traditional possible-world semantics works at the **tuple-level**, which quickly becomes infeasible for large datasets. This project introduces **block-level possible-worlds**, where tuples are grouped based on semantic similarity, and computations are lifted to blocks of tuples. This reduces computational cost while preserving correctness.

The approach applies to both:

- **Relational databases** – grouping tuples based on attributes or custom feature mappings.
- **Vector databases** – grouping embeddings from numeric, categorical, or textual attributes.

---

## Key Concepts

1. **Semantic Partitioning**
   - Transform tuples into vector representations via a feature map `φ^A`.
   - Cluster vectors deterministically using `g` to form blocks.
   - Each tuple belongs to exactly one block.

2. **Block-world Mapping**
   - Deterministic map `f` sends each tuple-level possible world to the set of blocks containing tuples.
   - The fibres of `f` partition all tuple-level possible worlds.

3. **Lifted Semantics**
   - Aggregate computations and annotations are lifted from tuples to blocks.
   - Block-level expressions compactly represent all underlying tuple-level worlds, enabling **lazy expansion** on demand.

---

## Example (Conceptual)

Given tuples with numeric attributes, we can cluster them into blocks and then compute block-level aggregates:

/\_/\  
( o.o )

> ^ <  
>  / \  
> / \~~~~~
