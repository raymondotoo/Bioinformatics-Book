# Chapter 9: Phylogenetics: Understanding Evolutionary Relationships


<div class="download-slides">
📥 <a href="../slides/chapter-08.pptx" download>Download Lecture Slides (PPTX)</a>
</div>

## 9.1 The Tree of Life

"Nothing in biology makes sense except in the light of evolution." - Theodosius Dobzhansky.

<p align="center">
  <img src="../assets/illustrations/figure-template.svg" alt="Illustration of a Phylogenetic Tree">
</p>

For an interactive view of tree manipulation and collapsing, open the interactive demo: [Interactive Phylogenetic Tree](../interactive/phylo.html)

**Phylogenetics** is the study of evolutionary relationships among groups of organisms. We represent these relationships using a **Phylogenetic Tree**.

*   **Leaves (Tips):** The current species or sequences we are analyzing.
*   **Nodes:** The hypothetical common ancestors.
*   **Branches:** The lines connecting nodes. The length often represents time or amount of genetic change.
*   **Root:** The oldest point in the tree, representing the common ancestor of all species in the tree.

## 9.2 Multiple Sequence Alignment (MSA)

Before you can build a tree, you must align your sequences. Since we are comparing more than two, we use **Multiple Sequence Alignment**.

Imagine stacking 10 DNA sequences on top of each other. You need to insert gaps so that the "columns" of the stack align (e.g., all the ancestors' Adenines line up).

*   **Tools:** ClustalW, MUSCLE, MAFFT.

## 9.3 Building the Tree

There are two main approaches to building trees:

1.  **Distance-Based (e.g., Neighbor-Joining):**
    *   Calculate the percent difference between every pair of sequences.
    *   Group the two most similar ones, then the next, until the tree is finished.
    *   *Pros:* Very fast. *Cons:* Less accurate for distant relationships.

2.  **Character-Based (e.g., Maximum Likelihood, Bayesian):**
    *   Uses statistical models of how DNA mutates (e.g., transitions are more common than transversions).
    *   Calculates the probability of the tree given the data.
    *   *Pros:* Highly accurate. *Cons:* Computationally expensive (slow).

## 9.4 Bioinformatics in Action: Drawing a Tree

Biopython can parse tree files (often in "Newick" format) and visualize them.

```python
from Bio import Phylo
from io import StringIO

# A sample tree in Newick format (usually this comes from a file)
# ((Raccoon, Bear), ((Sea_Lion, Seal), ((Monkey, Cat), Weasel)), Dog);
tree_data = "((Raccoon:10, Bear:10):5, ((Sea_Lion:8, Seal:8):4, ((Monkey:15, Cat:15):3, Weasel:12):2):3, Dog:20);"

# Read the tree
handle = StringIO(tree_data)
tree = Phylo.read(handle, "newick")

# Draw it in ASCII art (perfect for the terminal!)
Phylo.draw_ascii(tree)
```

**Output:**
```text
                                            __________________ Raccoon
  _________________________|
 |                         |__________________ Bear
 |
 |                                            ________ Sea_Lion
 |                       ____________________|
 |                      |                    |________ Seal
 |______________________|
 |                      |                     ________________ Monkey
 |                      |____________________|
 |                                           |________________ Cat
 |                                           |
 |                                           ____________ Weasel
 |
 |____________________ Dog
```

## Summary

Phylogenetics allows us to reconstruct the history of life. We start with an **MSA**, choose a method (like **Maximum Likelihood**), and produce a tree that visualizes the evolutionary distance between species.

## 9.5 Model Selection, Tools, and Robustness

Modern phylogenetic practice emphasizes model selection, statistical support, and reproducibility.

- **Model selection:** Use tools like `ModelFinder` (built into `IQ-TREE`) to select substitution models that best fit your MSA.
- **Tree inference:** Popular, fast, and reliable tools include `IQ-TREE` and `RAxML-NG` for Maximum Likelihood trees; `MrBayes` for Bayesian inference.
- **Support values:** Perform bootstrapping (standard or ultrafast bootstrap in `IQ-TREE`) to quantify node support.
- **Visualization:** Use `ETE3`, `FigTree`, or interactive services like `iTOL` to visualize annotated trees.

Example: running `IQ-TREE` with model selection and ultrafast bootstraps:

```bash
# Model selection + ML tree + ultrafast bootstrap (1000 replicates)
iqtree2 -s alignment.fasta -m MFP -B 1000 -T AUTO
```

Practical tips:

- Inspect the MSA for poorly aligned regions and trim them (e.g., `trimAl`) before building trees.
- For large datasets, consider partitioning or using gene/species tree reconciliation methods.
- Share alignment, trees, and commands (e.g., `README` or workflow file) so results are reproducible.