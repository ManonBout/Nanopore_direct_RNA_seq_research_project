# xPore for the detection of mRNA modifications


### Preparations to use xPore

 ```sh
# Access conda:
conda activate
 
# Install xpore:
conda create -n xpore
 
# Activate xpore:
conda activate xpore
 
# Install minimap2 (v2.22):
conda install minimap2 -c bioconda
 
# Install nanopolish:
conda install nanopolish -c bioconda


# Install xpore:
conda install datacache -c conda-forge
conda install memoized-property -c conda-forge
conda install serializable -c conda-forge
conda install tinytimer -c conda-forge
conda install typechecks -c conda-forge
 
conda install xpore -c bioconda
 
# Download gtf annotation file v38
wget https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_38/gencode.v38.annotation.gtf.gz
```


### Minimap2 transcriptome (GRCh38 human) alignment of the Guppy v6.0.6 basecalled data

#### NHA-hTERT

```sh 
# Transcriptome alignment command:
minimap2 -ax map-ont -uf -t 10 --secondary=no gencode.v38.transcripts.fa.gz /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_pass.fastq.gz > NHA-hTERT_DRNA_20220609.transcriptome_aligned.sam
```
```sh
#Convert sam to sorted bam file:
samtools view -Sb NHA-hTERT_DRNA_20220609.transcriptome_aligned.sam | samtools sort -o NHA-hTERT_DRNA_20220609.transcriptome_aligned.bam -

# Index sorted bam file:
samtools index NHA-hTERT_DRNA_20220609.transcriptome_aligned.bam &>> NHA-hTERT_DRNA_20220609.transcriptome_aligned.bam.bai
```

#### DIPG-IV Run#1

```sh 
# Transcriptome alignment command:
minimap2 -ax map-ont -uf -t 10 --secondary=no gencode.v38.transcripts.fa.gz /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/DIPG-IV_DRNA_20220314_Guppy_6.0.6_pass.fastq.gz > DIPG-IV_DRNA_20220314.transcriptome_aligned.sam
```
```sh
#Convert sam to sorted bam file:
samtools view -Sb DIPG-IV_DRNA_20220314.transcriptome_aligned.sam | samtools sort -o DIPG-IV_DRNA_20220314.transcriptome_aligned.bam -

# Index sorted bam file:
samtools index DIPG-IV_DRNA_20220314.transcriptome_aligned.bam &>> DIPG-IV_DRNA_20220314.transcriptome_aligned.bam.bai
```

#### DIPG-IV Run#2

```sh 
# Transcriptome alignment command:
minimap2 -ax map-ont -uf -t 10 --secondary=no gencode.v38.transcripts.fa.gz /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data/DIPG-IV_DRNA_20220401_Guppy_6.0.6_pass.fastq.gz > DIPG-IV_DRNA_20220401.transcriptome_aligned.sam
```
```sh
#Convert sam to sorted bam file:
samtools view -Sb DIPG-IV_DRNA_20220401.transcriptome_aligned.sam | samtools sort -o DIPG-IV_DRNA_20220401.transcriptome_aligned.bam -

# Index sorted bam file:
samtools index DIPG-IV_DRNA_20220401.transcriptome_aligned.bam &>> DIPG-IV_DRNA_20220401.transcriptome_aligned.bam.bai
```


### Resquiggle using nanopolish eventalign

#### NHA-hTERT

```sh 
nanopolish index -d /public/groups/treehouse/nanopore/primary/original/NHA-hTERT_DRNA_20220609/20220609_2141_MN36450_FAT24326_a4c4d924/fast5 /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_pass.fastq.gz

# Nanopolish eventalign
nanopolish eventalign --reads /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/xpore/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_pass.fastq.gz \
--bam /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/xpore/NHA-hTERT_DRNA_20220609.transcriptome_aligned.bam \
--genome /public/groups/treehouse/nanopore/primary/derived/gencode.v38.transcripts.fa \
--signal-index \
--scale-events \
--summary /public/groups/treehouse/nanopore/primary/original/NHA-hTERT_DRNA_20220609/20220609_2141_MN36450_FAT24326_a4c4d924/sequencing_summary_FAT24326_7ca35724.txt \
--threads 32 > /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/xpore/NHA-hTERT_DRNA_20220609.eventalign.txt
```

#### DIPG-IV Run#1

