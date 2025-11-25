# Assignment 4 Summary - Understanding Deep Learning Textbook

**Student:** Ardavan Mehdizadeh  
**Date:** November 24, 2025

## Chapter Read: Chapter 13 - Graph Neural Networks

I read Chapter 13 on Graph Neural Networks from the *Understanding Deep Learning* textbook. Here's what stood out to me:

---

## Main Concepts I Solidified

The chapter provides a rigorous explanation of why GNNs are needed. The key insight that **graph node ordering is arbitrary**, so any network layer must be **equivariant to node permutations**. This was more mathematically rigorous than what I think we covered in class and helped clarify the fundamental constraints on GNN architectures.

---

## Most Useful Sections

### 1. Section 13.2: Graph Representation

The adjacency matrix properties were eye-opening. I understood that **A^L** counts how many different paths of exactly L steps exist between any two nodes. This explains why stacking GNN layers lets each node "see" further into the graph - layer 1 looks at direct neighbors, layer 2 reaches neighbors-of-neighbors, and so on. Each new layer extends the reach by one connection.
For example, if you have 3 GNN layers, a node can gather information from any other node that's 3 steps away or less.

### 2. Section 13.4: GCN Layers

The chapter walks through how GCN layers work, starting simple and adding complexity:
Basic idea (equation 13.10):
```
H_{k+1} = a[β_k 1^T + Ω_k H_k(A + I)]
```
This says: to update each node's features, add up features from its neighbors (that's the A part) plus its own features (the I part), transform them with weights Ω, and apply an activation function.
The chapter then shows fancier versions like:

Diagonal enhancement: giving the node's own features extra weight compared to neighbors.
Kipf normalization (Section 13.8.4): adjusting the neighbor contributions based on how many connections each node has

These normalization tricks seem relevant for my surface structures research, because  surface atoms at top, bottom and edges have fewer neighbors than bulk atoms, and we probably want to account for that difference in a efficient model.

### 3. Section 13.7: Node Classification

The chapter explains two different scenarios for training GNNs:

**Inductive:** You have many separate graphs to train on, then test on completely new graphs. This is what can be related to my work. We have millions of different structures in training set, and we'll predict properties for new surfaces the model has never seen.
**Transductive:** You have one giant graph where you know labels for some nodes and want to predict labels for other nodes in the same graph.

Even though we're doing inductive learning, the transductive section was helpful because it explains practical problems like:

Graph expansion: When you try to update one node, you need its neighbors, then their neighbors, and the number of nodes explodes quickly
Neighborhood sampling: Solutions like only looking at a random subset of neighbors to keep computation manageable

These issues pop up in PyTorch Geometric's design (like batching strategies), so understanding them helps make sense of why the framework works the way

---

## Key Takeaways

The chapter explains that GNN layers deeper than 2-5 tend to make all nodes look the same (the "over-smoothing" problem). This tells me not to go crazy with depth when building models.

Section 13.8 shows options beyond just adding up neighbor features: 1) Take the average instead of sum. 2) Take the maximum value from neighbors. 3) Use attention to weight important neighbors more.
If the models aren't learning well, these are alternatives to try.

Whether you divide by the number of neighbors, for example weight by connectivity, it can make a big difference in performance.

Figure 13.3 shows graphs as three pieces:

A: which atoms connect to which (adjacency matrix)
X: features for each atom (like element type, position)
E: features for each bond (optional)

This is interesting and it is exactly how PyTorch Geometric stores graphs internally, so now I understand why their Data objects are structured that way.
---

## What I'm Still Unclear On

The **edge graph concept** (Section 13.9) seems relevant for molecular systems where bonds have different types and strengths. I need to think more about whether we need explicit edge features for surface structures or if node features (atomic species, coordination) are sufficient for capturing the relevant physics.