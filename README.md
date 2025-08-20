# In Silico Identification of Novel Inhibitors Against NRAS in Melanoma

This repository documents the workflow used to identify potential natural product inhibitors targeting mutant **NRAS** in melanoma using **in silico approaches**.

---

## Overview

Melanoma is an aggressive form of skin cancer where NRAS mutations (codons **12, 13, and 61**) play a key role in oncogenesis. Existing therapies (e.g., MEK inhibitors like Binimetinib) show limited efficacy.  
This study applies **virtual screening** and **molecular docking** to explore natural compounds as potential inhibitors of mutant NRAS.

---

## Workflow

### 1. Target Selection
- **Protein**: NRAS (PDB ID: `5UHV`, UniProt ID: `P01111`)
- **Mutations introduced**:
  - G12D (Gly → Asp)
  - G13D (Gly → Asp)
  - Q61R (Gln → Arg)

---

### 2. Protein Preparation
- Download wild-type NRAS structure from PDB.
- Introduce mutations in **Swiss PDB Viewer (SPDBV)** / Discovery Studio.
- Save final mutant structure for docking.

---

### 3. Structure Validation
- **ProSA**: Global z-score and residue energy profile.
- **PROCHECK**: Ramachandran plot and stereochemical quality.
- Criteria: Most residues should fall in allowed regions; majority of z-scores should be negative.

---

### 4. Compound Library
- Source: **ZINC Database** (Natural Product Repository).
- Total compounds screened: **5322**.
- Filtering with **FAF-Drugs4**:
  - Lead-like properties.
  - Removal of **PAINS** (Pan-Assay Interference Compounds).
  - ADME-Tox pre-screening.

---

### 5. Docking Setup
- Tool: **PyRx (AutoDock 4.2)** with Lamarckian GA.
- Validation:
  - Docked known ligand (phosphoaminophosphonic acid-guanylate ester, GTP analog).
  - RMSD tolerance: ≤ 2.0 Å.
- Parameters:
  - Grid box: `50 x 50 x 50 Å`
  - Spacing: `0.375 Å`
  - 10 poses per compound generated.
- Ligands converted to **pdbqt** format.

---

### 6. Virtual Screening
- Docked 5322 compounds against mutant NRAS.
- Top hits shortlisted based on **binding free energy (kcal/mol)**.

---

### 7. Post-Docking Analysis
- Tool: **LigPlot+**
- Generated **2D interaction diagrams**.
- Identified:
  - **Hydrogen bond donors/acceptors**
  - **Hydrophobic interactions** (stability indicators)

Key residues observed in stable complexes:
- **Thr-35** – stability, Mg²⁺ coordination.
- **Tyr-32** – switch I interactions.
- **Phe-28** – stabilizes nucleotide binding.
- **Asp-119** – critical for nucleotide binding.

---

### 8. Results
- 11 compounds shortlisted (binding free energy: –10.62 to –10.04 kcal/mol).
- **Top 3 potential inhibitors**:
  - ZINC02096813
  - ZINC02120343
  - ZINC00518885
- Stable hydrogen bonds observed with mutant residues (Asp-12, Asp-13, Q61R).
- Hydrophobic stabilization by **Phe-28** and **Asp-119**.

---

### 9. Conclusion
- Mutant NRAS validated as a druggable melanoma target.
- Three natural product compounds identified as **potential inhibitors**.
- These results provide a **starting point for further validation**.

---

## Future Work
- Perform **Molecular Dynamics (MD) simulations** (50–100 ns) to confirm complex stability.
- Apply **binding free energy calculations** (MM/PBSA or MM/GBSA).
- Predict **ADMET** properties (SwissADME, pkCSM).
- Explore **experimental validation** in melanoma cell lines.

---

## Tools & Resources
- **Protein structures**: [PDB](https://www.rcsb.org/) (5UHV)
- **Mutant modeling**: Swiss PDB Viewer (SPDBV), Discovery Studio
- **Validation**: [ProSA](https://prosa.services.came.sbg.ac.at/prosa.php), [PROCHECK](https://www.ebi.ac.uk/thornton-srv/software/PROCHECK/)
- **Compound library**: [ZINC Database](https://zinc.docking.org/)
- **Filtering**: [FAF-Drugs4](http://fafdrugs4.mti.univ-paris-diderot.fr/)
- **Docking**: [PyRx](https://pyrx.sourceforge.io/) (AutoDock 4.2 backend)
- **Interaction analysis**: [LigPlot+](https://www.ebi.ac.uk/thornton-srv/software/LigPlus/)

---

