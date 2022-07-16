# Assessing the longest high quality, mapped reads in the DIPG-IV combined Nanopore direct RNA seq data


### Filtering of bam file created after flairome alignment

```sh 
# Filter the longest well-mapped reads (mapping score of 60) in the whole dataset:
samtools view full_fq_to_sample_transcripts_output.sorted.bam | awk '$5  > 59' | less | awk '{print $1"\t"length($10)}' | sort -k 2 -n  

# Output:
ed968b88-73b3-4d32-9b3d-7d04e7a3072a	15093
4075caaf-f8e4-41e4-b9ee-2ed06dc8c889	15373
4cf72346-126d-4ad4-9e23-31372e574714	15706
5e97e85c-2e7c-4ffc-9840-2a5409c62ea2	15720
4ffd9bfc-6815-47f1-aeb6-536e93b37026	15731
fbdde36e-7fb7-43eb-aa5e-83a16d8d4853	16231
2e47ccb1-ea92-42c4-a1c2-8df2dcf505e0	16422
b3739b5b-9334-42f7-abc8-e09578bc72e6	16797
84d23b20-2315-4471-88ba-97fa284bcb30	18489
1ea563e5-4545-498e-ac3c-67870aba0647	18758
```

```sh
# Look at the longest read:
samtools view full_fq_to_sample_transcripts_output.sorted.bam | grep b3739b5b-9334-42f7-abc8-e09578bc72e6 |  cut -f1-5

# Output:
1ea563e5-4545-498e-ac3c-67870aba0647	0	be7f4ca7-3603-412e-9af7-9d85d7bb1d95_ENSG00000115306.16	24	60
```

```sh 
# Find the sequence of this longest read:
samtools view full_fq_to_sample_transcripts_output.sorted.bam | grep 1ea563e5-4545-498e-ac3c-67870aba0647 

# Sequence can be used to visualize in IGV or UCSC genome browser
```
