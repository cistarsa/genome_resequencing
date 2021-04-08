## follow tutorial from [here](https://github.com/mfumagalli/ngsTools/blob/master/TUTORIAL.md)  

print distribution per site and per sample:
```
$ANGSD/angsd -P 4 -b ALL.bamlist -ref $REF -out Results/ALL.qc -r 11\
        -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 \
	-minMapQ 20 \
        -doQsDist 1 -doDepth 1 -doCounts 1 -maxDepth 500 &> /dev/null
        
 ## run molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/Linear_Bams$
 
./angsd/angsd -P 20 -b final_bam.list -ref F_Kansas_60.fasta -out \
Results_test/ALL_FKS_scaff9.qc -r F_KS_P_RNA_scaffold_9 -uniqueOnly 1 \
-remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 -minMapQ 20 \
-doQsDist 1 -doDepth 1 -doCounts 1 -maxDepth 500

```
```output

	[ALL done] cpu-time used =  12244.16 sec
	[ALL done] walltime used =  9006.00 sec
  ````
  
  PCA 1 from tutorial:
  ``filter for mInd=44, 
  
  ANGSD/angsd -P 20 -b ALL.bamlist -ref $REF -out Results/ALL -r 11 \
        -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 \
        -minMapQ 20 -minQ 20 -minInd 15 -setMinDepth 60 -setMaxDepth 400 -doCounts 1 \
        -GL 1 -doMajorMinor 1 -doMaf 1 -skipTriallelic 1 \
        -SNP_pval 1e-3 \
	-doGeno 32 -doPost 1 &> /dev/null
  
  ## run:
  ./angsd/angsd -P 20 -b final_bam.list -ref F_Kansas_60.fasta -out Results_test/ALL_Scaff9_pca1 \
  -r F_KS_P_RNA_scaffold_9 -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 \
  -minMapQ 30 -minQ 20 -minInd 44 -setMinDepth 60 -setMaxDepth 400 -doCounts 1 -GL 1 -doMajorMinor 1 \
  -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1
  ```
  ##stdout
  
  Wed Apr  7 19:13:42 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 56269033
	-> Number of sites retained after filtering: 3496662 
	[ALL done] cpu-time used =  17884.00 sec
	[ALL done] walltime used =  8860.00 sec
  
  
  #NSITES
  NSITES=`zcat Results_test/ALL_Scaff9_pca1.mafs.gz | tail -n+2 | wc -l`
  echo $NSITES
  3496662

   ## pca
   #$NGSTOOLS/ngsPopGen/ngsCovar -probfile Results/ALL.geno -outfile Results/ALL.covar -nind 30 -nsites $NSITES -call 0 -norm 0 &> /dev/null
open geno
molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/Linear_Bams$ gunzip Results_test/ALL_Scaff9_pca1.geno.gz 

## generate numbers for PCA eigenvalues:

Rscript -e 'write.table(cbind(seq(1,88),rep(1,88),c(rep("AZ",1),rep("MA",1),rep("VA",1),rep("PLAINS",4),rep("MEX",9),rep("TN",1),rep("PLAINS",1),rep("MEX",1),rep("OH",1),rep("KT",1),rep("NC",1),rep("FL",1),rep("PLAINS",3),rep("EURO",2),rep("WI",10),rep("MI",10),rep("OR",10),rep("MD",10),rep("NJ",5),rep("NY",5),rep("VT",5),rep("MN",5))), row.names=F, sep="\t", col.names=c("FID","IID","CLUSTER"), file="Results_test/ALL_FKS_9.clst", quote=F)'

## run and plot
#Rscript $NGSTOOLS/Scripts/plotPCA.R -i Results/ALL.covar -c 1-2 -a Results/ALL.clst -o Results/ALL.pca.pdf
evince Results/ALL.pca.pdf

Rscript ./Analysis/ngsTools/Scripts/plotPCA.R_2 -i Results_test/ALL_Scaff9_pca1.covar -c 4-5 -a Results_test/ALL_FKS_9.clst -o Results_test/ALL_FKS9_pca4-5.pdf
## not very well resolved in first several PC's try with more stringent thresholds:

./angsd/angsd -P 30 -b final_bam.list -ref F_Kansas_60.fasta -out Results_test/ALL_Scaff9_pca2 \
  -r F_KS_P_RNA_scaffold_9 -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 \
  -minMapQ 30 -minQ 20 -minInd 70 -setMinDepth 70 -setMaxDepth 400 -doCounts 1 -GL 1 -doMajorMinor 1 \
  -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1

```
## try only plains and pest:
```
 ./angsd/angsd -P 30 -b plains_pest_bam.list -ref F_Kansas_60.fasta -out Results_test/ALL_Scaff9_pca2\
 -r F_KS_P_RNA_scaffold_9 -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 -minMapQ 30 \
 -minQ 20 -minInd 50 -setMinDepth 50 -setMaxDepth 400 -doCounts 1 -GL 1 -doMajorMinor 1\
 -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1

~2hrs 
-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 56139005
	-> Number of sites retained after filtering: 2300783 
	[ALL done] cpu-time used =  13334.33 sec
	[ALL done] walltime used =  6953.00 sec

## gunzip output

## generate genofiles:
./Analysis/ngsTools/ngsPopGen/ngsCovar -probfile Results_test/ALL_Scaff9_pca2.geno -outfile Results_test/ALL_Scaff9_pca2.covar -nind 69 -nsites 2300783 -call 0 -norm 0

