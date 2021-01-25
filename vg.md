#### generate variant graph using PGGB (pangenome)roughly as edyeet --> seqwish --> smoothxg (>260G used)

```
cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg convert -g smoothed/aln5_smoothed.gfa -v > aln5_smooothed_gfa.vg

# chunk:
cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg chunk -x aln5_smooothed_gfa.vg -C -p "$j" > subgraph_aln5/"$j".vg; done

# mod each chunk:
cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg mod -X 256 subgraph_aln5/"$j".vg > subgraph_aln5/mod_"$j"_gfa.vg; done
## node id space?

#vg ids -j $(for i in $(seq 1 22; echo X; echo Y); do echo chr${i}.vg; done)
# echo ./vg/variant_graph_refs/vg ids -j $(for i in `cat F_Kansas_scaffs.list`; do echo subgraph_aln5/mod_"$j"_gfa.vg; done)

##xg index for each .vg chromosome:
#vg index -x all.xg $(for i in $(seq 1 22; echo X; echo Y); do echo chr${i}.vg; done)

cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg index -p -t 16 -b ./ -x subgraph_aln5/"$j"_aln5c.xg subgraph_aln5/mod_"$j"_gfa.vg; done

## prune:
#for i in $(seq 1 22; echo X; echo Y); do
#  vg prune chr${i}.vg > chr${i}.pruned.vg
#done

cohen@denali:/data2/zach_data$ for i in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg prune subgraph_aln5/mod_"$i"_gfa.vg > subgraph_aln5/pruned_mod_"$i"_gfa.vg; done


##gcsa index:

cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg index -t 16 -p -b ./ -k 11 -X 3 -g subgraph_aln5/"$j"_aln5c.gcsa subgraph_aln5/pruned_mod_"$j"_gfa.vg; done


-x _alln5c.xg subgraph_aln5/mod_"$j"_gfa.vg -p -t 16; done
out:
Building XG index
Saving XG index to aln5_smooothed_gfa.xg
Memory usage: 8.24732 GB
```

#### pre gcsa index pruning and mod:

```
##Found kmer with offset >= 1024. GCSA2 cannot handle nodes greater than 1024 bases long. To enable indexing, modify your graph using `vg mod -X 256 x.vg >y.vg`. AAAAAAACACAAGGAA	1898918:1024	A	A	1898918:1040

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg mod -X 256 pruned_aln5_smooothed_gfa.vg > mod_pruned_aln5_smooothed_gfa.vg 

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg index -t 16 -p -b ./ -k 11 -X 3 -g aln5_smooothed_gfa.gcsa mod_pruned_aln5_smooothed_gfa.vg
```

## chunk graph by scaffold:
```
cohen@denali:/data2/zach_data$ for i in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg prune subgraph_aln5/mod_"$i"_gfa.vg > subgraph_aln5/pruned_mod_"$i"_gfa.vg; done

```
## map reads to vg:

#cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg map -d all -i -f #/data2/CPBWGS/WORKING_DIR/Fastq_files/Decemlineata/CPBWGS_13_TCCGGAGA-AGGCGAAG_L003_R1_001.fastq.gz -f #/data2/CPBWGS/WORKING_DIR/Fastq_files/Decemlineata/CPBWGS_13_TCCGGAGA-AGGCGAAG_L003_R2_001.fastq.gz -t 16 > all5_13.gam

