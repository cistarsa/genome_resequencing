# Generate canu assemblies on CHTC using long read pacbio and short read illumina:


@ zcohen3@submit-2.chtc.wisc.edu:/home/zcohen3/mdx_plains_LARGE.sh
```bash
$canu \
-p F1 -d ${out_fn} \
genomeSize=650m \
-haplotypePM repaired_CPBP2M.fq.gz \
-haplotypePF repaired_CPBP2F.fq.gz \
-pacbio-raw CPBF1_cat.fq.gz 
```

@'''/mdx_plains_LARGE.sub

```bash
transfer_input_files =/mnt/gluster/zcohen3/repaired_CPB2f.fq.gz, /mnt/gluster/zochen3/repaired_CPB2M.fq.gz, /mnt/gluster/zcohen3/CPBF1_cat.fq.gz, canu.tar.gz

etc. etc.
```

### remap Ldecv2 genes using minimap2 on CHTC, interactively?:
```bash
bash-4.2$ ./minimap2-2.17_x64-linux/minimap2 -x asm10 (varied) F1-haplotypePF.contigs_v2.fasta GCF_000500325.1_Ldec_2.0_cds_from_genomic.fna -o F1_PF_Ld2_CDS-asm10.pah

for f in *paf; do for j in `cat "$f" | awk '{print $1}' | wc -l`; do for z in `cat "$f" | awk '{print $1}' | sort -u | wc -l`; do for q in `cat "$f" | awk '{print $6}' | sort -u | wc -l`;
do echo "$f" hits "$j" unique "$z" scaffs "$q" ; done; done; done; done

```

F1_PF_Ld2_CDS-asm10.paf hits 79814 unique 18999 scaffs 426

## determine shared and unique scaffolds per assembly that 1) dont have any Ldec genes on them and 2) are not shared between the two haploid assemblies 


