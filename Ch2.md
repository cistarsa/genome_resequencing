## rerun minigraph with larger MD sample:
```
molecularecology@Chimborazo:/media/Summit/zach_vg/minigraph$ ./minigraph/minigraph -xggs -t4 /media/Summit/zach_vg/vg/F_Kansas_60.fasta /media/Summit/zach_vg/vg/F_Oregon_60.fasta /media/Summit/zach_vg/vg/Ldec_2018LI_60.fasta /media/Summit/zach_vg/vg/Mexi_60.fasta /media/Summit/zach_vg/vg/M_MD_contigs2.fasta > CPB_Mar18.gfa
[M::main::11.373*0.28] loaded the graph from "/media/Summit/zach_vg/vg/F_Kansas_60.fasta"
[M::mg_index::237.637*0.30] indexed the graph
[M::mg_opt_update::248.441*0.29] occ_weight=20, occ_max1=250; 95 percentile: 3
[M::ggen_map::262.848*0.29] loaded file "/media/Summit/zach_vg/vg/F_Oregon_60.fasta"
[M::ggen_map::3006.234*0.89] mapped 3513 sequence(s) to the graph
[M::mg_ggsimple::3082.696*0.87] inserted 97086 events, including 4 inversions
[M::mg_index::3313.712*0.83] indexed the graph
[M::mg_opt_update::3325.857*0.83] occ_weight=20, occ_max1=250; 95 percentile: 3
[M::ggen_map::3338.027*0.83] loaded file "/media/Summit/zach_vg/vg/Ldec_2018LI_60.fasta"
[M::ggen_map::24257.707*0.93] mapped 26909 sequence(s) to the graph
[W::mg_ggsimple] query overlap on gchain 424: [>s21401:8369,>s21403:709|736] <=> LI_2018_scaffold554_size199581:[134208,134205|-3]
[M::mg_ggsimple::24288.924*0.93] inserted 50867 events, including 0 inversions
[M::mg_index::24525.231*0.92] indexed the graph
[M::mg_opt_update::24535.453*0.92] occ_weight=20, occ_max1=250; 95 percentile: 3
[M::ggen_map::24550.466*0.92] loaded file "/media/Summit/zach_vg/vg/Mexi_60.fasta"
[M::ggen_map::90226.085*0.92] mapped 230 sequence(s) to the graph
[M::mg_ggsimple::90457.949*0.91] inserted 148986 events, including 3 inversions
[M::mg_index::90733.589*0.91] indexed the graph
[M::mg_opt_update::90744.220*0.91] occ_weight=20, occ_max1=250; 95 percentile: 3
[M::ggen_map::90758.848*0.91] loaded file "/media/Summit/zach_vg/vg/M_MD_contigs2.fasta"
[M::ggen_map::185968.926*0.90] mapped 230 sequence(s) to the graph
[M::mg_ggsimple::186047.760*0.90] inserted 8080 events, including 1 inversions

```
## gfa -> bed (minigraph)
```bash
molecularecology@Chimborazo:/media/Summit/zach_vg/minigraph$ ../vg/gfatools/gfatools bubble CPB_Mar18.gfa > CPB_Mar18.bed
241413 CPB_Mar18.bed
<< 244756 (v1

```

## gfa to .fa 
```bash
./gfatools/gfatools gfa2fa -s CPB_Mar18.gfa > CPB_Mar18_linear.fa
[M::main] Version: 0.4-r214-dirty
[M::main] CMD: ./gfatools/gfatools gfa2fa -s CPB_Mar18.gfa
[M::main] Real time: 52.191 sec; CPU: 13.615 sec

```
## map OGS3 to linear.fa in minimap2
```bash
#1 
./minimap2/minimap2 -x splice CPB_Mar18_linear.fa Lepdec_OGS2.1.2.mfa > OGS3_CPB_Mar18.paf

#2

```

## pull reference alleles/paths:
```bash 
molecularecology@Chimborazo:/media/Summit/zach_vg/minigraph$ ./minigraph/minigraph -xasm --call CPB_Mar18.gfa F_Kansas_60.fasta > F_KS_60.bed

...etc
```

