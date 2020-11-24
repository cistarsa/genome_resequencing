#### generate variatn graph reference genome from Ldec: Long Island, Kansas, Oregon and Marylang using minigraph on CHTC

```bash
./minigraph -xggs -t16 F_Kansas_contigs.fasta M_MD_contigs.fasta F_Oregon_contigs.fasta Ldec_2018_redundas_allpaths.fa > Ldec_Kansas_ref.gfa
# Assemble Nanopore reads:
./gfatools gfa2fa -s Ldec_Kansas_ref.gfa > Ldec_Kansas_ref.stable.fa

ls -lhS
# Compressing output and sending to gluster:
mkdir Ldec_kansasRef
mv Ldec_Kansas_ref.gfa Ldec_kansasRef/
mv Ldec_Kansas_ref.stable.fa Ldec_kansasRef/
tar -czf Ldec_kansasRef.tar.gz Ldec_kansasRef/
cp Ldec_kansasRef.tar.gz /squid/zcohen3/

rm -r .
exit

```

## now create .bams from the 88 using graphAligner(gam) -> vg(bam) -> indelseek(vcf): 

1) graphAligner, build conda environment for it at /home/zcohen3
```python
conda create -n align
conda activate align
conda install -c bioconda graphaligner
conda deactivate
conda pack -n align
```
2) then create bash file
#!/bin/bash
# Assembles Nanopore reads for nebria riversi genome

set -e
ENVNAME=align
ENVDIR=$align
export PATH
mkdir $ENVDIR
tar -xzf $ENVNAME.tar.gz -C $ENVDIR
. $ENVDIR/bin/activate

./align/bin/GraphAligner 

##

sed 's/s//g'
/vg convert -g Ldec_Kansas_ref.gfa



