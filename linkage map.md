## Generate LG using STACKS to demultiplex single-end reads:

```java
# from EMILY on 8, @/mnt/md0/zachary/GBS_data/GB-eaSy/Sample_data$ process_radtags -f CPB_1.fastq.gz -b barcode_key.txt -e apeKI -o barcoded_fastq/

## note, inline barcodes, 96 barcodes for 76
#233320936 total sequences
# 2654625 barcode not found drops (1.1%)
#        0 low quality read drops (0.0%)
#  2352795 RAD cutsite not found drops (1.0%)
#228313516 retained reads (97.9%)

```
## align reads to reference using BWA:
parallel --max-procs $NUM_CORES --keep order --link "bwa mem $REF_GE {} |

