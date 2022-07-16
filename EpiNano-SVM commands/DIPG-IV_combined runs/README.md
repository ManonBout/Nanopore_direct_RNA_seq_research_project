# EpiNano-SVM for the detection of mRNA modifications in the DIPG-IV combined Nanopore direct RNA seq data


### Preparation of the files

 ```sh
# Running EpiNano-SVM from a docker container 

# Create sorted bam file:
samtools sort --threads 4 -O BAM -o /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314-20220401//full_fq_to_sample_transcripts_output.sorted.bam /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314-20220401/flair_workflow_for_EpiNano/full_fq_to_sample_transcripts/full_fq_to_sample_transcripts_output.bam

# Create an indexed sorted bam file:
samtools index /public/groups/treehouse/nanopore/primary/derived/DIPG-IV_DRNA_20220314-20220401/full_fq_to_sample_transcripts_output.sorted.bam

# Create an indexed fasta file from the reference flairome, created by FLAIR:
samtools faidx DIPG_IV_DRNA_20220314_and_20220401_flair_collapse_output.isoforms.fa

# Create a fa.dict file from the fasta file:
java -jar picard.jar CreateSequenceDictionary R=DIPG_IV_DRNA_20220314_and_20220401_flair_collapse_output.isoforms.fa O=DIPG_IV_DRNA_20220314_and_20220401_flair_collapse_output.isoforms.fa.dict
```


## Running EpiNano-SVM on DIPG-IV combined data

### Step 1. Extract base-calling error features

```sh 
#EpiNano_Variants:
python3 /usr/local/bin/EpiNano/Epinano_Variants.py -R /usr/local/bin/EpiNano/DIPG-IV_data/complete_DIPG_data/Run2/DIPG_IV_DRNA_20220314_and_20220401_flair_collapse_output.isoforms.fa -b /usr/local/bin/EpiNano/DIPG-IV_data/complete_DIPG_data/Run2/full_fq_to_sample_transcripts_output.sorted.bam -s /usr/local/bin/sam2tsv.jar -T t

# Output csv file contains base-calling ‘error’ information for each reference position.
```
```sh
# Organize the variants in 5-mers:
python3 /usr/local/bin/EpiNano/misc/Slide_Variants.py /usr/local/bin/EpiNano/DIPG-IV_data/complete_DIPG_data/Run2/full_fq_to_sample_transcripts_output.sorted.plus_strand.per.site.csv 5
```

### STEP 2. Predict RNA modifications

```sh 
# EpiNano_Predict:
python3 /usr/local/bin/EpiNano/Epinano_Predict.py --model /usr/local/bin/EpiNano/models/rrach.q3.mis3.del3.linear.dump --predict full_fq_to_sample_transcripts_output.sorted.plus_strand.per.site.5mer.csv --columns 8,13,23 --out_prefix full_fq_to_sample_transcripts_output_sorted_mod_prediction
```

#### Filtering the dataset for RRACH motif

```sh
# Filter the data to only keep RRACH motif 5-mers 
sh /usr/local/bin/EpiNano/test_data/make_predictions/RRACH_kmer_filter.sh -i /usr/local/bin/EpiNano/DIPG-IV_data/complete_DIPG_data/Run2/full_fq_to_sample_transcripts_output_sorted_mod_prediction.q3.mis3.del3.MODEL.rrach.q3.mis3.del3.linear.dump.csv -o full_fq_to_sample_transcripts_output_mod_prediction_RRACH_filter_out.csv
```

#### Filtering the dataset to determine amount of A's

```sh
# Filter the dataset for 5-mers with an A in the middle
sh /usr/local/bin/EpiNano/DIPG-IV_data/complete_DIPG_data/NNANN_kmer_filter.sh -i /usr/local/bin/EpiNano/DIPG-IV_data/complete_DIPG_data/Run2/full_fq_to_sample_transcripts_output_sorted_mod_prediction.q3.mis3.del3.MODEL.rrach.q3.mis3.del3.linear.dump.csv -o full_fq_to_sample_transcripts_output_sorted_mod_prediction_NNANN_filter_out.csv

# Run following command to count the amount of A's
wc -l full_fq_to_sample_transcripts_output_sorted_mod_prediction_NNANN_filter_out.csv
```