# CXCR4 Structural Contact Analysis

## Overview

CXCR4 is a G protein-coupled chemokine receptor involved in immune-cell migration, inflammatory signaling, cancer progression, and HIV entry.

This project compares the CXCR4 binding-pocket footprints of two structurally different antagonists:

- **IT1t**, a small-molecule antagonist in PDB structure **3ODU**
- **CVX15**, a cyclic peptide antagonist in PDB structure **3OE0**

The goal was to identify CXCR4 residues located near each antagonist and determine which receptor contacts are shared or unique to each ligand.

## Research question

Which CXCR4 residues are located within 4.5 Å of IT1t and CVX15, and how do their contact footprints differ?

## Structures analyzed

### 3ODU

- Receptor: CXCR4
- Antagonist: IT1t
- Ligand identifier: `ITD`
- Ligand type: Small molecule
- Receptor copy analyzed: Chain A

### 3OE0

- Receptor: CXCR4
- Antagonist: CVX15
- Ligand type: Cyclic peptide
- Receptor chain: Chain A
- Ligand chain: Chain I
- CVX15 residues included: 1 through 16

Crystallographic water molecules in chain I were excluded from the CVX15 selection.

## Analysis workflow

The analysis was performed in Python using Biopython.

1. Downloaded PDB structures 3ODU and 3OE0 from the RCSB Protein Data Bank.
2. Parsed both structures using `Bio.PDB.PDBParser`.
3. Selected IT1t from chain A of 3ODU.
4. Selected CVX15 residues 1 through 16 from chain I of 3OE0.
5. Excluded crystallographic water molecules from the CVX15 selection.
6. Selected modeled CXCR4 residues from chain A.
7. Excluded hetero-components and the engineered T4 lysozyme region.
8. Defined a contact as a CXCR4 residue with at least one atom within 4.5 Å of a ligand atom.
9. Identified contact residues using Biopython's `NeighborSearch`.
10. Compared shared, IT1t-only, and CVX15-only contacts.
11. Repeated the analysis at several distance cutoffs.
12. Generated a colorblind-friendly comparison chart and CSV result files.

## Contact definition

A CXCR4 residue was classified as a ligand contact when at least one atom in that residue was within 4.5 Å of at least one ligand atom.

This is a geometric proximity measurement. It does not independently identify the chemical type or strength of an interaction.

## Results

Using a 4.5 Å distance cutoff, the analysis identified:

- **[IT1T COUNT] CXCR4 residues** within 4.5 Å of IT1t
- **[CVX15 COUNT] CXCR4 residues** within 4.5 Å of CVX15

Comparison of the two contact footprints showed:

- **[SHARED COUNT] shared residues**, found near both antagonists
- **[IT1T-ONLY COUNT] IT1t-specific residues**, found near IT1t but not CVX15
- **[CVX15-ONLY COUNT] CVX15-specific residues**, found near CVX15 but not IT1t

Together, these results show that the antagonists occupy partially overlapping
but nonidentical regions of the CXCR4 binding pocket.

### Contact-footprint comparison
```text
Results/High_Resolution_Cxcr4_Contact_Comparison_Graph.png
```
```text
Results/Preview_Cxcr4_Contact_Comparison_Graph.png
```
## Interpretation

The analysis shows that IT1t and CVX15 occupy partly overlapping regions of the CXCR4 binding pocket.

The shared contact residues identify a common region of CXCR4 used by both antagonists. This overlap suggests that, despite their 
different chemical structures, IT1t and CVX15 interact with some of the same parts of the receptor.

The ligand-specific contacts show that the two antagonists do not occupy the pocket in exactly the same way. IT1t is a relatively 
small molecule, so its contacts are concentrated within a more restricted region of the pocket. CVX15 is a larger cyclic peptide 
and extends across a broader portion of the receptor, allowing it to contact additional CXCR4 residues.

These differences describe the geometric footprints of the antagonists in the two crystal structures. They do not show that 
one antagonist binds more strongly or is more effective than the other. Binding strength and antagonist
activity depend on the types, strengths, and dynamics of the interactions, not only on the number of nearby residues.

Overall, the results demonstrate that CXCR4 contains a shared antagonist-binding region while also accommodating chemically 
different ligands through distinct contact patterns.

## Cutoff-sensitivity analysis

The definition of a contact depends on the selected distance cutoff. To examine
how this choice affected the results, the analysis was repeated using four
cutoffs:

- 3.5 Å
- 4.0 Å
- 4.5 Å
- 5.0 Å

As the cutoff increased, more CXCR4 residues were classified as being near each
ligand. This is expected because a larger cutoff includes residues located
farther from the ligand.

The sensitivity analysis was used to determine whether the main conclusion
remained consistent across different cutoffs. Although the exact number of
contact residues changed, IT1t and CVX15 continued to show overlapping but
different contact footprints.

The complete cutoff-sensitivity results are available in
`Results/cutoff_sensitivity.csv`.