```
for base in `cat list.1`; do for gcsa in `ls subgraph_aln5/"$base"*gcsa`; do for xg in `ls subgraph_aln5/"$base"*xg`; do for file in `ls subgraph_aln5/pruned*"$base"*vg`; do for R1 in `ls 88_fastq/*13*R1*`; do for R2 in `ls 88_fastq/*13*R2*`; do if [[ $file == *"$base"* ]] && [[ $gcsa = *"$base"* ]] && [[ $xg == *"$base"* ]]; then ./vg/variant_graph_refs/vg map -x $xg -g $gcsa -i -f $R1 $R2 > "$base"_CP13.bam; fi; done; done; done; done; done; done
```
cohen@denali:/data2/zach_data$ mv F_KS_P_RNA_scaffold_10_CP13.bam F_KS_P_RNA_scaffold_10_CP13.gam

## dummy code on one scaffold:
```
for base in `cat list.1`; do for gcsa in `ls subgraph_aln5/"$base"*gcsa`; do for xg in `ls subgraph_aln5/"$base"*xg`; do for file in `ls subgraph_aln5/pruned*"$base"*vg`; do for R1 in `ls 88_fastq/*13*R1*`; do for R2 in `ls 88_fastq/*13*R2*`; do if [[ $file == *"$base"* ]] && [[ $gcsa = *"$base"* ]] && [[ $xg == *"$base"* ]]; then ./vg/variant_graph_refs/vg map -x $xg -g $gcsa -i -f $R1 $R2 > "$base"_CP13.gam; fi; done; done; done; done; done; done
```
## gam to bam to SV's?

# sv's in vcf?
```
vg augment x.vg aln.gam -A aug.gam > aug.vg

for base in `cat list.1`; do for file in `ls subgraph_aln5/pruned*"$base"*vg`; do ./vg/variant_graph_refs/vg augment "$file" -A "$base"_CP13.gam > "$base".vg; done

./vg/variant_graph_refs/vg augment subgraph_aln5/mod_F_KS_P_RNA_scaffold_10_gfa.vg F_KS_P_RNA_scaffold_10_CP13.gam > augmented_mod_F_KS_P_RNA_scaffold_10_gfa.vg
```
## pack variants only in graph:	
```
vg pack -x x.xg -g aln.gam -Q 5 -o aln.pack

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg pack -x subgraph_aln5/mod_F_KS_P_RNA_scaffold_10_gfa.vg -g F_KS_P_RNA_scaffold_10_CP13.gam -Q 5 -o aln5c_graph.pack 
```
##vg call
```
vg call x.xg -k aln.pack > graph_calls.vcf
./vg/variant_graph_refs/vg call subgraph_aln5/mod_F_KS_P_RNA_scaffold_10_gfa.vg -k aln5c_graph.pack > graph_aln5_calls.vcf
```
## server crashed. run on chtc:
gcsa construction per scaffold
```bash vg_map_13.sh
#!/bin/bash

tar -xzf subgraphs_aln5.tgz 


#tar -xzf variant_graph_refs.tgz  
#mv CPBWGS_13_TCCGGAGA-AGGCGAAG_L003_R* variant_graph_refs
#cd variant_graph_refs

for dir in `ls -d s*`; do echo $dir; done
cd $dir

for j in `cat x*`; do for z in `ls *vg`; do if [[ "$z" == "$j" ]]; then ../vg index -p -t 4 -b ./ -k 11 -X 3 -g "$j".gcsa $z; fi; done; done

#mv *gcsa ../
cd ..

#mv *gam 13_out
#mkdir "$dir"_out
#cp *gcsa "$dir"_out
tar -czf "$dir"_out.tgz "$dir"
mv "$dir"_out.tgz /staging/zcohen3/gcsa_out/
exit
```
```bash vg_map_13.sub

universe = vanilla
log = vg_index_$(sxg).log
error = vg_index_$(sxg).err

executable = vg_map_13.sh
#output = yiming_canu_ecoli/yiming_ecoli_assembly.out

## Specify that HTCondor should transfer files to and from the
##  computer where each job runs. The last of these lines *would* be
##  used if there were any other files needed for the executable to run.
#should_transfer_files = YES
#when_to_transfer_output = ON_EXIT
transfer_input_files = /staging/zcohen3/F_kansas_scaff.list, /staging/zcohen3/gcsa_directs/$(sxg), /home/zcohen3/VariantGraph/vg
#samtools-1.11.tar.bz2
#P_RNA_pmpf_2.fasta, GCF_000500325.1_Ldec_2.0_cds_from_genomic.fna
#module load GCC/4.9.4
## IMPORTANT! Require execute servers that have Gluster and CentOS 7
requirements = (OpSysMajorVer =?= 7)

#+IsBuildJob =true
## Tell HTCondor what amount of compute resources
##  each job will need on the computer where it runs.
request_cpus = 2
request_memory = 20 GB
request_disk = 50 GB

# Tell HTCondor to run 1 instance of this job:
queue sxg from 189_ss.list
```

### map reads to vg ./vg/variant_graph_refs/vg map -x $xg -g $gcsa -i -f $R1 $R2 ```
#for base in `cat list.1`; do for gcsa in `ls subgraph_aln5/"$base"*gcsa`; do for xg in `ls subgraph_aln5/"$base"*xg`; do for file in `ls subgraph_aln5/pruned*"$base"*vg`; do for R1 in `ls 88_fastq/*13*R1*`; do for R2 in `ls 88_fastq/*13*R2*`; do if [[ $file == *"$base"* ]] && [[ $gcsa = *"$base"* ]] && [[ $xg == *"$base"* ]]; then ./vg/variant_graph_refs/vg map -x $xg -g $gcsa -i -f $R1 $R2 > "$base"_CP13.gam; fi; done; done; done; done; done; done

for reads in `ls -d *_*`; do echo $reads; done 

for vg in `cat s*/x* | sed 's/pruned_//g; s/.vg//g'`; do for gcsa in `ls s*/*"$vg"*gcsa`; do for xg in `ls s*/*"$vg"*xg`; do for R1 in `ls 11_20/*13*R1*`; do for R2 in `ls 11_20/*13*R2*`; do if [[ $gcsa = *"$vg"* ]] && [[ $xg == *"$vg"* ]]; then ./vg map -x $xg -g $gcsa -i -f $R1 $R2 > "$vg"_CP13.gam; fi; done; done; done; done; done```

### map reads again (final loop), augment and call variants: Mon Jan 25:
```## 
## for rest:
for dir in `ls sx*tgz`; do for reads in `ls *_*tgz | sed 's/.tgz//g'`; do for numbers in `ls $reads/*gz | sed 's/\//_/g; s/_/ /g' | awk '{print $3}' | sort -u`; do for vg in `cat s*/x* | sed 's/pruned_//g; s/.vg//g'`; do for gcsa in `ls s*/*"$vg"*gcsa`; do for xg in `ls s*/*"$vg"*xg`; do for R1 in `ls "$reads"/*"$numbers"*R1*`; do for R2 in `ls "$reads"/*"$numbers"*R2*`; do for R1_b in `echo "$R1" | sed 's/_L.*.//g'`; do for R2_b in `echo "$R2" | sed 's/_L.*.//g'`; do if [[ "$R1_b" == "$R2_b" ]] && [[ $gcsa = *"$vg"* ]] && [[ $xg == *"$vg"* ]]; then ./vg map -t 16 -s $xg -g $gcsa -i -f "$R1" -f "$R2" > "$vg"_CP"$numbers"_2.gam; fi; done; done; done; done; done; done; done; done; done; done

## for combo:
for dir in `ls sx*tgz`; do for reads in `ls c*tgz | sed 's/.tgz//g'`; do for numbers in `ls $reads/*gz | sed 's/\//_/g; s/_/ /g' | awk '{print $3}' | sort -u`; do for vg in `cat s*/x* | sed 's/pruned_//g; s/.vg//g'`; do for gcsa in `ls s*/*"$vg"*gcsa`; do for xg in `ls s*/*"$vg"*xg`; do for R1 in `ls "$reads"/*"$numbers"*R1*`; do for R2 in `ls "$reads"/*"$numbers"*R2*`; do for R1_b in `echo "$R1" | sed 's/_L.*.//g'`; do for R2_b in `echo "$R2" | sed 's/_L.*.//g'`; do if [[ "$R1_b" == "$R2_b" ]] && [[ $gcsa = *"$vg"* ]] && [[ $xg == *"$vg"* ]]; then ./vg map -t 16 -s $xg -g $gcsa -i -f "$R1" -f "$R2" > "$vg"_CP"$numbers"_2.gam; fi; done; done; done; done; done; done; done; done; done; done

## then augment, index:

##augment:

for dir in `ls sx*tgz`; do for reads in `ls *_*tgz | sed 's/.tgz//g'`; do for numbers in `ls $reads/*gz | sed 's/\//_/g; s/_/ /g' | awk '{print $4}' | sort -u`; do for vg in `ls s*/*vg`; do for gam in mod*gam; do if [[ "$gam" == *"$numbers"* ]]; then ./vg augment -s "$vg" "$gam" -A aug_"$gam" > aug_"$gam".vg; fi; done; done; done; done; done

## index

for vg2 in `ls aug_"$gam".vg`; do ./vg index -x "$vg2".xg
