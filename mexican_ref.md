## Generate mexican reference genome from 88 read database: indvd #24, CPBWGS_24	L. decemlineata	America	Mexico	Saltillo	Saltillo	25.45	-100.99	1534			Victor Izzo/Yolanda				SDS15-355	6-7X	8/28/15	Upper abdomen			25.6	400	102.4

### chtc to map bams:
```bash
#!/bin/bash

## use bwa-mem2 precompiled binaries

##PART I (ran first, output moved to /staging/zcohen3/mex_ref.tgz):

curl -L https://github.com/bwa-mem2/bwa-mem2/releases/download/v2.0pre2/bwa-mem2-2.0pre2_x64-linux.tar.bz2 \
  | tar jxf -

./bwa-mem2-2.0pre2_x64-linux/bwa-mem2 index M_MD_contigs2.fasta 


tar -xzf Mexi*tgz
tar -xzf build_bcf.tgz
tar -xzf tabix-0.2.6_bld.tgz
#tar -xzf atlas_2.tgz

ls -lhS

for f in `ls Mexi*tgz | sed 's/.tgz//g'`; do for z in "$f"/*R1*; do for j in "$f"/*R2*; do if [[ "$z" ==  *"$f"* ]] && [[ "$j" == *"$f"* ]]; \
then for header in `zcat $z | head -n 1`; do for id in `echo $header | head -n 1 | cut -f 1-4 -d":" | sed 's/@//' | sed 's/:/_/g'`; \
do for sm in `echo $header | head -n 1 | grep -Eo "[ATGCN]+$"`; do bwa-mem2-2.0pre2_x64-linux/bwa-mem2 mem -R "@RG\tID:$f\tSM:$id"_"$sm\tLB:$id"_"$sm\tPL:ILLUMINA" M_MD_contigs2.fasta "$z" "$j" >  24_"$f".sam; \
done; done; done;fi; done; done ; done

./samtools view -S -b *sam > 24_"$f".bam

./samtools sort *bam -o 24_sorted_"$f".bam

./samtools index 24_sorted_"$f".bam
mkdir mex_ref
mv M* mex_ref/
mv 24_*bam mex_ref/
#cp sorted* atlas_run_"$f"/

tar -czf mex_ref.tgz mex_ref/

mv mex_ref.tgz /staging/zcohen3/

## part II (ran interactively)
tar -xzf mex_ref.tgz
tar -xzf build_bcf.tgz
tar -xzf tabix-0.2.6_bld.tgz

./samtools faidx M_MD_contigs2.fasta

./build/bin/bcftools mpileup -Ou -f M_MD_contigs2.fasta mex_ref/24_sorted_Mexi.bam | ./build/bin/bcftools call -Ou -mv | ./build/bin/bcftools norm -f M_MD_contigs2.fasta -Oz -o output.vcf.gz
#./build/bin/bcftools mpileup -Ou -f M_MD_contigs2.fasta mex_ref/24_sorted_Mexi.bam ò ./build/bin/bcftools call -Ou -mv ò ./build/bin/bcftools norm -f M_MD_contigs2.fasta -Oz -o output.vcf.gz
#compressed? yes
#./tabix-0.2.6/bgzip -c output.vcf > output.vcf.gz

#index
./tabix-0.2.6/tabix output.vcf.gz

#consensus fasta
./build/bin/bcftools consensus -f M_MD_contigs2.fasta output.vcf.gz > Mexi_24.fasta
scp Mexi_24.fasta /staging/zcohen3/

```
