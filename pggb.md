## create pangenome using pggb
pull image from: docker pull jmonlong/pggb:970d2e5
docker run -it -v ${PWD}:/tmp jmonlong/pggb:970d2e5 /bin/bash

# cat 

root@8e8dbbdcd4ed:/# pggb -i /tmp/Ldec5.fasta -w 50000 -s 10000 -p 70 -a 70 -n 5 -t 16 -v -l       

## run docker image
cohen@denali:/data2/zach_data$ docker run -it -v ${PWD}:/tmp jmonlong/pggb:970d2e5 /bin/bash

root@524fdab85d5c:/# edyeet /tmp/F_Kansas_60.fasta /tmp/F_Oregon_60.fasta /tmp/M_MD_60.fasta /tmp/Mexi_60.fasta /tmp/Ldec_2018LI_60.fasta -p 90 -a 90 -N -t 16 > aln5.paf 

root@524fdab85d5c:/# cat /tmp/F_Kansas_60.fasta /tmp/F_Oregon_60.fasta /tmp/M_MD_60.fasta /tmp/Mexi_60.fasta /tmp/Ldec_2018LI_60.fasta > L_5_5.fasta
 
 
root@524fdab85d5c:/#  seqwish -t 16 -s aln5.paf -s L_5_5.fasta -g aln5.gfa -P 

root@524fdab85d5c:/# smoothxg -g aln5.gfa -V -o smoothed_aln5L5.gfa -m msa_alnL5.msa -t 16 
[smoothxg::main] loading graph
[smoothxg::main] prepping graph for smoothing
[smoothxg::prep] building path index
[smoothxg::prep] sorting graph
[odgi::path_linear_sgd] calculating linear SGD schedule (1.47449e-10 1 30 0 0.01)
[odgi::path_linear_sgd] calculating zetas for 1091 zipf distributions
[odgi::path_linear_sgd] 1D path-guided SGD: 100.00% @ 7.26e+06/s elapsed: 00:00:00:05 remain: 00:00:00:00
[odgi::groom] grooming: 100.00% @ 1.85e+05/s elapsed: 00:00:00:04 remain: 00:00:00:00
[odgi::groom] adding edges: 100.00% @ 9.58e+05/s elapsed: 00:00:00:01 remain: 00:00:00:00
[odgi::groom] adding paths: 100.00% @ 3.30e+04/s elapsed: 00:00:00:01 remain: 00:00:00:00
[odgi::topological_order] sorting nodes: 100.00% @ 9.27e+04/s elapsed: 00:00:00:08 remain: 00:00:00:00
[smoothxg::prep] chopping graph to 100
[odgi::chop] 70073 node(s) to chop.
[smoothxg::prep] writing graph aln5.gfa.prep.gfa
[smoothxg::main] building xg index
[smoothxg::smoothable_blocks] computing blocks
[smoothxg::smoothable_blocks] computing blocks for 40672325 handles: 100.00% @ 5.10e+05/s elapsed: 00:00:01:19 remain: 00:00:00:00
[smoothxg::break_blocks] splitting short sequences out of 398823 blocks: 100.00% @ 3.98e+05/s elapsed: 00:00:00:01 remain: 00:00:00:00
[smoothxg::break_blocks] split 4603 blocks
[smoothxg::break_blocks] cutting blocks that contain sequences longer than max-poa-length (10000)
[smoothxg::break_blocks] cutting 403426 blocks: 100.00% @ 8.84e+03/s elapsed: 00:00:00:45 remain: 00:00:00:00
[smoothxg::break_blocks] cut 370290 blocks of which 2262 had repeats
Illegal instruction (core dumped)

let's try dockerfile for smoothxg on chtc:
#built locally using docker instance from pggg:
```
Zachary-Cohens-MacBook-2:pggb zacharycohen$ docker build -t kingcohn1/pggb .
Sending build context to Docker daemon   5.12kB
Step 1/1 : FROM ghcr.io/pangenome/pggb:202012122000576ef861
 ---> 93d5d5d740d1
Successfully built 93d5d5d740d1
Successfully tagged kingcohn1/pggb:latest
Zachary-Cohens-MacBook-2:pggb zacharycohen$ sudo docker push kingcohn1/pggb:latest 

root@524fdab85d5c:/# smoothxg -g aln5.gfa -V -o smoothed_aln5L5.gfa -m msa_alnL5.msa -t 16
```
```
#index:
cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg index -x all.xg -t 16 -p ./test/*vg

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg index -b tmp_gcsa/ -g all.gcsa -p -t 16 ./test/*prnd_test.vg



```#map, took around 5-6hrs 16CPUs:

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg map -d all -i -f /data2/CPBWGS/WORKING_DIR/Fastq_files/Decemlineata/CPBWGS_13_TCCGGAGA-AGGCGAAG_L003_R1_001.fastq.gz -f /data2/CPBWGS/WORKING_DIR/Fastq_files/Decemlineata/CPBWGS_13_TCCGGAGA-AGGCGAAG_L003_R2_001.fastq.gz -t 16 > all5_13.gam
```
```
#call only variants in graph (among 5)
#vg pack -x x.xg -g aln.gam -Q 5 -o aln.pack
cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg pack -x all.xg -g all5_13.gam -Q 5 -o all5_13.pack
#vg call x.xg -k aln.pack > graph_calls.vcf
cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg call all.xg -k all5_13.pack > graph_calls.vcf

```
```
#augment graph back:
## turn gam to bam:

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg augment aln5.vg all5_13.gam -A all5_aug.gam > all_aln5_aug.vg

```

## Using INDELSEEK:

### first, sort bam:
(use old samtools) 
samtools sort aln5_13.bam -o sorted_aln5_13 > sorted_aln5_13.bam
### then, index bam:
samtools index sorted_aln5_13.bam 

```cohen@denali:/data2/zach_data$ samtools view sorted_aln5_13.bam F_KS_tig00027578_RagTag_RagTag | ./indelseek.pl --refseq F_Kansas_60.fasta --skip_lowqual | tee cp13.complexindel.vcf
```
