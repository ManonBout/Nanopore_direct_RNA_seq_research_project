# EpiNano-SVM for the detection of mRNA modifications in NHA-hTERT Nanopore direct RNA seq data


### Preparation of the files

 ```sh
# Running EpiNano-SVM from a docker container 

# Create sorted bam file:
samtools sort --threads 4 -O BAM -o /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/flair_workflow_for_EpiNano/NHA_hTERT_DRNA_20220609_self_transcript_aligned.sorted.bam /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/flair_workflow_for_EpiNano/NHA_hTERT_DRNA_20220609_self_transcript_aligned.bam

# Create an indexed sorted bam file:
samtools index /public/groups/treehouse/nanopore/primary/derived/NHA-hTERT_DRNA_20220609/flair_workflow_for_EpiNano/NHA_hTERT_DRNA_20220609_self_transcript_aligned.sorted.bam

# Create an indexed fasta file from the reference flairome, created by FLAIR:
samtools faidx NHA_hTERT_DRNA_20220609_flair_collapse_output.isoforms.fa

# Create a fa.dict file from the fasta file:
java -jar /usr/local/bin/picard.jar CreateSequenceDictionary R=NHA_hTERT_DRNA_20220609_flair_collapse_output.isoforms.fa O=NHA_hTERT_DRNA_20220609_flair_collapse_output.isoforms.fa.dict
```


### Running EpiNano-SVM on NHA-hTERT

## Step 1. Extract base-calling error features

```sh 
#EpiNano_Variants:
python3 /usr/local/bin/EpiNano/Epinano_Variants.py -R /usr/local/bin/EpiNano/NHA_data/NHA_hTERT_DRNA_20220609_flair_collapse_output.isoforms.fa -b /usr/local/bin/EpiNano/NHA_data/NHA_hTERT_DRNA_20220609_self_transcript_aligned.sorted.bam -s /usr/local/bin/sam2tsv.jar -T t

# Output csv file contains base-calling ‘error’ information for each reference position.
```
```sh
# Organize the variants in 5-mers:
python3 /usr/local/bin/EpiNano/misc/Slide_Variants.py /usr/local/bin/EpiNano/NHA_data/NHA_hTERT_DRNA_20220609_self_transcript_aligned.sorted.plus_strand.per.site.csv 5
```

#### STEP 2. Predict RNA modifications

```sh 
# EpiNano_Predict:
python3 /usr/local/bin/EpiNano/Epinano_Predict.py --model /usr/local/bin/EpiNano/models/rrach.q3.mis3.del3.linear.dump --predict NHA_hTERT_DRNA_20220609_self_transcript_aligned.sorted.plus_strand.per.site.5mer.csv --columns 8,13,23 --out_prefix NHA_hTERT_DRNA_20220609_output_mod_prediction
```

### Filtering the dataset for RRACH motif

```sh
# Filter the data to only keep RRACH motif 5-mers 
sh /usr/local/bin/EpiNano/test_data/make_predictions/RRACH_kmer_filter.sh -i /usr/local/bin/EpiNano/NHA_data/NHA_hTERT_DRNA_20220609_output_mod_prediction.q3.mis3.del3.MODEL.rrach.q3.mis3.del3.linear.dump.csv -o /usr/local/bin/EpiNano/NHA_data/NHA_hTERT_data_output_mod_prediction_RRACH_filter_out.csv
```

### Filtering the dataset to determine amount of A's

```sh
# Filter the dataset for 5-mers with an A in the middle
sh /usr/local/bin/EpiNano/DIPG-IV_data/complete_DIPG_data/NNANN_kmer_filter.sh -i /usr/local/bin/EpiNano/NHA_data/NHA_hTERT_DRNA_20220609_output_mod_prediction.q3.mis3.del3.MODEL.rrach.q3.mis3.del3.linear.dump.csv -o NHA_hTERT_data_output_mod_prediction_NNANN_filter_out.csv

# Run following command to count the amount of A's
wc -l NHA_hTERT_data_output_mod_prediction_NNANN_filter_out.csv
```