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
