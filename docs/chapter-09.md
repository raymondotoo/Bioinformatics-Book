# Chapter 9: Genome Assembly and Annotation

## 9.1 The Jigsaw Puzzle

When we sequence a genome, we do not read the chromosome from start to finish. Current technology cannot do that. Instead, we break the DNA into millions of tiny pieces, sequence them, and then try to put them back together.

This is **Genome Assembly**.

Imagine shredding 100 copies of the *New York Times*, mixing them up, and trying to reconstruct the Sunday edition.

## 9.2 Key Concepts in Assembly

### Reads
The raw, short sequences that come off the machine (e.g., 150 letters long).

### Coverage (Depth)
The average number of times a specific base in the genome was sequenced.
*   If a genome is 100 bases long, and you have 3000 bases of data, you have **30x coverage**. Higher coverage gives higher confidence.

### Contigs and Scaffolds
1.  **Contig:** A continuous sequence formed by overlapping reads. (A completed puzzle section).
2.  **Scaffold:** Contigs connected by gaps of known length. (Knowing that the "Sports" section comes after "Business", even if you are missing the page in between).

### Repeats: The Villain
Genomes are full of repetitive sequences (e.g., `ATATAT...` for thousands of bases). If a read is shorter than the repeat, the assembler doesn't know where it belongs. This is the hardest part of assembly.

## 9.3 Assessing Quality: N50

How do we know if an assembly is "good"? We use a metric called **N50**.

Imagine lining up all your contigs from longest to shortest. Walk down the line until you have covered 50% of the total genome length. The length of the contig you are standing on is the N50.
*   **High N50** = Good (Long, continuous pieces).
*   **Low N50** = Bad (Fragmented, tiny pieces).

## 9.4 Genome Annotation

Once you have the sequence, you need to find the landmarks. **Annotation** is the process of identifying genes and features.

*   **Ab Initio:** Using algorithms to find "gene-like" patterns (Start codon ... ORF ... Stop codon).
*   **Homology-Based:** Aligning known proteins from other species to your new genome to find matches.

## 9.5 Bioinformatics in Action: Calculating N50

Let's write a function to calculate N50 from a list of contig lengths.

```python
def calculate_n50(contig_lengths):
    """Calculates the N50 metric for a list of contig lengths."""
    # 1. Sort lengths in descending order
    contig_lengths.sort(reverse=True)
    
    # 2. Calculate total genome size
    total_size = sum(contig_lengths)
    
    # 3. Find the threshold (50% of total size)
    threshold = total_size / 2
    
    # 4. Walk down the list
    current_sum = 0
    for length in contig_lengths:
        current_sum += length
        if current_sum >= threshold:
            return length
    return 0

# Example: A fragmented assembly
contigs = [100, 300, 500, 50, 20, 800] 
# Sorted: 800, 500, 300, 100, 50, 20. Total = 1770. Half = 885.
# 800 < 885
# 800 + 500 = 1300 (> 885). So N50 is 500.

n50_val = calculate_n50(contigs)
print(f"N50: {n50_val}")
```

**Output:**
```text
N50: 500
```

## Summary

Genome assembly stitches short reads into long **contigs**. We use metrics like **N50** to judge the quality. Finally, **annotation** turns the raw sequence into a map of genes and functions.