```sh
nanopolish index -d /public/groups/treehouse/nanopore/primary/original/DIPG-IV_DRNA_20220314/20220315_0025_MN36450_FAS62838_efe61d48/fast5 /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/DIPG-IV_DRNA_20220314_Guppy_6.0.6_pass.fastq.gz

# Nanopolish eventalign
anopolish eventalign --reads /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/xpore/DIPG-IV_DRNA_20220314_Guppy_6.0.6_pass.fastq.gz \
--bam /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/xpore/DIPG-IV_DRNA_20220314.transcriptome_aligned.bam \
--genome /public/groups/treehouse/nanopore/primary/derived/gencode.v38.transcripts.fa \
--signal-index \
--scale-events \
--summary /public/groups/treehouse/nanopore/primary/original/DIPG-IV_DRNA_20220314/20220315_0025_MN36450_FAS62838_efe61d48/sequencing_summary_FAS62838_83afdafe.txt \
--threads 32 > /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/xpore/DIPG-IV_DRNA_20220314.eventalign.txt

```

#### DIPG-IV Run#2

```sh
nanopolish index -d /public/groups/treehouse/nanopore/primary/original/DIPG-IV_DRNA_20220401/20220401_2340_MN36450_FAS49730_4fb0104a/fast5 /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data/DIPG-IV_DRNA_20220401_Guppy_6.0.6_pass.fastq.gz

# Nanopolish eventalign
nanopolish eventalign --reads /scratch/mvanden1/DIPG-IV_DRNA_20220401_Guppy_6.0.6_pass.fastq.gz \
--bam DIPG-IV_DRNA_20220401.transcriptome_aligned.bam \
--genome gencode.v38.transcripts.fa \
--signal-index \
--scale-events \
--summary /public/groups/treehouse/nanopore/primary/original/DIPG-IV_DRNA_20220401/20220401_2340_MN36450_FAS49730_4fb0104a/sequencing_summary_FAS49730_1077e191.txt \
--threads 32 > /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data/xpore/DIPG-IV_DRNA_20220401.eventalign.txt

```


### Data preparation xPore

#### NHA-hTERT

```sh
xpore dataprep \
--eventalign /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/NHA-hTERT_DRNA_20220609_Guppy_6.0.6_basecalled_data/xpore/NHA-hTERT_DRNA_20220609.eventalign.txt \
--gtf_or_gff /scratch/mvanden1/gencode.v38.annotation.gtf.gz \
--transcript_fasta /scratch/mvanden1/gencode.v38.transcripts.fa \
--n_processes 16 \
--out_dir /scratch/mvanden1/NHA-hTERT_dataprep
```

#### DIPG-IV Run#1

```sh
xpore dataprep \
--eventalign /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314/DIPG-IV_DRNA_20220314_basecalled_data/xpore/DIPG-IV_DRNA_20220314.eventalign.txt \
--gtf_or_gff /scratch/mvanden1/gencode.v38.annotation.gtf.gz \
-transcript_fasta /scratch/mvanden1/gencode.v38.transcripts.fa \
--n_processes 16 \
--out_dir /scratch/mvanden1/DIPG-IV_DRNA_20220314_dataprep
```

#### DIPG-IV Run#2

```sh
xpore dataprep \
--eventalign /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220401/DIPG-IV_DRNA_20220401_Guppy_6.0.6_basecalled_data/xpore/DIPG-IV_DRNA_20220401.eventalign.txt \
--gtf_or_gff /scratch/mvanden1/gencode.v38.annotation.gtf.gz \
--transcript_fasta /scratch/mvanden1/gencode.v38.transcripts.fa \
--n_processes 16 \
--out_dir /scratch/mvanden1/DIPG-IV_DRNA_20220401_dataprep
```

### Convert data into .yaml files

```sh
# Create file with nano in terminal:
nano config.yaml

# Paste in this file:
notes: Pairwise comparison without replicates with default parameter setting.
 
data:
	NHA:
    	rep1: /data/scratch/mvanden1/NHA-hTERT_dataprep
	DIPG:
    	rep1: /data/scratch/mvanden1/DIPG-IV_DRNA_20220314_dataprep
    	rep2: /data/scratch/mvanden1/DIPG-IV_DRNA_20220401_dataprep
 
out: ./out # output dir

# Save and press enter

# Activate conda xpore:
conda activate xpore
 
# Command to start the convertion to .yaml files:
xpore diffmod --config config.yaml --resume --n_processes 16
```

### Post-processing 

```sh
xpore postprocessing --diffmod_dir out
```

### Filter the file on RRACH motif 5-mers

```sh
# A script was made to do this
# Run:
sh xPORE_RRACH_filter.sh -i [PATH TO FILE TO BE FILTERED] -o [OUTPUT FILE NAME]
```