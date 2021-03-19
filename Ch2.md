## rerun minigraph with larger MD sample:

molecularecology@Chimborazo:/media/Summit/zach_vg/minigraph$ ./minigraph/minigraph -xggs -t4 /media/Summit/zach_vg/vg/F_Kansas_60.fasta /media/Summit/zach_vg/vg/F_Oregon_60.fasta /media/Summit/zach_vg/vg/Ldec_2018LI_60.fasta /media/Summit/zach_vg/vg/Mexi_60.fasta /media/Summit/zach_vg/vg/M_MD_contigs2.fasta > CPB_Mar18.gfa
```bash
## convert gfa to vg using vg build:

# first converted minigraph .gfa -> vg using CI docker suggestion: 
$ docker run -v $(pwd):/data --rm quay.io/vgteam/vg:ci-2785-69b052f68df85d69f80f0ad52f685ef05ac3dc60 vg convert 
-g /data/CPB_Feb5.gf -v > CPB_Feb5.vg

# prune 
./vg prune -r -p -t 32 CPB_Feb5.vg  > CPB_Feb5.pruned.vg

# modify for large bubbles:
./vg mod -X 256 CPB_Feb5.pruned.vg > mod_CPB_Feb5.pruned.vg

# the call error occurred in the docker container, so I then used the vg from the step above on the newest vg binaries v 1.30.0 and the issue persisted:
#index = xg
./vg index -x mod_CPB_Feb5.pruned.xg mod_CPB_Feb5.pruned.vg

# index = gcsa
./vg index -g mod_CPB_Feb5.pruned.gcsa mod_CPB_Feb5.pruned.vg -t 32 -b ./ -p

# map *error*
./vg map -t 16 -x CPB_Feb5_1.30.xg -g CPB_Feb5_1.30.gcsa -i -f CPBWGS_11_R1.fastq.gz -f CPBWGS_11_R2.fastq.gz > CPB_11.gam
```
## generate bed file with bubbles


## map pooled reads to variantgraph

## surject gams to bams

## pooled whole genome sequences -> selection and differentiation popoolation2, pcadapt 

# for example MD_1 generate plink.bed file: 
```bash
# normalize
molecularecology@Chimborazo:/media/Summit/plink$ bcftools norm -Ob -m-any genotypes_CPB_MD_1.vcf > MD_1.norm.bcf

# index
bcftools index MD_1.norm.bcf

#generate (PLINK v1.90b6.21 64-bit (19 Oct 2020)          www.cog-genomics.org/plink/1.9/)
./plink --bcf MD_1.norm.bcf --aec --make-bed --out bed_genotypes_MD1
1 person (0 males, 0 females, 1 ambiguous) loaded from .fam.
Ambiguous sex ID written to bed_genotypes_MD1.nosex .
Using 1 thread (no multithreaded calculations invoked).
Before main variant filters, 1 founder and 0 nonfounders present.
Calculating allele frequencies... done.
2095554 variants and 1 person pass filters and QC.
Note: No phenotypes present.
--make-bed to bed_genotypes_MD1.bed + bed_genotypes_MD1.bim +
bed_genotypes_MD1.fam ... done.

## upload to R, PCAdapt, shared variant sites?
```