## gfa to vg (vg1.31.0 Caffaraccia
```bash
## convert gfa to vg using vg build:

# first converted minigraph .gfa -> vg using CI docker suggestion: 
## new vg build 1.31.0
./vg convert -g CPB_Mar18.gfa -v >  CPB_Mar18.vg

./vg stats -lz CPB_Mar18.vg 
nodes	842440
edges	1147270
length	1068342500

# prune messed up graph
#./vg prune -r -p -t 32 CPB_Mar18.vg > CPB_Mar18.pruned.vg
Original graph CPB_Mar18.vg: 842440 nodes, 1147270 edges
Built a temporary XG index
Removed all paths
Pruned complex regions: 842440 nodes, 1147270 edges
Removed small subgraphs: 842440 nodes, 1147270 edges
Restored graph: 842440 nodes
Serialized the graph: 842440 nodes, 1147270 edges

# modify for large bubbles (redid):
molecularecology@Chimborazo:/media/Summit/zach_vg/minigraph$ ./vg mod -X 256 CPB_Mar18.vg > 256_CPB_Mar18.vg

#index = xg
./vg index -x 256_CPB_Mar18.xg -g 256_CPB_Mar18.gcsa -t 32 -b ./ -p 256_CPB_Mar18.vg

# index = gcsa #./vg index -g mod_CPB_Mar18.pruned.gcsa mod_CPB_Mar18.pruned.vg -t 32 -b ./ -p

# map 
./vg map -t 24 -d /media/Summit/zach_vg/minigraph/256_CPB_Mar18 -i -f CPBWGS_12_TCCGGAGA-GGCTCTGA_L003_R1_001.fastq.gz_CLEAN.fq -f CPBWGS_12_TCCGGAGA-GGCTCTGA_L003_R2_001.fastq.gz_CLEAN.fq > CPB_12_mar256.gam

#augment media/Summit/zach_vg/minigraph/vg augment /media/Summit/zach_vg/minigraph/mod_CPB_Mar18.pruned.vg CPBWGS_12_TCCGGAGA-GGCTCTGA.gam -A  2aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.gam > 2aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg 

./vg augment -t 24 /media/Summit/zach_vg/minigraph/256_CPB_Mar18.vg CPB_12_mar256.gam -A aug_CPB_12_mar256.gam > aug_CPB_12_mar256.vg

## confirm paths in vg
./vg paths -L -v aug_CPB_12_mar256.vg
(success)

#index
./vg index -t 24 aug_CPB_12_mar256.vg -x aug_CPB_12_mar256.vg.xg -b ./ -p 

#pack 
./vg pack -x aug_CPB_12_mar256.vg.xg -g aug_CPB_12_mar256.gam -o aug_CPB_12_mar256.pack

#call
./vg call aug_CPB_12_mar256.vg.xg -k aug_CPB_12_mar256.pack -a > genotypes_aug_CPB_12_mar256.vcf

```
## call variants on CPB12:
```bash
# map:
 for j in `cat CPBWGS_list.1`; do for R1 in `ls "$j"*R1*`; do for R2 in `ls "$j"*R2*`; do if [[ "$R1" == "$j"*R1* ]] && [[ "$R2" == "$j"*R2* ]]; then /media/Summit/zach_vg/minigraph/vg map -d /media/Summit/zach_vg/minigraph/mod_CPB_Mar18.pruned -t 16 -f "$R1" -f "$R2" > "$j".gam; fi; done; done; done
 
# augment (not for pooled):
/media/Summit/zach_vg/minigraph/vg augment /media/Summit/zach_vg/minigraph/mod_CPB_Mar18.pruned.vg CPBWGS_12_TCCGGAGA-GGCTCTGA.gam -A  2aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.gam > 2aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg

## augment (pooled)
#/media/Summit/zach_vg/minigraph/vg augment /media/Summit/zach_vg/minigraph/mod_CPB_Mar18.pruned.vg CPBWGS_12_TCCGGAGA-GGCTCTGA.gam -m 4 -q 5 -A  aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.gam > aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg

# index:
/media/Summit/zach_vg/minigraph/vg index -t 8 aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg -x aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg.xg -b ./ -p 

# pack (NO QUAL FILTER)
#vg pack -x CPB_MD_1.gam.vg.xg -g filtered_aug_CPB_MD_1.gam.gam -o filtered_CPB_MD_1.pack
/media/Summit/zach_vg/minigraph/vg pack -x aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg.xg -g aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.gam -o aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.pack

# pack (QUAL FILTER 5)
/media/Summit/zach_vg/minigraph/vg pack -x aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg.xg -g aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.gam -o aug_Q5_CPBWGS_12_TCCGGAGA-GGCTCTGA.pack -Q 5

# call (NO QUAL FILTER):
/media/Summit/zach_vg/minigraph/vg call aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg.xg -k aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.pack -a > genotypes_aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vcf

# call (QUAL FILTER 5):
/media/Summit/zach_vg/minigraph/vg call aug_CPBWGS_12_TCCGGAGA-GGCTCTGA.vg.xg -k aug_Q5_CPBWGS_12_TCCGGAGA-GGCTCTGA.pack -a > genotypes_aug_ Q5_CPBWGS_12_TCCGGAGA-GGCTCTGA.vcf
## pull gams from CHTC and independnet runs, augment and generate vgs:

for j in {39..67}; do for z in `ls C*_"$j"_256*gam`; do ./vg augment -t 24 ./vg augment /media/Summit/zach_vg/minigraph/256_CPB_Mar18.vg "$z" -A Aug_"$z" > "$z".vg; done ; done

 ./vg augment /media/Summit/zach_vg/minigraph/256_CPB_Mar18.vg CPBWGS_62_256_Mar18.gam -A Aug_CPBWGS_62_256_Mar18.gam > CPBWGS_62_256_Mar18.gam.vg

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
