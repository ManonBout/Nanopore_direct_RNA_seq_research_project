# NHA-hTERT

### Guppy v6.0.6

```sh 
# Define the variables:
cfg=/data/miten/guppy_6.0.6/ont-guppy/data/rna_r9.4.1_70bps_hac_prom.cfg
fast5=/public/groups/treehouse/nanopore/primary/original/NHA-hTERT_DRNA_20220609/20220609_2141_MN36450_FAT24326_a4c4d924/fast5 fastq_out=/public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data 

# Basecall command for Guppy v6.0.6: 
/data/miten/guppy_6.0.6/ont-guppy/bin/guppy_basecaller -i  $fast5 -s $fastq_out --device "cuda:all" -c $cfg --reverse_sequence yes --u_substitution yes --calib_detect
```
```sh
# Combine fastq pass files into one pass.fastq.gz file
# Define the variables:
fastqs_to_combine=/public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/pass/*
output_fastq=/public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_pass.fastq.gz

#Command to combine the files:
cat $fastqs_to_combine > $output_fastq
```


### Guppy v3.1.5:

```sh 
# Define the variables:
cfg=/public/groups/treehouse/bin/guppy_cpu_3.1.5/ont-guppy-cpu/data/rna_r9.4.1_70bps_hac_prom.cfg
fast5=/public/groups/treehouse/nanopore/primary/original/NHA-hTERT_DRNA_20220609/20220609_2141_MN36450_FAT24326_a4c4d924/fast5
fastq_out=/public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_3.1.5_basecalled_data

# Basecall command for Guppy v3.1.5:
/public/groups/treehouse/bin/guppy_cpu_3.1.5/ont-guppy-cpu/bin/guppy_basecaller -i  $fast5 -s $fastq_out -c $cfg --compress_fastq --qscore_filtering --calib_detect
```
```sh
# Combine fastq pass files into one pass.fastq.gz file
# Define the variables:
fastqs_to_combine=/public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_3.1.5_basecalled_data/pass/*
output_fastq=/public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_3.1.5_basecalled_data/NHA-hTERT_DRNA_20220609_Guppy_3.1.5_pass.fastq.gz

# Command to combine the files:
cat $fastqs_to_combine > $output_fastq
```
