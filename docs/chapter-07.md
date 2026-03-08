# Chapter 7: Sequence Alignment

## 7.1 The Most Fundamental Algorithm

If you have two DNA sequences, the first question you usually ask is: "Are they similar?"

**Sequence Alignment** is the process of arranging sequences to identify regions of similarity. This similarity often points to functional, structural, or evolutionary relationships.

*   **Homology:** A binary state. Sequences are either homologous (share a common ancestor) or they are not.
*   **Similarity:** A mathematical quantity (e.g., "85% similar"). We use similarity to infer homology.

## 7.2 Global vs. Local Alignment

### Global Alignment (Needleman-Wunsch)
Attempts to align the *entire* length of two sequences.
*   **Use case:** Comparing two genes that are expected to be roughly the same length and similar overall.

### Local Alignment (Smith-Waterman)
Searches for the most similar *regions* within the sequences, ignoring the rest.
*   **Use case:** Finding a small gene inside a massive chromosome, or finding a shared domain between two otherwise different proteins.

## 7.3 Scoring the Alignment

Computers need a score to decide which alignment is "best".
*   **Match (+):** Reward for identical letters.
*   **Mismatch (-):** Penalty for different letters.
*   **Gap (-):** Penalty for inserting a space (representing an insertion or deletion).

## 7.4 BLAST: The Google of Biology

Running a rigorous alignment (like Smith-Waterman) against millions of sequences is too slow.

**BLAST (Basic Local Alignment Search Tool)** uses a heuristic (shortcut) method. It finds short, perfect matches ("seeds") and extends them. It is incredibly fast and is the standard tool for searching databases.

*   **E-value (Expect Value):** The number of hits one can "expect" to see by chance.
    *   E-value = 0.0: Perfect, statistically significant match.
    *   E-value = 10: Likely random noise.

## 7.5 Bioinformatics in Action: Pairwise Alignment

Let's use Biopython to perform a global alignment.

```python
from Bio import Align

# Create an aligner object
aligner = Align.PairwiseAligner()

# Set the scoring system
aligner.mode = 'global'
aligner.match_score = 1.0
aligner.mismatch_score = -1.0
aligner.open_gap_score = -2.0
aligner.extend_gap_score = -1.0

seq1 = "GATTACA"
seq2 = "GCATGCU"

# Perform alignment
alignments = aligner.align(seq1, seq2)

# Print the best alignment
print(f"Score: {alignments.score}")
print(alignments)
```

**Output:**
```text
Score: 0.0
target            0 GATTACA 7
                  0 |.|T.|. 7
query             0 GCATG-U 6
```

## Summary

Sequence alignment allows us to compare biological strings. **Global alignment** compares whole sequences, while **Local alignment** finds shared parts. **BLAST** is the tool we use to search massive databases.