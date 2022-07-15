# NHA-hTERT

### PycoQC (Guppy v6.0.6 basecalled data)

```sh 
# Activate conda environment to run PycoQC on personal computer:
conda activate pycoQC

# Run PycoQC command:
pycoQC -f /Users/manon/Desktop/Nanopore-data\ analysis/NHA-hTERT_DRNA_20220609/sequencing_summary.txt \
-o /Users/manon/Desktop/Nanopore-data\ analysis/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data_pycoQC_output.html

# Deactivate conda environment:
conda deactivate
```


### Nanoplot (Guppy v6.0.6 basecalled data)

```sh 
# Nanoplot command:
NanoPlot --summary /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/sequencing_summary.txt \
-o /public/groups/treehouse/nanopore/secondary/NHA-hTERT_DRNA_20220609/Nanoplot_output
```

