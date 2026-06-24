# Misc. Notes

## Problems

- aggregate functions are not allowed in WHERE
- having agg(\*) $\neq$ 10

- Example:
  > $B_k=\{3,4,6\}$
  > $\text{tuple-world}_1=\{3,6\}$
  > $\text{tuple-world}_2=\{4,6\}$
  > because of this particular subset $B_k$ does not satisfy $\text{agg}(*)\neq10$

## Ideas

- Is the query result determined by only k clusters?
- Which clusters have highest influence?
- which clustering(.. embedding) is best? merge learning techniques with provenance techniques.
- Many structural questions about the uncertain database become questions about the cluster hypergraph:

  > Is the hypergraph linear?
  > Does it contain a forbidden/wanted patterns?
  > Does it satisfies some hereditary property?
  > How many clusters must be modified to eliminate all bad configurations?

- Can we allow techniques from extremal combinatorics and property testing to be applied directly to this uncertainty model.

---

## Tasks

- [] clear clutter and define semantics for vector databases.
- [] add non-monotone Example
- [] write motivation:
  > rdbms to clusters
  > vector databases to clusters add information to existing embeddings

---

## Hypergraph View of Clusters

Tuples:

$$
T = \{t_1,t_2,t_3,t_4,t_5\}.
$$

Clusters/Blocks:

$$
C_1 = \{t_1,t_2,t_3\},
$$

$$
C_2 = \{t_2,t_4\},
$$

$$
C_3 = \{t_3,t_4,t_5\}.
$$

eachCluster is a hyperedge and that gives us a hypergraph:

$$
H = (V,E)
$$

$$
V = \{t_1,t_2,t_3,t_4,t_5\}
$$

$$
E = \{C_1,C_2,C_3\}.
$$

ASCII diagramof H:

```text
t1 -----\
         \
          C1
         /
t2 -----/

t2 ----- C2 ----- t4

t3 -----\
         \
          C3
         /
t4 -----/

         \
          t5
```

A possible world is obtained by choosing which clusters are active.

For example:

| Active Clusters | Present Tuples |
| --------------- | -------------- |
| $C_1$           | $t_1,t_2,t_3$  |
| $C_2$           | $t_2,t_4$      |
| $C_3$           | $t_3,t_4,t_5$  |

If $C_1$ and $C_3$ are active, then the world contains

$$
\{t_1,t_2,t_3,t_4,t_5\}.
$$

If only $C_2$ is active, then the world contains

$$
\{t_2,t_4\}.
$$

---

### Example Property: Linearity

A hypergraph is **linear** if any two hyperedges intersect in at most one vertex:

$$
|C_i \cap C_j| \leq 1
$$

for all $i \neq j$.

In the example,

$$
C_1 \cap C_2 = \{t_2\},
$$

$$
C_1 \cap C_3 = \{t_3\},
$$

$$
C_2 \cap C_3 = \{t_4\},
$$

so the hypergraph is linear.

If instead

$$
C_2 = \{t_2,t_3,t_4\},
$$

then

$$
C_1 \cap C_2 = \{t_2,t_3\},
$$

and that violates linearity.

---
