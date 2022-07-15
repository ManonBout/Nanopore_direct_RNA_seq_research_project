# DIPG-IV

### Run#1

### Guppy v6.0.6

```sh 
# Define the variables:
cfg=/data/miten/guppy_6.0.6/ont-guppy/data/rna_r9.4.1_70bps_hac_prom.cfg
fast5=/public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314/20220315_0025_MN36450_FAS62838_efe61d48/fast5 fastq_out=/public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data

# Basecall command for Guppy v6.0.6: 
/data/miten/guppy_6.0.6/ont-guppy/bin/guppy_basecaller -i  $fast5 -s $fastq_out --device "cuda:all" -c $cfg --reverse_sequence yes --u_substitution yes
```
```sh
# Combine fastq pass files into one pass fastq.gz file
# Define the variables:
fastqs_to_combine=/public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/pass/*
output_fastq=/public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/DIPG-IV_DRNA_20220314_Guppy_6.0.6_pass.fastq.gz


#Command to combine the files:
cat $fastqs_to_combine > $output_fastq
```


### Guppy v3.1.5:

```sh 
# Define the variables:
cfg=/public/groups/treehouse/bin/guppy_cpu_3.1.5/ont-guppy-cpu/data/rna_r9.4.1_70bps_hac_prom.cfg
fast5=/public/groups/treehouse/nanopore/primary/original/DIPG-IV_DRNA_20220314/20220315_0025_MN36450_FAS62838_efe61d48/fast5
fastq_out=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_Guppy_3.1.5_basecalled_data


# Basecall command for Guppy v3.1.5:
/public/groups/treehouse/bin/guppy_cpu_3.1.5/ont-guppy-cpu/bin/guppy_basecaller -i  $fast5 -s $fastq_out -c $cfg --compress_fastq --qscore_filtering --calib_detect
```
```sh
#Combine fastq pass files into one pass fastq.gz file
# Define the variables:
fastqs_to_combine=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_Guppy_3.1.5_basecalled_data/pass/*
output_fastq=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_Guppy_3.1.5_basecalled_data/DIPG-IV_DRNA_20220314_Guppy_3.1.5_pass.fastq.gz


#Command to combine the files:
cat $fastqs_to_combine > $output_fastq
```



### Run#2

### Guppy v6.0.6

```sh 
# Define the variables:
cfg=/data/miten/guppy_6.0.6/ont-guppy/data/rna_r9.4.1_70bps_hac_prom.cfg
fast5=/public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401/20220401_2340_MN36450_FAS49730_4fb0104a/fast5 fastq_out=/public/groups/treehouse/nanopore/primary/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data

# Basecall command for Guppy v6.0.6: 
/data/miten/guppy_6.0.6/ont-guppy/bin/guppy_basecaller -i  $fast5 -s $fastq_out --device "cuda:all" -c $cfg --reverse_sequence yes --u_substitution yes
```
```sh
#Combine fastq pass files into one pass fastq.gz file
# Define the variables:
fastqs_to_combine=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data/pass/*
output_fastq=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data/DIPG-IV_DRNA_20220401_Guppy_6.0.6_pass.fastq.gz


#Command to combine the files:
cat $fastqs_to_combine > $output_fastq
```


### Guppy v3.1.5:

```sh 
# Define the variables:
cfg=/public/groups/treehouse/bin/guppy_cpu_3.1.5/ont-guppy-cpu/data/rna_r9.4.1_70bps_hac_prom.cfg
fast5=/public/groups/treehouse/nanopore/primary/original/DIPG-IV_DRNA_20220401/20220401_2340_MN36450_FAS49730_4fb0104a/fast5
fastq_out=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_3.1.5_basecalled_data

# Basecall command for Guppy v3.1.5:
/public/groups/treehouse/bin/guppy_cpu_3.1.5/ont-guppy-cpu/bin/guppy_basecaller -i  $fast5 -s $fastq_out -c $cfg --compress_fastq --qscore_filtering --calib_detect
```
```sh
#Combine fastq pass files into one pass fastq.gz file
# Define the variables:
fastqs_to_combine=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_3.1.5_basecalled_data/pass/*
output_fastq=/public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_3.1.5_basecalled_data/DIPG-IV_DRNA_20220401_Guppy_3.1.5_pass.fastq.gz

#Command to combine the files:
cat $fastqs_to_combine > $output_fastq
```