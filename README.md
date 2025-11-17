# NCRP

NCRP: a graph-based framework for improving long-read metagenomic classification via neighborhood-consistency refinement and label propagation on the overlap graph.

- [Installation](#installation)
  - [With Conda](#with-conda)
    - [From yaml file](#from-yaml-file)
- [Input files](#input-files)
- [Testing your NCRP installation](#testing-your-ncrp-installation)
- [Basic Usage](#basic-usage)
- [Main output files](#main-output-files)
- [Advanced usage](#advanced-usage)
  - [Using an edge list instead of PAF](#using-an-edge-list-instead-of-paf)
  - [Tuning overlap and plotting diagnostics](#tuning-overlap-and-plotting-diagnostics)
- [Simulation script](#simulation-script)
  - [Reference preparation](#reference-preparation)
  - [Basic usage](#simulation-basic-usage)
- [Citation](#citation)

---

## Installation

### With Conda

We recommend installing NCRP in a dedicated conda environment.

#### From yaml file

Create a file called `environment.yml` in the repository root:

```yaml
name: ncrp
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - python>=3.8
  - matplotlib
Then create and activate the environment:
conda env create -f environment.yml
conda activate ncrp
