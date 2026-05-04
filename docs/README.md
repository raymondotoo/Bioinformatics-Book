# The Serial Bioinformatician

<p align="center">
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/ci.yml">
    <img src="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/ci.yml/badge.svg" alt="CI Status">
  </a>
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/deploy.yml">
    <img src="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/deploy.yml/badge.svg" alt="Deploy Status">
  </a>
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg" alt="License">
  </a>
</p>

<p align="center">
  <img src="assets/cover.png" alt="Cover of The Serial Bioinformatician" width="500">
</p>

A comprehensive guide that takes readers from the central dogma to practical, real-world bioinformatics analysis.

[Download PDF](pdf/document.pdf){ .md-button .md-button--primary }
[View on GitHub](https://github.com/raymondotoo/Bioinformatics-Book){ .md-button }

---

## About the Book

This book connects biological foundations with modern computational workflows. It is meant to be approachable for beginners while still being useful to researchers who want a structured overview of current bioinformatics topics.

## What You Will Learn

- How DNA, RNA, proteins, and genetic variation connect to computational analysis.
- How to work with the command line, Python, and biological databases.
- How common workflows such as NGS and RNA-seq are structured.
- How statistical thinking, visualization, and multi-omics fit into modern bioinformatics.

## Book Structure

### Part 1: The Biological Foundation

- [**Chapter 1: Introduction to the Central Dogma**](chapter-01.md)
- [**Chapter 2: The Genome and its Variations**](chapter-02.md)
- [**Chapter 3: Proteins - The Functional Units**](chapter-03.md)

### Part 2: Foundational Computational Skills

- [**Chapter 4: Introduction to the Command Line for Biologists**](chapter-04.md)
- [**Chapter 5: Programming for Bioinformatics with Python**](chapter-05.md)
- [**Chapter 6: Navigating Biological Databases (NCBI, Ensembl, UniProt)**](chapter-06.md)
- [**Chapter 7: Statistics for Bioinformatics**](chapter-19.md)

### Part 3: Core Bioinformatics Analysis

- [**Chapter 8: Sequence Alignment**](chapter-07.md)
- [**Chapter 9: Phylogenetics: Understanding Evolutionary Relationships**](chapter-08.md)
- [**Chapter 10: Genome Assembly and Annotation**](chapter-09.md)

### Part 4: High-Throughput Omics

- [**Chapter 11: Introduction to Next-Generation Sequencing (NGS)**](chapter-10.md)
- [**Chapter 12: Transcriptomics: Analyzing Gene Expression (RNA-Seq)**](chapter-11.md)
- [**Chapter 13: Proteomics and Metabolomics**](chapter-12.md)
- [**Chapter 14: Microbiomics: Analyzing Microbial Communities (16S rRNA & QIIME 2)**](chapter-13.md)

### Part 5: Advanced Topics and Applications

- [**Chapter 15: Structural Bioinformatics**](chapter-14.md)
- [**Chapter 16: Systems Biology: Integrating the Omics**](chapter-15.md)
- [**Chapter 17: Bioinformatics in Medicine**](chapter-16.md)
- [**Chapter 18: Integrated Clinical Proteomics**](chapter-17.md)
- [**Chapter 19: Interactive Visualization with R Shiny**](chapter-18.md)
- [**Chapter 20: Multiomics Data Integration**](chapter-20.md)

### Appendix

- [**Glossary of Terms**](GLOSSARY.md)

## About the Author

**Raymond Otoo, Ph.D.** is a Bioinformatics Scientist specializing in multi-omics integration and biomarker discovery. His work focuses on applying systems biology approaches to unravel the complexities of neurodegenerative diseases and on building tools that make these insights more accessible to clinicians and researchers.

## Building the Book Locally

1. Install dependencies:

   ```bash
   pip3 install -r requirements.txt
   ```

2. Run the local documentation server:

   ```bash
   python3 -m mkdocs serve
   ```

3. Open `http://127.0.0.1:8000`.
