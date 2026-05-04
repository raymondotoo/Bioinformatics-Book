# The Serial Bioinformatician

<p align="center">
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/ci.yml">
    <img src="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/ci.yml/badge.svg" alt="CI Build Status">
  </a>
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/deploy.yml">
    <img src="https://github.com/raymondotoo/Bioinformatics-Book/actions/workflows/deploy.yml/badge.svg" alt="Deploy Status">
  </a>
  <a href="https://raymondotoo.github.io/Bioinformatics-Book/">
    <img src="https://img.shields.io/badge/docs-online-brightgreen?logo=readthedocs" alt="Documentation">
  </a>
  <a href="https://raymondotoo.github.io/Bioinformatics-Book/pdf/document.pdf">
    <img src="https://img.shields.io/badge/PDF-Download-blue?logo=adobe-acrobat-reader" alt="Download PDF">
  </a>
</p>

<p align="center">
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg" alt="License: CC BY-SA 4.0">
  </a>
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/stargazers">
    <img src="https://img.shields.io/github/stars/raymondotoo/Bioinformatics-Book?style=social" alt="GitHub Stars">
  </a>
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/network/members">
    <img src="https://img.shields.io/github/forks/raymondotoo/Bioinformatics-Book?style=social" alt="GitHub Forks">
  </a>
  <a href="https://github.com/raymondotoo/Bioinformatics-Book/issues">
    <img src="https://img.shields.io/github/issues/raymondotoo/Bioinformatics-Book" alt="GitHub Issues">
  </a>
</p>

<p align="center">
  <img src="docs/assets/cover.png" alt="Cover of The Serial Bioinformatician" width="560">
</p>

<p align="center">
  <a href="https://raymondotoo.github.io/Bioinformatics-Book/"><strong>Read Online</strong></a> ·
  <a href="https://raymondotoo.github.io/Bioinformatics-Book/pdf/document.pdf"><strong>Download PDF</strong></a>
</p>

A comprehensive guide to modern bioinformatics, moving from the central dogma and molecular biology foundations to sequencing, transcriptomics, structural biology, statistical analysis, visualization, and multi-omics integration.

## About the Book

This book is written to help readers move from biological concepts to practical computational analysis. It is designed for students, early-career researchers, and scientists who want a structured path into bioinformatics without losing the biological intuition behind the tools.

## What the Book Covers

- Molecular biology foundations: DNA, transcription, translation, proteins, and genetic variation.
- Core computational skills: command line, Python, biological databases, and basic statistics.
- Bioinformatics workflows: sequence alignment, phylogenetics, genome assembly, NGS, and RNA-seq.
- Advanced applications: structural bioinformatics, systems biology, clinical proteomics, visualization, and multi-omics.

## Table of Contents

### Part 1: The Biological Foundation

- [**Chapter 1: Introduction to the Central Dogma**](docs/chapter-01.md)
- [**Chapter 2: The Genome and its Variations**](docs/chapter-02.md)
- [**Chapter 3: Proteins - The Functional Units**](docs/chapter-03.md)

### Part 2: Foundational Computational Skills

- [**Chapter 4: Introduction to the Command Line for Biologists**](docs/chapter-04.md)
- [**Chapter 5: Programming for Bioinformatics with Python**](docs/chapter-05.md)
- [**Chapter 6: Navigating Biological Databases (NCBI, Ensembl, UniProt)**](docs/chapter-06.md)
- [**Chapter 7: Statistics for Bioinformatics**](docs/chapter-19.md)

### Part 3: Core Bioinformatics Analysis

- [**Chapter 8: Sequence Alignment**](docs/chapter-07.md)
- [**Chapter 9: Phylogenetics: Understanding Evolutionary Relationships**](docs/chapter-08.md)
- [**Chapter 10: Genome Assembly and Annotation**](docs/chapter-09.md)

### Part 4: High-Throughput Omics

- [**Chapter 11: Introduction to Next-Generation Sequencing (NGS)**](docs/chapter-10.md)
- [**Chapter 12: Transcriptomics: Analyzing Gene Expression (RNA-Seq)**](docs/chapter-11.md)
- [**Chapter 13: Proteomics and Metabolomics**](docs/chapter-12.md)
- [**Chapter 14: Microbiomics: Analyzing Microbial Communities (16S rRNA & QIIME 2)**](docs/chapter-13.md)

### Part 5: Advanced Topics and Applications

- [**Chapter 15: Structural Bioinformatics**](docs/chapter-14.md)
- [**Chapter 16: Systems Biology: Integrating the Omics**](docs/chapter-15.md)
- [**Chapter 17: Bioinformatics in Medicine**](docs/chapter-16.md)
- [**Chapter 18: Integrated Clinical Proteomics**](docs/chapter-17.md)
- [**Chapter 19: Interactive Visualization with R Shiny**](docs/chapter-18.md)
- [**Chapter 20: Multiomics Data Integration**](docs/chapter-20.md)

### Appendix

- [**Glossary of Terms**](docs/GLOSSARY.md)

## About the Author

**Raymond Otoo, Ph.D.** is a Bioinformatics Scientist specializing in multi-omics integration and biomarker discovery. His work focuses on applying systems biology approaches to unravel the complexities of neurodegenerative diseases and on building tools that make these insights more accessible to clinicians and researchers.

## Building the Book Locally

To preview the book on your computer:

1. Install dependencies:

   ```bash
   pip3 install -r requirements.txt
   ```

2. Run the local server:

   ```bash
   python3 -m mkdocs serve
   ```

3. Open `http://127.0.0.1:8000`.

## Publishing to GitHub Pages

This repository is configured to deploy automatically when changes are pushed to `main` or `master`.

1. Commit your changes.
2. Push to the deployment branch.
3. Wait for the GitHub Actions deploy workflow to finish.
