# Chapter 4: Introduction to the Command Line for Biologists

## 4.1 Breaking the GUI Habit

<p align="center">
  <img src="../assets/illustrations/figure-template.svg" alt="Illustration of CLI vs GUI">
</p>

## 4.3 Practical CLI Best Practices

A bioinformatics environment is built on reliable command-line workflows. Key recommendations:

- **Environments:** Use `conda`/`mamba` to manage packages and isolate environments.
- **Containers:** Ship reproducible analysis with `Docker` or `Singularity/Apptainer` to freeze software stacks.
- **Workflow managers:** Combine CLI tools with `Snakemake` or `Nextflow` for reproducibility and scalability.
- **Useful utilities:** `jq` for JSON, `csvkit` for CSV, `htop` for processes, and `tmux` for session management.

Example: quickly view a BAM header and index it:

```bash
# View header
samtools view -H sample.bam

# Sort and index (recommended post-alignment)
samtools sort -o sample.sorted.bam sample.bam
samtools index sample.sorted.bam
```

Use containers when distributing pipelines; include `Dockerfile` or `Singularity` recipes in the repo.

Up until now, you have likely interacted with computers using a Graphical User Interface (GUI)—clicking icons, dragging folders, and using menus. While intuitive, GUIs have limits. They are hard to automate, struggle with massive files (try opening a 50GB genome file in Excel!), and are often unavailable on the powerful remote servers where actual bioinformatics work happens.

Enter the **Command Line Interface (CLI)**, also known as the terminal or shell. It might look intimidating—a black screen with blinking text—but it is the most powerful tool in your arsenal.

## 4.2 Navigation: Finding Your Way

When you open a terminal, you are "standing" in a specific folder on your computer.

### Where am I? (`pwd`)
`pwd` stands for **P**rint **W**orking **D**irectory.
```bash
$ pwd
/Users/biologist/data
```

### What is here? (`ls`)
`ls` **L**i**s**ts the files in your current directory.
```bash
$ ls
genome.fasta  notes.txt  raw_data/
```

### Go somewhere else (`cd`)
`cd` stands for **C**hange **D**irectory.
```bash
$ cd raw_data
$ pwd
/Users/biologist/data/raw_data
```
*Tip: `cd ..` moves you "up" one folder.*

---

## 4.3 Handling Files: The Basics

Bioinformatics involves moving, renaming, and organizing thousands of files.

*   **`mkdir analysis`**: **M**a**k**e a **dir**ectory (folder) named "analysis".
*   **`cp gene.txt gene_backup.txt`**: **C**o**p**y a file.
*   **`mv gene.txt analysis/`**: **M**o**v**e a file into a folder (also used to rename files).
*   **`rm junk.txt`**: **R**e**m**ove (delete) a file. **Warning: There is no Trash Can in the terminal. Deleted files are gone forever.**

---

## 4.4 Inspecting Biological Data

Biological data files (like FASTA or FASTQ) are often massive text files. You don't want to open them in a text editor; it will crash your computer. Instead, we peek at them.

### `head` and `tail`
View the first or last 10 lines of a file.
```bash
$ head genome.fasta
>chr1
ATGCGTAC...
```

### `less`
Allows you to scroll through a huge file page by page without loading the whole thing into memory. Press `q` to exit.

### `wc`
**W**ord **C**ount. Counts lines, words, and characters.
```bash
$ wc -l genome.fasta
50000 genome.fasta
```
(This tells us the file has 50,000 lines).

---

## 4.5 The Power Tools: `grep` and Pipes

This is where the magic happens.

### `grep`: Search
`grep` searches for a specific pattern in a file.
Imagine you want to find a specific gene ID in a massive annotation file.
```bash
$ grep "TP53" annotations.gff
```

### The Pipe (`|`)
The pipe takes the output of one command and passes it as input to the next. It allows you to chain tools together.

**Scenario:** How many sequences are in my FASTA file?
In a FASTA file, every sequence header starts with a `>`. We can find all headers with `grep`, and then count them with `wc`.

```bash
$ grep ">" sequences.fasta | wc -l
450
```
We just counted the number of sequences in a file without ever opening it!