# Chapter 14: Microbiomics: Analyzing Microbial Communities

## 14.1 We Are Not Alone

You are more bacteria than human. The **Microbiome** refers to the trillions of microorganisms living in and on us (and in the environment). These communities affect digestion, immunity, and even mental health.

**Microbiomics** (or Metagenomics) is the study of these communities.

## 14.2 16S rRNA: The Barcode of Bacteria

To identify which bacteria are present, we don't sequence their whole genomes. We sequence one specific gene: **16S rRNA**.

*   **Universal:** All bacteria have it.
*   **Variable:** It has specific regions (V3, V4) that are different between species.

By sequencing this "barcode," we can identify the bacteria without growing them in a lab.

## 14.3 The QIIME 2 Workflow

**QIIME 2** (Quantitative Insights Into Microbial Ecology) is the industry-standard command-line platform for this analysis.

1.  **Import Data:** Load FASTQ files.
2.  **Denoising (DADA2):** Correct sequencing errors and group identical sequences into **ASVs (Amplicon Sequence Variants)**.
3.  **Taxonomy Assignment:** Compare ASVs to a database (like **Silva** or **Greengenes**) to give them names (e.g., *E. coli*).
4.  **Diversity Analysis:** Calculate how diverse the samples are.

## 14.4 Diversity: Alpha vs. Beta

<p align="center">
    <img src="../assets/illustrations/figure-template.svg" alt="Illustration of Microbiome Diversity">
</p>

## 13.4 Modern Microbiome Methods and Best Practices

Microbiome research can use targeted marker gene sequencing (16S) or whole-metagenome shotgun sequencing. Key practices:

- **DADA2 / Deblur:** Use amplicon denoising (DADA2) rather than OTU clustering for higher resolution.
- **QIIME2:** A full ecosystem for 16S processing, visualization, and reproducible pipelines.
- **Shotgun metagenomics:** Provides species- and strain-level resolution and functional profiling (e.g., HUMAnN).

Analysis considerations:

- **Contamination control:** Include blanks and negative controls; use `decontam` to identify contaminants.
- **Compositional data:** Use compositional-aware methods (ALDEx2, DESeq2 with caution) and transform data (CLR) before multivariate analyses.
- **Diversity metrics:** Alpha (within-sample) and Beta (between-sample) are standard; use rarefaction carefully and prefer robust normalization methods.

Data sharing:

- Deposit raw reads in SRA/ENA and provide sample metadata in standard formats (MIxS). Provide analysis notebooks and environment files for reproducibility.

This is the most important concept in microbiome analysis.

### Alpha Diversity (Within Sample)
"How many different species are in *this* sample?"
*   **Richness:** Count of species.
*   **Shannon Entropy:** Accounts for both richness and evenness (abundance).

### Beta Diversity (Between Samples)
"How different is the community in Sample A compared to Sample B?"
*   **Jaccard Index:** Based on presence/absence.
*   **Bray-Curtis:** Based on abundance.
*   **UniFrac:** Based on the phylogenetic distance between bacteria.

## 14.5 Bioinformatics in Action: Calculating Alpha Diversity

While QIIME 2 does this on a massive scale, let's write a Python function to understand the math behind **Shannon Entropy**, a common Alpha Diversity metric.

$$ H = - \sum p_i \ln(p_i) $$

Where $p_i$ is the proportion of the total population made up of species $i$.

```python
import math

def calculate_shannon_entropy(counts):
    """Calculates Shannon Entropy (Alpha Diversity) for a list of species counts."""
    total = sum(counts)
    if total == 0:
        return 0.0
    
    entropy = 0.0
    for count in counts:
        if count > 0:
            # Calculate proportion (p)
            p = count / total
            # Add to entropy sum
            entropy -= p * math.log2(p)
            
    return entropy

# Example:
# Sample A: Very diverse (even spread)
sample_A = [10, 10, 10, 10] 

# Sample B: Low diversity (dominated by one species)
sample_B = [37, 1, 1, 1]

entropy_A = calculate_shannon_entropy(sample_A)
entropy_B = calculate_shannon_entropy(sample_B)

print(f"Sample A (Diverse): {entropy_A:.2f}")
print(f"Sample B (Dominated): {entropy_B:.2f}")
```

**Output:**
```text
Sample A (Diverse): 2.00
Sample B (Dominated): 0.56
```

Higher entropy means higher diversity!

## Summary

Microbiomics uses the **16S rRNA** gene to identify bacteria. We use tools like **QIIME 2** to process reads into **ASVs**. We then compare communities using **Alpha Diversity** (richness within a sample) and **Beta Diversity** (differences between samples).