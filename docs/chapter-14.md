# Chapter 15: Structural Bioinformatics

## 15.1 Structure Determines Function

In Chapter 3, we learned that proteins fold into complex 3D shapes. **Structural Bioinformatics** is the subfield dedicated to analyzing, predicting, and simulating these 3D structures.

Why does this matter? Because if you know the shape of a lock (a protein involved in a disease), you can design a key (a drug) to fit it.

## 15.2 The Protein Data Bank (PDB)

<p align="center">
  <img src="assets/illustrations/alphafold.svg" alt="Illustration of 3D Protein Structure">
</p>

## 14.4 Interpreting Predicted Structures and Downstream Analyses

Structure prediction (AlphaFold) is best used as a hypothesis generator. Guidance:

- **Confidence metrics:** Inspect per-residue confidence (pLDDT) and predicted aligned error (PAE) when available.
- **Compare to experiment:** Overlay predicted models with PDB or cryo-EM maps when possible to validate conformations.
- **Molecular dynamics (MD):** Use MD (e.g., `GROMACS`) to sample conformational flexibility and assess stability, when necessary.
- **Binding site inference:** Combine structure with docking and evolutionary conservation to predict ligand-binding residues.

Visualization & tools:

- `PyMOL`, `ChimeraX` for high-quality figures and interactive exploration.
- Use AlphaFold DB to query precomputed models before running local predictions.

The **PDB** is the worldwide repository for 3D structural data of large biological molecules. Unlike GenBank (which stores sequences), PDB stores **coordinates** (X, Y, Z positions) for every atom in the molecule.

These structures are usually determined experimentally using:
1.  **X-ray Crystallography:** Shining X-rays at a crystallized protein.
2.  **NMR Spectroscopy:** Using magnetic fields.
3.  **Cryo-Electron Microscopy (Cryo-EM):** Freezing samples and using electron microscopes (the current hot technology).

## 15.3 The AlphaFold Revolution

For 50 years, the "Protein Folding Problem" (predicting structure from sequence alone) was considered one of the hardest challenges in biology.

In 2020, Google DeepMind's **AlphaFold** AI solved this problem for most proteins. It uses deep learning to predict structures with accuracy comparable to experimental methods. This has completely transformed the field, giving us structures for nearly every known protein.

## 15.4 Molecular Docking

**Docking** is a computational simulation to predict how two molecules interact.
*   **Protein-Ligand Docking:** Predicting how a small drug molecule binds to a protein target. This is the basis of **Structure-Based Drug Design**.
*   **Protein-Protein Docking:** Predicting how two proteins form a complex.

## 15.5 Bioinformatics in Action: Parsing PDB Files

Biopython has a powerful module called `Bio.PDB` for manipulating these structures. Let's look at how to calculate the distance between two atoms.

```python
from Bio.PDB import PDBParser
import warnings

# Suppress PDB construction warnings for this example
warnings.filterwarnings("ignore")

# In a real scenario, you would download a file like '1FAT.pdb'
# parser = PDBParser()
# structure = parser.get_structure("MyProtein", "1FAT.pdb")

# For this example, let's imagine we have two atoms with 3D coordinates
# Atom A coordinates (x, y, z)
atom_a_coord = [1.0, 2.0, 3.0]

# Atom B coordinates
atom_b_coord = [4.0, 6.0, 8.0]

# We can calculate the Euclidean distance manually
import math

def calculate_distance(coord1, coord2):
    dx = coord1[0] - coord2[0]
    dy = coord1[1] - coord2[1]
    dz = coord1[2] - coord2[2]
    return math.sqrt(dx**2 + dy**2 + dz**2)

distance = calculate_distance(atom_a_coord, atom_b_coord)

print(f"Atom A: {atom_a_coord}")
print(f"Atom B: {atom_b_coord}")
print(f"Distance: {distance:.2f} Angstroms")
```

**Output:**
```text
Atom A: [1.0, 2.0, 3.0]
Atom B: [4.0, 6.0, 8.0]
Distance: 7.07 Angstroms
```

*Note: In `Bio.PDB`, you can simply subtract two atom objects (`dist = atom1 - atom2`) to get this distance!*

## Summary

Structural bioinformatics bridges the gap between linear sequence and 3D reality. With tools like the **PDB** and **AlphaFold**, we can visualize the molecular machinery of life and design drugs to fix it when it breaks.