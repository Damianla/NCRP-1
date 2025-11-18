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

yaml
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
### Input file
NCRP expects two main inputs:

1.classification file

The standard per-read output:
```
C   read_0001   1345   ...
U   read_0002   0       ...
```
2.overlap graph

You can provide the graph in two formats:
- minimap2 PAF(--paf) : NCRP parses the file and builds an overlap graph,keeping the best overlap for each read pair.
- Sample edge list(--edges) : a 3-column,tab-delimitered file:
```
readA   readB   350
readB   readC   420
...
```
where the third column is the overlap length. Exactly one of --paf or --edges must be provided.
### Testing your NCRP installation
After installing NCRP and preparing a small test dataset, you can run:
```
cd NCRP
python ncrp_main.py \
  --kraken tests/example.kraken \
  --paf tests/example.paf \
  --output tests/ncrp_labels.tsv
```
If the command finishes successfully and tests/ncrp_labels.tsv is created, your installation works.

To see all available options:
```
python ncrp_main.py --help
```
### Base Usage
```
python ncrp_main.py \
  --kraken path/to/reads.kraken \
  --paf path/to/overlaps.paf \
  --min-overlap 130 \
  --hist-bin 100 \
  --output ncrp_final_labels.tsv
```
### Important command-line options
```
--kraken            Kraken2 per-read output file (required)
--paf               minimap2 PAF overlap file (optional; mutually exclusive with --edges)
--edges             simple edge list "read1 read2 overlap" (optional; mutually exclusive with --paf)
--min-overlap       minimum overlap length (bp) to keep an edge (default: 130)
--hist-bin          bin width (bp) for textual overlap histogram (default: 100)
--output            output file for final labels (default: final_labels.tsv)

--plot-overlap-png  save overlap-length histogram as PNG
--plot-degree-png   save degree histogram as PNG
--plot-weight-png   save normalized weight histogram as PNG
--dpi               DPI for PNG figures (default: 300)
--logy              use log-scale on the y-axis of histograms
```
