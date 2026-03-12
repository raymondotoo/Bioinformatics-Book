# The Serial Bioinformatician

<!-- Status Badges -->
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
  <a href="https://github.com/raymondotoo/Bioinformatics-Book">
    <img src="https://img.shields.io/github/stars/raymondotoo/Bioinformatics-Book?style=social" alt="Stars">
  </a>
</p>

<p align="center">
  <img src="assets/cover.png" alt="Book Cover" width="500">
</p>

A comprehensive guide from the central dogma to cutting-edge computational techniques in bioinformatics.

[Download PDF](pdf/document.pdf){ .md-button .md-button--primary }

---

## About the Author

**Raymond Otoo, Ph.D.** is a Bioinformatics Scientist specializing in multi-omics integration and biomarker discovery. His work focuses on applying systems biology approaches to unravel the complexities of neurodegenerative diseases and developing interactive tools to make these insights accessible to clinicians.

## Introduction

The journey of bioinformatics is one of translation. We start with a biological problem—a disease, a phenotype, or an unknown mechanism—and generate massive amounts of biological data.

The main goal of this book is to guide you from the problem and raw biological data to robust molecular insights. It is these insights that provide the necessary directions for identifying novel therapeutic targets and advancing the field of precision medicine.

---

## Book Structure & Table of Contents

This book is structured to guide the reader from the fundamental principles of molecular biology to the practical application of bioinformatics tools and algorithms.

### Part 1: The Biological Foundation

*   [**Chapter 1: Introduction to the Central Dogma**](chapter-01.md)
    *   What is Bioinformatics?
    *   DNA: The Blueprint of Life
    *   Transcription: From DNA to RNA
    *   Translation: From RNA to Protein

*   [**Chapter 2: The Genome and its Variations**](chapter-02.md)
    *   DNA Structure and Replication
    *   Genes and Chromosomes
    *   Genetic Variation: SNPs, Indels, and Structural Variants

*   [**Chapter 3: Proteins - The Functional Units**](chapter-03.md)
    *   Amino Acids and Protein Structure (Primary, Secondary, Tertiary, Quaternary)
    *   Protein Function and Families

### Part 2: Foundational Computational Skills

*   [**Chapter 4: Introduction to the Command Line for Biologists**](chapter-04.md)
*   [**Chapter 5: Programming for Bioinformatics with Python**](chapter-05.md)
*   [**Chapter 6: Navigating Biological Databases (NCBI, Ensembl, UniProt)**](chapter-06.md)
*   [**Chapter 7: Statistics for Bioinformatics**](chapter-19.md)

### Part 3: Core Bioinformatics Analysis

*   [**Chapter 8: Sequence Alignment**](chapter-07.md)
*   [**Chapter 9: Phylogenetics: Understanding Evolutionary Relationships**](chapter-08.md)
*   [**Chapter 10: Genome Assembly and Annotation**](chapter-09.md)

### Part 4: High-Throughput "Omics"

*   [**Chapter 11: Introduction to Next-Generation Sequencing (NGS)**](chapter-10.md)
*   [**Chapter 12: Transcriptomics: Analyzing Gene Expression (RNA-Seq)**](chapter-11.md)
*   [**Chapter 13: Proteomics and Metabolomics**](chapter-12.md)
*   [**Chapter 14: Microbiomics: Analyzing Microbial Communities (16S rRNA & QIIME 2)**](chapter-13.md)

### Part 5: Advanced Topics and Applications

*   [**Chapter 15: Structural Bioinformatics**](chapter-14.md)
*   [**Chapter 16: Systems Biology: Integrating the 'Omics'**](chapter-15.md)
*   [**Chapter 17: Bioinformatics in Medicine**](chapter-16.md)
*   [**Chapter 18: Integrated Clinical Proteomics**](chapter-17.md)
*   [**Chapter 19: Interactive Visualization with R Shiny**](chapter-18.md)
*   [**Chapter 20: Multiomics Data Integration**](chapter-20.md)

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

---

## Deploying to GitHub Pages

To publish or update the live version of the book:

1.  **Commit your changes:** Make sure all your latest work is saved.
    ```bash
    git add .
    git commit -m "Update book content"
    ```
2.  **Run the deploy command:**
    ```bash
    python3 -m mkdocs gh-deploy
    ```
