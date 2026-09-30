# FoldCheck-RNA

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mirikrupkin/foldcheck-rna/blob/main/foldcheck-rna.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Version 0.0.1 (2026-09-30), early release.**
> **New:** 2D structure drawings and 2D distance heat maps (experimental), a prediction-only view, and a pLDDT color legend.

**Compare an RNA 3D structure prediction with an experimental structure from the PDB: RMSD, matched nucleotides, sequence identity, and a side-by-side 3D view.**

Author: [Dr. Miri Krupkin](https://linkedin.com/in/mirikrupkin) (Applied AI Research Scientist & Computational Biologist)

## How to run
1. Open the notebook in Colab with the badge above. Viewing works without an account; running needs a free Google account.
2. Choose **Runtime → Run all**, then answer the prompts in the last cell:
   - press **Enter** or type **1-4** to run a built-in demo (table below), or
   - paste the **URL of your prediction** (a raw mmCIF or PDB file, not an upload), then the **PDB ID** of the experimental structure. If your file name starts with the PDB ID (for example `1y26_model.cif`), the notebook suggests it.
3. Results appear below the cell, and an HTML report is saved in `assets/report/`. Colab sessions are temporary, so download what you need.

## Built-in demos
| Option | RNA | PDB ID |
|---|---|---|
| Enter | L1 Ribozyme Ligase - circular | 2OIU |
| 1 | Adenine riboswitch aptamer | 1Y26 |
| 2 | Yeast tRNA-Phe | 1EHZ |
| 3 | THF riboswitch | 4LVV |
| 4 | Hammerhead ribozyme | 2OEU |
| 5 | Your own prediction: paste its URL, then the PDB ID | yours |

The demo predictions were made with AlphaFold Server (AlphaFold 3).

## What it does
- Matches the nucleotides of the prediction and the experimental structure by sequence alignment, superimposes them (least squares on P atoms, C4' where P is missing), and reports **RMSD, matched nucleotides and sequence identity**.
- Shows both structures side by side in 3D. The prediction is colored by the B-factor column of its file (pLDDT if your predictor stores it there).
- Adds 2D structure drawings and 2D distance heat maps for both structures (*experimental*).
- Leave the PDB ID blank to view your prediction on its own.
- RMSD only for now: no TM-score, lDDT or base-pair agreement yet.

## Known limitations
- Agreement with one experimental structure is not proof that a prediction is correct: RNAs are flexible, and crystal packing, ligands, ions or construct differences matter.
- Only the longest RNA chain of each file is used, and NMR entries use model 1 only.
- Residue names are matched against a built-in list, so a ligand with a nucleotide-like name can be counted (the bound adenine `ADE` in 1Y26) and an unusual residue skipped (the 5' `GTP` in 2OEU). The superposition atom (P, else C4') is chosen per nucleotide, which can shift the RMSD slightly (about 0.08 Å in 1Y26).
- A valid but wrong PDB ID is not detected. Low sequence identity or few matched pairs gives no warning, so check both numbers.
- The 2D drawings call base pairs with a distance heuristic, not a base-pair annotator (no complementarity check, no pseudoknots).
- Tested on RNAs up to 155 nucleotides.

## Software used
Biopython, NumPy, pandas, SciPy, PyYAML, py3Dmol, matplotlib, seaborn, pytest and ViennaRNA (2D drawings). Versions are not pinned.

Cock PJA, et al. Biopython: freely available Python tools for computational molecular biology and bioinformatics. *Bioinformatics* 2009;25(11):1422-1423. doi:10.1093/bioinformatics/btp163

## License
MIT License. See `LICENSE`.
