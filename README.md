# The Serial Bioinformatician

<p align="center">
  <img src="docs/assets/cover.png" alt="Book Cover" width="500">
</p>

A comprehensive guide from the central dogma to cutting-edge computational techniques in bioinformatics.

---

## About the Author

**Raymond Otoo, Ph.D.** is a Bioinformatics Scientist specializing in multi-omics integration and biomarker discovery. His work focuses on applying systems biology approaches to unravel the complexities of neurodegenerative diseases and developing interactive tools to make these insights accessible to clinicians.

## Introduction

The journey of bioinformatics is one of translation. We start with a biological problem: a disease, a phenotype, or an unknown mechanism and generate massive amounts of biological data.

The main goal of this book is to guide you from the problem and raw biological data to robust molecular insights. It is these insights that provide the necessary directions for identifying novel therapeutic targets and advancing the field of precision medicine.

---

## Book Structure & Table of Contents

This book is structured to guide the reader from the fundamental principles of molecular biology to the practical application of bioinformatics tools and algorithms.

### Part 1: The Biological Foundation

*   [**Chapter 1: Introduction to the Central Dogma**](docs/chapter-01.md)
    *   What is Bioinformatics?
    *   DNA: The Blueprint of Life
    *   Transcription: From DNA to RNA
    *   Translation: From RNA to Protein

*   [**Chapter 2: The Genome and its Variations**](docs/chapter-02.md)
    *   DNA Structure and Replication
    *   Genes and Chromosomes
    *   Genetic Variation: SNPs, Indels, and Structural Variants

*   [**Chapter 3: Proteins - The Functional Units**](docs/chapter-03.md)
    *   Amino Acids and Protein Structure (Primary, Secondary, Tertiary, Quaternary)
    *   Protein Function and Families

### Part 2: Foundational Computational Skills

*   [**Chapter 4: Introduction to the Command Line for Biologists**](docs/chapter-04.md)
*   [**Chapter 5: Programming for Bioinformatics with Python**](docs/chapter-05.md)
*   [**Chapter 6: Navigating Biological Databases (NCBI, Ensembl, UniProt)**](docs/chapter-06.md)

### Part 3: Core Bioinformatics Analysis

*   [**Chapter 7: Sequence Alignment**](docs/chapter-07.md)
*   [**Chapter 8: Phylogenetics: Understanding Evolutionary Relationships**](docs/chapter-08.md)
*   [**Chapter 9: Genome Assembly and Annotation**](docs/chapter-09.md)

### Part 4: High-Throughput "Omics"

*   [**Chapter 10: Introduction to Next-Generation Sequencing (NGS)**](docs/chapter-10.md)
*   [**Chapter 11: Transcriptomics: Analyzing Gene Expression (RNA-Seq)**](docs/chapter-11.md)
*   [**Chapter 12: Proteomics and Metabolomics**](docs/chapter-12.md)
*   [**Chapter 13: Microbiomics: Analyzing Microbial Communities (16S rRNA & QIIME 2)**](docs/chapter-13.md)

### Part 5: Advanced Topics and Applications

*   [**Chapter 14: Structural Bioinformatics**](docs/chapter-14.md)
*   [**Chapter 15: Systems Biology: Integrating the 'Omics'**](docs/chapter-15.md)
*   [**Chapter 16: Bioinformatics in Medicine**](docs/chapter-16.md)
*   [**Chapter 17: Integrated Clinical Proteomics**](docs/chapter-17.md)
*   [**Chapter 18: Interactive Visualization with R Shiny**](docs/chapter-18.md)

---

### Appendices

*   [**Glossary of Terms**](GLOSSARY.md)

---

## Building the Book Locally

To read this book on your own computer or to check your changes before contributing:

1.  **Install Dependencies:**
    ```bash
    pip3 install -r requirements.txt
    ```
2.  **Run the Server:**
    ```bash
    python3 -m mkdocs serve
    ```
3.  **View:** Open your browser to `http://127.0.0.1:8000`.
