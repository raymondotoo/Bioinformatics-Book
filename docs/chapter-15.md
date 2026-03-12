# Chapter 16: Systems Biology: Integrating the 'Omics'


<div class="download-slides">
📥 <a href="../slides/chapter-15.pptx" download>Download Lecture Slides (PPTX)</a>
</div>

## 16.1 Reductionism vs. Holism

Traditional biology is **reductionist**: it breaks things down to study them (e.g., studying one gene at a time).

**Systems Biology** is **holistic**: it studies the interactions between the parts. It views the cell not as a bag of individual parts, but as a complex, interconnected network.

> "The whole is greater than the sum of its parts."

## 16.2 Biological Networks

<p align="center">
  <img src="../assets/illustrations/figure-template.svg" alt="Illustration of Biological Networks">
</p>

## 15.4 Network Analysis and Pathway Enrichment

Systems biology connects molecular entities into networks and pathways. Practical components:

- **Network construction:** Build co-expression or protein–protein interaction networks (WGCNA, STRING interactions).
- **Module detection:** Identify modules/clusters and test for enrichment of pathways or gene ontology terms.
- **Pathway enrichment:** Tools include `g:Profiler`, `ReactomePA`, `clusterProfiler` for pathway over-representation and GSEA approaches.

Best practices:

- Use multiple evidence sources (expression, interaction databases) to build robust networks.
- Correct for multiple testing and report effect sizes, not only p-values.
- Visualize modules with clear legends, colors, and interactive viewers where possible.

We represent these systems using **Graphs** (Networks).
*   **Nodes:** The biological entities (Genes, Proteins, Metabolites).
*   **Edges:** The relationships (Interacts with, Regulates, Converts to).

### Types of Networks
1.  **Protein-Protein Interaction (PPI) Networks:** Who talks to whom? (Physical binding).
2.  **Gene Regulatory Networks (GRN):** Who is the boss? (Transcription factors controlling gene expression).
3.  **Metabolic Networks:** The factory floor. (Enzymes converting Substrate A to Product B).

## 16.3 Network Topology: Hubs and Bottlenecks

Biological networks are not random. They are **Scale-Free Networks**.
*   Most nodes have very few connections.
*   A few nodes (**Hubs**) have a massive number of connections.

**TP53** (the guardian of the genome) is a classic hub protein. If you knock out a random gene, the cell might survive. If you knock out a hub like TP53, the system collapses (often leading to cancer).

## 16.4 Bioinformatics in Action: Network Analysis

We use the Python library `networkx` to analyze these graphs.

```python
import networkx as nx

# Create an empty graph
G = nx.Graph()

# Add interactions (Edges)
# Imagine Protein A interacts with B, C, and D (A is a Hub)
interactions = [
    ("Protein_A", "Protein_B"),
    ("Protein_A", "Protein_C"),
    ("Protein_A", "Protein_D"),
    ("Protein_B", "Protein_C"),
    ("Protein_E", "Protein_F")
]

G.add_edges_from(interactions)

# Calculate "Degree Centrality" (How connected is each node?)
centrality = nx.degree_centrality(G)

# Find the most connected node
most_connected = max(centrality, key=centrality.get)

print("Network Nodes:", G.nodes())
print(f"The Hub is: {most_connected} with score {centrality[most_connected]:.2f}")
```

**Output:**
```text
Network Nodes: ['Protein_A', 'Protein_B', 'Protein_C', 'Protein_D', 'Protein_E', 'Protein_F']
The Hub is: Protein_A with score 0.60
```

## 15.5 Integration

The ultimate goal of systems biology is to integrate data from Genomics, Transcriptomics, Proteomics, and Metabolomics into a single model. This allows us to simulate entire cells (e.g., **Flux Balance Analysis**) to predict how a bacteria will grow or how a drug will affect a human cell.

## Summary

Systems Biology puts the pieces of the puzzle back together. By analyzing **networks** and identifying **hubs**, we understand the organization of life.