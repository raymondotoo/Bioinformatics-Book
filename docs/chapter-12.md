# Chapter 12: Proteomics and Metabolomics

## 12.1 Beyond the Genome

Genomics tells us what *could* happen (the blueprint). Transcriptomics tells us what *appears* to be happening (the instructions). But **Proteomics** and **Metabolomics** tell us what is *actually* happening.

Proteins are the functional units, and metabolites are the fuel and building blocks. Studying them gives us the closest view of the organism's phenotype.

## 12.2 Proteomics: The Mass Spec Revolution

Unlike DNA, we cannot "sequence" proteins easily. Instead, we weigh them.

**Mass Spectrometry (Mass Spec)** is the workhorse of proteomics.
1.  **Digestion:** Proteins are chopped into small peptides using enzymes like Trypsin.
2.  **Ionization:** Peptides are given an electric charge and turned into gas.
3.  **Detection:** The machine measures the **Mass-to-Charge Ratio (m/z)** of these peptides.

Bioinformatics software then takes these lists of masses and compares them against a database of known protein masses to identify which proteins are present.

## 12.3 Metabolomics: The Chemical Fingerprint

**Metabolomics** studies small molecules (sugars, lipids, amino acids, vitamins).

*   **Targeted Metabolomics:** Looking for a specific set of known compounds (e.g., "How much glucose is in this blood sample?").
*   **Untargeted Metabolomics:** Measuring everything to find new patterns (e.g., "What molecules are different in cancer patients vs healthy people?").

## 12.4 Bioinformatics in Action: Protein Analysis

While analyzing raw Mass Spec data requires specialized tools (like MaxQuant), we can use Biopython to analyze the properties of the proteins we identify.

Let's calculate the molecular weight and instability index of a protein sequence.

```python
from Bio.SeqUtils.ProtParam import ProteinAnalysis

# A sample protein sequence (p53 partial)
protein_seq = "MEEPQSDPSVEPPLSQETFSDLWKLLPENNVLSPLPSQAMDDLMLSPDDIEQWFTEDPGP"

# Create an analysis object
analysed_seq = ProteinAnalysis(protein_seq)

# 1. Calculate Molecular Weight (in Daltons)
mw = analysed_seq.molecular_weight()

# 2. Calculate Isoelectric Point (pH where charge is 0)
pi = analysed_seq.isoelectric_point()

# 3. Calculate Amino Acid Percentages
aa_count = analysed_seq.get_amino_acids_percent()

print(f"Sequence Length: {len(protein_seq)}")
print(f"Molecular Weight: {mw:.2f} Da")
print(f"Isoelectric Point: {pi:.2f}")
print(f"Percent Leucine (L): {aa_count['L']:.1%}")
```

**Output:**
```text
Sequence Length: 60
Molecular Weight: 6793.46 Da
Isoelectric Point: 3.77
Percent Leucine (L): 13.3%
```

## 12.5 Pathway Analysis

Once we have a list of changed proteins or metabolites, we map them to **Pathways**.

*   **KEGG (Kyoto Encyclopedia of Genes and Genomes):** A database of metabolic pathways.
*   **Reactome:** A database of biological reactions.

If you find that "Glucose", "Pyruvate", and "ATP" are all elevated, pathway analysis will tell you that "Glycolysis" is upregulated.

## Summary

Proteomics and Metabolomics use **Mass Spectrometry** to identify and quantify the functional molecules of the cell. Bioinformatics is used to identify these molecules from their mass fingerprints and map them to biological **pathways** to understand the cell's metabolic state.