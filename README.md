# FoldCheck-RNA: Automated Nucleic Acid Structural Integrity & Biophysical Validation Suite

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mirikrupkin/foldcheck-rna/blob/main/foldcheck-rna.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)

**Author:** [Dr. Miri Krupkin](https://linkedin.com/in/mirikrupkin) (Applied AI Research Scientist & Computational Biologist)
**Description:** Production-grade architecture for automated nucleic acid structural model validation, stoichiometry-aware monomer isolation, and coarse-grained phosphorus backbone alignment against empirical experimental ground truth.

---

## 🧬 Project Overview
`FoldCheck-RNA` is a high-throughput computational pipeline designed to bridge generative structural predictions (such as AlphaFold 3) with empirical validation data from X-ray crystallography and Cryo-EM (RCSB PDB). Standard RNA structural alignments often break down when handling crystal packing dimers, symmetry mates, or unmanaged non-canonical nucleotide modifications.

This suite introduces programmatic robustness checks, automated multi-case FASTA sequence extraction, and biophysical confidence mapping to flag AI hallucination risks and global structural compaction errors in RNA models.

---

## 🛠️ Tech Stack
* **Language & Core:** Python 3.10+, NumPy, pandas, PyYAML
* **Structural Bioinformatics:** BioPython (`MMCIFParser`, `Superimposer`, `PDBIO`), py3Dmol, SciPy (`linear_sum_assignment`, `ConvexHull`)
* **Testing & Infrastructure:** PyTest, RCSB PDB REST architecture, Jupyter interactive sandbox

---

## 📂 Repository Architecture

```text
structural-ai-validation-suite/
│
├── src/
│   ├── constants.py      # Comprehensive RNA modification dictionary & solvent ion filters
│   ├── fetcher.py        # Automated coordinate downloading & EBI API ingestion handlers
│   ├── alignment.py      # Stoichiometry parser, pairwise aligner, and P-backbone superimposer
│   └── metrics.py        # pLDDT confidence mapping and structural state analyzer
│
├── data/                 # Experimental mmCIF files, target predictions, and multi-case FASTA
│   └── all_benchmark_sequences.fasta
│
├── configs/              # Centralized hyperparameter configuration
│   └── config.yaml
│
├── assets/               # Compiled publication assets
│   ├── tables/           # Master benchmark summaries (CSV & LaTeX formats)
│   └── report/           # Standalone interactive HTML 3D viewer comparison reports
│
├── tests/                # Automated pytest verification suite
│   └── test_pipeline.py
│
└── foldcheck_rna.ipynb   # Master executable Jupyter notebook with interactive 3D sandbox


```
---

## ⚙️ Key Technical Highlights

1. **Stoichiometry-Aware Monomer Filtering (src/alignment.py)**: Automatically detects and isolates functional monomer chains, stripping out crystal packing dimers and asymmetric unit contact artifacts prior to structural alignment.
2. **Coarse-Grained Phosphorus Backbone Alignment (src/alignment.py)**: Performs robust global superposition using phosphorus (P) backbone atoms to capture global fold geometry while filtering out local base torsion and stacking noise.
3. **Comprehensive Modification Registry (src/constants.py)**: Manages over 30 modified nucleotides (including 2'-O-methylations, pseudouridines, and methylated bases), mapping them back to standard canonical residues for accurate sequence alignment.
4. **Interactive 3D Visualization & HTML Reporting**: Renders synchronized, side-by-side Py3Dmol cartoon views comparing predictions against experimental ground truths, automatically archiving standalone HTML reports for citation.
5. **Interactive Sandbox & Auto-Fallback**: Features pre-configured case studies highlighting classical RNA structural folds plus a smart custom mode supporting any raw GitHub CIF URL.

---

 ## 🔬 Benchmarked Biological Case Studies
The interactive menu guides users through five distinct structural biology challenges:
* **[1] Adenine Riboswitch Aptamer**: Validates ligand-induced folding and purine-sensing pocket architecture (PDB: 1Y26).
* **[2] Yeast Phenylalanine tRNA**: Maps classical L-shaped tertiary stacking architecture and modified loop nucleosides (PDB: 1EHZ).
* **[3] THF Riboswitch Multi-Stem**: Isolates complex multi-stem junction topologies from crystal packing contacts (PDB: 4LVV).
* **[4] Hammerhead Ribozyme Core**: Accurately aligns catalytic core phosphate backbone for cleavage site evaluation (PDB: 2OEU).
* **[5] Custom Sandbox & Circular RNA Demo**: Input any raw GitHub CIF URL and 4-letter PDB code to benchmark custom models. Leaving the prompt blank automatically launches the default demonstration featuring the L1 Ribozyme Circular Adduct (PDB: 2OIU), highlighting topological failure modes of linear AI predictors.

---

## 🚀 Quickstart & Usage
1. **Run via Google Colab:** Click the badge at the top of this file to launch the master notebook instantly.
2. **Interactive Explorer**: Run foldcheck_rna.ipynb interactively to test built-in case studies or input custom prediction URLs. Completed validation sessions automatically archive citation-ready reports into assets/report/.

---

## 📚 References & Attribution
1. **AlphaFold 3 Architecture**: Abramson, J., et al. (2024). "Accurate structure prediction of biomolecular interactions with AlphaFold 3." Nature, 630(8016), 493–500.
2. **Biopython PDB Module**: Cock, P. J., et al. (2009). "Biopython: freely available Python tools for computational molecular biology and bioinformatics." Bioinformatics, 25(11), 1422–1423.
3. **Optimal Superposition (RMSD)**: Kabsch, W. (1976). "A solution for the best rotation to relate two sets of vectors." Acta Cryst. A, 32(5), 922–923.
4. **Global Chain Matching**: Munkres, J. (1957). "Algorithms for the assignment and transportation problems." J. Soc. Ind. Appl. Math., 5(1), 32–38.

 ---

## 📜 License
Distributed under the MIT License. See LICENSE for more information.