Rscript -e 'write.table(cbind(seq(1,69),rep(1,69),c(rep("PLAINS",9),rep("WI",10),rep("MI",10),rep("OR",10),rep("MD",10),rep("NJ",5),rep("NY",5),rep("VT",5),rep("MN",5))), row.names=F, sep="\t", col.names=c("FID","IID","CLUSTER"), file="Results_test/ALL_FKS_9_2.clst", quote=F)'

Rscript -e 'write.table(cbind(seq(1,69),rep(1,69),c(rep("PLAINS",9),rep("MIDWEST",20),rep("OR",10),rep("NORTHEAST",30))), row.names=F, sep="\t", col.names=c("FID","IID","CLUSTER"), file="Results_test/ALL_FKS_9_2B.clst", quote=F)'

Rscript -e 'write.table(cbind(seq(1,69),rep(1,69),c(rep("PLAINS",9),rep("MIDWEST",20),rep("OR",10),rep("NORTHEAST",10),rep("NJ",5),rep("NORTHEAST",15))), row.names=F, sep="\t", col.names=c("FID","IID","CLUSTER"), file="Results_test/ALL_FKS_9_2C.clst", quote=F)'

#REPLOT
Rscript ./Analysis/ngsTools/Scripts/plotPCA.R_2 -i Results_test/ALL_Scaff9_pca2.covar -c 1-2 -a Results_test/ALL_FKS_9_2C.clst -o Results_test/ALL_FKS9_pca2C_1-2.pdf
```
# DROP NJ (79-83) plains_pest_bam.list
```
#mindepthind 2

./angsd/angsd -P 30 -b plains_pest_bam_noNJ.list -ref F_Kansas_60.fasta -out Results_test/ALL_Scaff9_pca3  
-r F_KS_P_RNA_scaffold_9 -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 -minMapQ 30 
-minQ 20 -minInd 50 -setMinDepth 50 -setMaxDepth 400 
-doCounts 1 -GL 1 -doMajorMinor 1   -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1


-> Total number of sites analyzed: 56096840
	-> Number of sites retained after filtering: 2031827 
	[ALL done] cpu-time used =  11886.40 sec
	[ALL done] walltime used =  6286.00 sec

#geno files
gunzip Results_test/ALL_Scaff9_pca3.geno.gz
./Analysis/ngsTools/ngsPopGen/ngsCovar -probfile Results_test/ALL_Scaff9_pca3.geno -outfile Results_test/ALL_Scaff9_pca3.covar -nind 64 -nsites 2031827 -call 0 -norm 0

## generate input table
Rscript -e 'write.table(cbind(seq(1,64),rep(1,64),c(rep("PLAINS",6),rep("NORTHWEST",1),rep("PLAINS",2),rep("MIDWEST",20),rep("NORTHWEST",10),rep("NORTHEAST",25))), row.names=F, sep="\t", col.names=c("FID","IID","CLUSTER"), file="Results_test/ALL_FKS_9_2D.clst", quote=F)'

Rscript ./Analysis/ngsTools/Scripts/plotPCA.R_2 -i Results_test/ALL_Scaff9_pca3.covar -c 1-2 -a Results_test/ALL_FKS_9_2D.clst -o Results_test/ALL_FKS9_pca2D_1-2.pdf

```

##redo with scaff_1, higher filters:
```

#mindepthind 2, minMAF 0.1
./angsd/angsd -P 30 -b plains_pest_bam_noNJ.list -ref F_Kansas_60.fasta \
-minMAF 0.1 -out Results_test/ALL_Scaff1_pca2 -r F_KS_P_RNA_scaffold_1 \
-uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 \
-minMapQ 30 -minQ 20 -minInd 50 -setMinDepthInd 2 -setMinDepth 120 -setMaxDepth 600 \
-doCounts 1 -GL 1 -doMajorMinor 1 -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1

[ALL done] cpu-time used =  4893.95 sec
	[ALL done] walltime used =  2955.00 sec
Total number of sites analyzed: 26317871
	-> Number of sites retained after filtering: 450546 
  
  molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/Linear_Bams$ gunzip Results_test/ALL_Scaff1_pca1.geno.gz

#covariance
./Analysis/ngsTools/ngsPopGen/ngsCovar -probfile Results_test/ALL_Scaff1_pca1.geno -outfile Results_test/ALL_Scaff1_pca1.covar -nind 64 -nsites 450546 -call 0 -norm 0

Rscript ./Analysis/ngsTools/Scripts/plotPCA.R_2 -i Results_test/ALL_Scaff1_pca1.covar -c 1-2 -a Results_test/ALL_FKS_9_2D.clst -o Results_test/ALL_FKS1_pca_1-2.pdf

```

## scale up, entire set
minMAF 0.1 @ 3:15
```
./angsd/angsd -P 30 -b plains_pest_bam_noNJ.list -ref F_Kansas_60.fasta \
-minMAF 0.1 -out Results_test/ALL_Scaffs_pca \
-uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 \
-minMapQ 30 -minQ 20 -minInd 50 -setMinDepthInd 2 -setMinDepth 120 -setMaxDepth 600 \
-doCounts 1 -GL 1 -doMajorMinor 1 -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1


./angsd/angsd -P 30 -b plains_pest_bam_noNJ.list -ref F_Kansas_60.fasta -minMAF 0.05 -out Results_test/ALL_Scaffs_pca -doPlink 2 -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 -minMapQ 30 -minQ 20 -minInd 50 -setMinDepthInd 2 -setMinDepth 120 -setMaxDepth 600 -doCounts 1 -GL 1 -doMajorMinor 1 -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1

#doVcf segmentation fault
```
