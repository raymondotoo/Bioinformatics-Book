# Chapter 5: Programming for Bioinformatics with Python

## 5.1 Why Python?

If you ask a room full of bioinformaticians what programming language they use, the vast majority will say **Python**.

Why?
1.  **Readability:** Python code reads almost like English. This is crucial for scientists who want to focus on biology, not complex syntax.
2.  **Libraries:** There is a massive ecosystem of pre-written code. Need to calculate statistics? Use `pandas`. Need to plot a graph? Use `matplotlib`. Need to parse a DNA file? Use `Biopython`.

In this chapter, we will focus on **Biopython**, the standard library for computational biology.

---

## 5.2 Getting Started with Biopython

<p align="center">
  <img src="assets/illustrations/figure-template.svg" alt="Illustration of Biopython">
</p>

Before we write code, you usually need to install the library. In your terminal (Chapter 4 skills!), you would run:

```bash
pip install biopython
```

### The `Seq` Object
In standard Python, DNA is just a string of text. In Biopython, we use the `Seq` object. It knows that the string represents a biological sequence and gives us powerful methods.

```python
from Bio.Seq import Seq

# Create a Sequence object
my_dna = Seq("AGTACACTGGT")

# It acts like a string...
print(f"Sequence: {my_dna}")

# ...but it has biological superpowers!
print(f"Complement: {my_dna.complement()}")
print(f"Reverse Complement: {my_dna.reverse_complement()}")
```

**Output:**
```text
Sequence: AGTACACTGGT
Complement: TCATGTGACCA
Reverse Complement: ACCAGTGTACT
```

*Note: Calculating a reverse complement manually is tedious and error-prone. Biopython does it instantly.*

---

## 5.3 Transcription and Translation (The Easy Way)

Remember the scripts we wrote in Chapters 1 and 3? We had to manually replace letters and build dictionary lookup tables. Biopython handles the Central Dogma natively.

```python
from Bio.Seq import Seq

gene = Seq("ATGGCCATTGTAATGGGCCGCTGAAAGGGTGCCCGATAG")

# 1. Transcribe (DNA -> RNA)
mRNA = gene.transcribe()

# 2. Translate (RNA -> Protein)
protein = mRNA.translate()

print(f"DNA:     {gene}")
print(f"mRNA:    {mRNA}")
print(f"Protein: {protein}")
```

**Output:**
```text
DNA:     ATGGCCATTGTAATGGGCCGCTGAAAGGGTGCCCGATAG
mRNA:    AUGGCCAUUGUAAUGGGCCGCUGAAAGGGUGCCCGAUAG
Protein: MAIVMGR*KGAR*
```
*(The `*` represents a Stop codon).*

---

## 5.4 Reading Biological Files (`SeqIO`)

In the real world, you don't type sequences into your code. You read them from files (FASTA, GenBank, FASTQ).

The `Bio.SeqIO` module is the standard way to read and write these files. It handles the messy formatting for you.

Imagine you have a file named `example.fasta` with multiple gene sequences.

```python
from Bio import SeqIO

# SeqIO.parse takes the filename and the format name
for record in SeqIO.parse("example.fasta", "fasta"):
    
    # 'record' holds the ID and the Sequence
    print(f"ID: {record.id}")
    print(f"Length: {len(record.seq)}")
    print(f"First 10 bases: {record.seq[:10]}")
    print("---")
```

This simple loop can process files containing millions of sequences without crashing your computer, as it reads them one by one.

## Summary

Python, combined with Biopython, allows us to automate the biological concepts we learned in Part 1. We can now manipulate sequences, perform the central dogma operations, and read standard file formats with just a few lines of code.

## 5.5 Practical Libraries, Workflows, and Best Practices

Python's ecosystem supports every step of modern bioinformatics. Key recommendations:

- **Core packages:** `biopython`, `pandas`, `numpy`, `scipy` for data handling and basic statistics.
- **Machine learning / deep learning:** `scikit-learn`, `xgboost`, `tensorflow`, `pytorch`.
- **Single-cell analysis:** `scanpy`, `anndata` for preprocessing and downstream analyses.
- **Interactive and reproducible:** Use Jupyter or VS Code notebooks for exploration; export production code as scripts and add tests.
- **Packaging & environments:** Use `poetry`, `pip`, or `conda`/`mamba` for environment management; pin dependencies in `environment.yml` or `requirements.txt`.

Example: a small, testable function with a type hint and a unit test-friendly design.

```python
from typing import List, Dict

def gc_content(seq: str) -> float:
  """Return GC percentage of a DNA sequence."""
  s = seq.upper()
  if not s:
    return 0.0
  return (s.count('G') + s.count('C')) / len(s) * 100

# This function is simple to unit test and reuse in pipelines.
```

Add CI and tests for critical utilities to avoid silent regressions in pipelines.