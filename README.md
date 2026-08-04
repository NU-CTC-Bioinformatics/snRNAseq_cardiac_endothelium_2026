# Ischemia Reperfusion in Human Cardiac Endothelium

Analysis code for the single-nucleus RNA sequencing (snRNA-seq) analysis described in [MANUSCRIPT CITATION — add once available].

## Overview

This repository contains the full analysis pipeline used to process, annotate, and analyze snRNA-seq data from human donor hearts subjected to cold static storage (HTK solution) and reperfusion. The analysis identifies endothelial cell subtypes (arterial, microvascular, venular) and characterizes their transcriptional response across three timepoints: Baseline, 10h cold storage, and Perfused.

## Data Availability

Raw and processed sequencing data are publicly available from the original study (Lei et al., *Nature Cardiovascular Research*, 2025; [https://doi.org/10.1038/s44161-025-00653-x](https://doi.org/10.1038/s44161-025-00653-x)), deposited under GEO accession [GSE261124](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE261124). This analysis uses sample `GSM8135503` and is restricted to the untreated HTK preservation arm (excluding the canrenone-treated samples in the original dataset).

## Repository Structure

```
├── code/
│   ├── Lantz_snRNAseq_analysis.Rmd      # Full analysis pipeline (source code)
│   └── Lantz_snRNAseq_analysis.html     # Knitted report — view figures/tables without running R
├── DE_Genes/                            # Output directory for differential expression CSV results
├── README.md
└── LICENSE
```

The `.html` file is self-contained (all figures/tables embedded) — download it and open it in any browser to view the full report, no R installation required.

## Pipeline Summary

The analysis proceeds through the following stages (see the R Markdown file for full detail and rationale at each step):

1. **Import & Subsetting** — Seurat object construction from the raw count matrix; isolation of HTK-only samples.
2. **Quality Control** — per-nucleus QC metrics, doublet detection (`scDblFinder`), multi-criteria filtering.
3. **Normalization & Integration** — cell cycle scoring, `SCTransform` (per-sample), Harmony batch correction via `IntegrateLayers`.
4. **Cell Annotation** — resolution sweep, `clustree` analysis, canonical + unbiased marker validation, manual cluster annotation.
5. **Endothelial Cell Sub-Analysis** — isolation and re-analysis of the three endothelial subtypes.
6. **Differential Gene Expression** — pairwise MAST comparisons across the storage/reperfusion timecourse within Microvascular ECs.

## Requirements

This analysis was run in R (version noted in `sessionInfo()` at the end of the `.Rmd` output) using the following key packages:

- `Seurat` (v5) — single-cell/nucleus analysis framework
- `SCTransform`, `glmGamPoi` — normalization
- `harmony` — batch integration
- `scDblFinder` — doublet detection
- `clustree` — clustering resolution selection
- `MAST` — differential expression testing
- `kableExtra`, `ggplot2`, `patchwork`, `cowplot` — visualization and reporting

A full, versioned package list is available in the `sessionInfo()` output at the end of the knitted report.

## Reproducing This Analysis

1. Download the raw `.h5` file for `GSM8135503` from GEO accession GSE261124.
2. Update the `base_dir` variable near the top of `code/Lantz_snRNAseq_analysis.Rmd` to point to your local copy of the raw data.
3. Knit the R Markdown file in RStudio (or via `rmarkdown::render()`).

## Citation

If you use this code, please cite the associated manuscript: [ADD FULL CITATION ONCE PUBLISHED]

This repository is also archived on Zenodo with a DOI corresponding to the exact code version used in the publication: [![DOI](https://zenodo.org/badge/1322450324.svg)](https://doi.org/10.5281/zenodo.21783591)

## Contact

Connor W. Lantz, 
Northwestern University
connor.lantz@northwestern.edu

## License

This project is licensed under the [MIT License](LICENSE) — see the LICENSE file for details.
