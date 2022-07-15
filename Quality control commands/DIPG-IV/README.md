# DIPG-IV

### Run#1

### PycoQC (Guppy v6.0.6 basecalled data)

```sh 
# Activate conda environment to run PycoQC on personal computer:
conda activate pycoQC

# Run PycoQC command:
pycoQC -f /Users/manon/Desktop/Nanopore-data\ analysis/sequencing_summary.txt -o /Users/manon/Desktop/Nanopore-data\ analysis/DIPG-IV_DRNA_20220314_basecalled_data_pycoQC_output.html

# Deactivate conda environment:
conda deactivate
```


### Nanoplot (Guppy v6.0.6 basecalled data)

```sh 
# Nanoplot command:
NanoPlot --summary /public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/sequencing_summary.txt \
-o /public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220314/Nanoplot_output
```


### Run#2

### PycoQC (Guppy v6.0.6 basecalled data)

```sh 
# Activate conda environment to run PycoQC on personal computer:
conda activate pycoQC

# Run PycoQC command:
pycoQC -f /Users/manon/Desktop/Nanopore-data\ analysis/DIPG-IV_DRNA_20220401/sequencing_summary.txt -o /Users/manon/Desktop/Nanopore-data\ analysis/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_basecalled_data_pycoQC_output.html

# Deactivate conda environment:
conda deactivate
```


### Nanoplot (Guppy v6.0.6 basecalled data)

```sh 
# Nanoplot command:
NanoPlot --summary /public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data/sequencing_summary.txt -o /public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220401/Nanoplot_output
```