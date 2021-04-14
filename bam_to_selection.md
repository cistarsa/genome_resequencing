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

@3:35

./angsd/angsd -P 30 -b plains_pest_bam_noNJ.list -ref F_Kansas_60.fasta -minMAF 0.05 -out Results_test/ALL_Scaffs_pca -doPlink 2 -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 -minMapQ 30 -minQ 20 -minInd 50 -setMinDepthInd 2 -setMinDepth 120 -setMaxDepth 600 -doCounts 1 -GL 1 -doMajorMinor 1 -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1

#doVcf segmentation fault
```

## try to generate from claire merot
```
#source 01_scripts/01_config.sh
PERCENT_IND=0.5 
MAX_DEPTH_FACTOR=3
N_IND=$(wc -l plains_pest_bam_noNJ.list | cut -d " " -f 1)
MIN_IND_FLOAT=$(echo "($N_IND * $PERCENT_IND)"| bc -l)
MIN_IND=${MIN_IND_FLOAT%.*} 
MAX_DEPTH=$(echo "($N_IND * $MAX_DEPTH_FACTOR)" |bc -l)


./angsd/angsd -nThreads 25 -nQueueSize 50 \
-doMaf 1 -dosaf 1 -GL 2 -doGlf 2 -doMajorMinor 1 -doCounts 1 \
-anc F_Kansas_60.fasta -remove_bads 1 -minMapQ 30 -minQ 20 \
-minInd $MIN_IND -minMaf 0.05 -setMaxDepth $MAX_DEPTH \
-b plains_pest_bam_noNJ.list \
-out Results_CM/all_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR"

##
Fri Apr  9 05:51:14 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 778889268
	-> Number of sites retained after filtering: 13203938 
	[ALL done] cpu-time used =  80007.72 sec
	[ALL done] walltime used =  24910.00 sec

gunzip **gunzip all_maf_pctind0.5_maxdepth3.mafs.gz**


Rscript 01_scripts/Rscripts/make_sites_list_maxdepth_simple.R "$INFILE" "$OUTFILE_sites" "$OUTFILE_regions"
..simple.R:
#this R script uses the mafs file provided by the analyses on all individuals, with filter for quality and maf 0.05
#it simply extract the first columns with chr, position of each SNP and Major/minor alleles as determined in step 03
#output is a "sites" files that will allwo restraining subsequent analyses 
#(for instance maf by pop, FSt by pop pairs, etc to a limited number of loci

argv <- commandArgs(T)
INFILE <- argv[1]
OUTFILE_sites <- argv[2]
OUTFILE_regions <- argv[3]

maf<-read.table(INFILE, header=T)
head (maf)
sites<-maf[,1:4]
sites_order <- sites[order(sites$chromo),] 
regions_order<-levels(sites_order$chromo)
write.table(sites_order, OUTFILE_sites, row.names=F, col.names=F, sep="\t", quote=F)
write.table(regions_order, OUTFILE_regions, row.names=F, col.names=F, sep="\t", quote=F)

#molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/Linear_Bams/Results_CM$ INFILE=all_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR".mafs
OUTFILE_sites=sites_all_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR"
OUTFILE_regions=regions_all_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR"

Rscript make_sites_list_maxdepth_simple.R "$INFILE" "$OUTFILE_sites" "$OUTFILE_regions"

../angsd/angsd sites index $OUTFILE_sites
```


## [pca](https://github.com/clairemerot/angsd_pipeline/blob/master/01_scripts/04_pca.sh#L25)
```
INPUT=Results_CM/all_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR".beagle.gz
## install pcangsd with python3:
molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/Linear_Bams/pcangsd2/pcangsd$ pip3 install --user -r requirements.txt 
molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/Linear_Bams/pcangsd2/pcangsd$ python3 setup.py build_ext --inplace

python3 pcangsd.py -threads 20 -beagle ../../Results_CM/all_maf_pctind0.5_maxdepth3.beagle.gz -o ../../Results_CM/all_maf_pctind0.5_maxdepth3.cov

...Saved covariance matrix as ../../Results_CM/all_maf_pctind0.5_maxdepth3.cov.cov (Text).

echo "transform covariance matrix into PCA"
COV_MAT=04_pca/all_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR".cov
Rscript 01_scripts/Rscripts/make_pca_simple.r "$COV_MAT" "$BAM_LIST"

## ran in R:
R
cov_mat<-as.matrix(read.table(/media/Summit/88_fastq/cleaned/Linear_Bams/Results_CM/all_maf_pctind0.5_maxdepth3.cov.cov), header=F)
cov_mat<-as.matrix(read.table("/media/Summit/88_fastq/cleaned/Linear_Bams/Results_CM/all_maf_pctind0.5_maxdepth3.cov.cov"), header=F)
head(cov_mat)
pca<-eigen(cov_mat)
pca.mat<-as.matrix(pca$vectors %*% (diag(pca$values))^0.5)
nPC<-dim(pca$vectors)[2]
col_PC<-vector(length=nPC)
for (i in 1 : nPC) {col_PC[i]<-paste0("PC",i)}
colnames(pca.mat)<-c(col_PC)
bam_names<-read.table("/media/Summit/88_fastq/cleaned/Linear_Bams/plains_pest_bam_noNJ.list",header=F)
head(bam_names)
rownames(pca.mat)<-bam_names$V1
var1<-round(pca$values[1]*100/sum(pca$values[pca$values>=0]),2)
var2<-round(pca$values[2]*100/sum(pca$values[pca$values>=0]),2)
var3<-round(pca$values[3]*100/sum(pca$values[pca$values>=0]),2)
var4<-round(pca$values[4]*100/sum(pca$values[pca$values>=0]),2)
kmeans_res<-kmeans(as.matrix(pca.mat[,1]), c(min(pca.mat[,1]), median(pca.mat[,1]), max(pca.mat[,1])))
k_ss<-round(kmeans_res$betweenss/kmeans_res$totss,3)
write.table(pca.mat[,1:4], paste0(INPUT,".pca"), quote=F)
write.table(pca.mat[,1:4], paste0(/media/Summit/88_fastq/cleaned/Linear_Bams/Results_CM/all_maf_pctind0.5_maxdepth3.cov.cov,".pca"), quote=F)
write.table(pca.mat[,1:4], paste0(all_maf_pctind0.5_maxdepth3.cov.cov,".pca"), quote=F)
write.table(pca.mat[,1:4], paste0(cov_mat,".pca"), quote=F)
write.table(c(var1,var2,var3,var4,k_ss), paste0(cov_mat,".eig"), quote=F)
jpeg(file=paste0(cov_mat,".pca.jpg"))
par(mfrow=c(1,1))
plot(pca.mat[,1], pca.mat[,2], pch=20, ylab=paste("PC2", var2), xlab=paste("PC1", var1),col=kmeans_res$cluster, main=paste("k_SS",k_ss))
dev.off()


## selection PCAngsd:
python $PCANGSD -beagle $IN_DIR/Demo2input.gz -o $OUT_DIR/Demo2PCANGSD_2 -selection -sites_save #-n $N 

molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/Linear_Bams/pcangsd2/pcangsd$ python3 pcangsd.py -threads 20 -beagle  ../../Results_CM/all_maf_pctind0.5_maxdepth3.beagle.gz -o ../../Results_CM/Selection_all_maf_0.5pc_3md -selection -sites_save #-n $N

```
#OK, 13m SNPS, try with higher stringency:

```

##./angsd/angsd -P 30 -b plains_pest_bam_noNJ.list -ref F_Kansas_60.fasta \
#-minMAF 0.1 -out Results_test/ALL_Scaffs_pca \
#-uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 \
#-minMapQ 30 -minQ 20 -minInd 50 -setMinDepthInd 2 -setMinDepth 120 -setMaxDepth 600 \
#-doCounts 1 -GL 1 -doMajorMinor 1 -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1

./angsd/angsd -nThreads 28 -nQueueSize 50 -doMaf 1 -dosaf 1 -GL 2 -doGlf 2 -doMajorMinor 1 -doCounts 1 -anc F_Kansas_60.fasta2 -remove_bads 1 -minMapQ 30 -minQ 20 -minInd $MIN_IND -minMaf 0.05 -setMinDepthInd 3 -setMaxDepth $MAX_DEPTH -skipTriallelic 1 -SNP_pval 1e-3 -b plains_pest_bam_noNJ.list -out Results_CM/all2_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR"
##-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 778889268
	-> Number of sites retained after filtering: 0 
	[ALL done] cpu-time used =  58960.95 sec
	[ALL done] walltime used =  26045.00 sec

## too high, no sites, use older Plink output:

./angsd/angsd -P 30 -b plains_pest_bam_noNJ.list -ref F_Kansas_60.fasta -minMAF 0.05 -out Results_test/ALL_Scaffs_pca -doPlink 2 -uniqueOnly 1 -remove_bads 1 -only_proper_pairs 1 -trim 0 -C 50 -baq 1 -minMapQ 30 -minQ 20 -minInd 50 -setMinDepthInd 2 -setMinDepth 120 -setMaxDepth 600 -doCounts 1 -GL 1 -doMajorMinor 1 -doMaf 1 -skipTriallelic 1 -SNP_pval 1e-3 -doGeno 32 -doPost 1


-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 776643496
	-> Number of sites retained after filtering: 5186125 
	[ALL done] cpu-time used =  153811.61 sec
	[ALL done] walltime used =  97363.00 sec
```

## rerun beagle file on 13mil:
```
python3 ../pcangsd2/pcangsd/pcangsd.py -beagle all_maf_pctind0.5_maxdepth3.beagle.gz -o ./all_maf_pcadapt -selection -pcadapt -sites_save -threads 20
```

## rerun with higher thresholds (again)
```
./angsd/angsd -nThreads 28 -nQueueSize 50 -doMaf 1 -dosaf 1 -GL 2 -doGlf 2 -doMajorMinor 1 -doCounts 1 -anc F_Kansas_60.fasta2 -remove_bads 1 -minMapQ 30 -minQ 20 -minInd $MIN_IND -minMaf 0.05 -setMinDepthInd 2 -setMaxDepth $MAX_DEPTH -skipTriallelic 1 -SNP_pval 1e-3 -b plains_pest_bam_noNJ.list -out Results_CM/all2_maf"$MIN_MAF"_pctind"$PERCENT_IND"_maxdepth"$MAX_DEPTH_FACTOR"
```

## lets use 90% at 1mil snps

## run pcadapt (from plink output) in R (macbook)

## isolate sig snps:
```bash
 for root in `ls *list2 | sed 's/.list2//g'`; do for list in `ls *list`; do for list2 in `ls *list2`; do if [[ "$list" == "$root"*list ]] && [[ "$list2" == "$root"*list2 ]] ; then for start in `awk '{print $2}' "$list"`; do for stop in `awk '{print $3}' "$list"`; do for snp in `awk '{print $2}' "$list2"`; do if (( "$start" >= "$snp" && "$snp" <= "$stop" )); then echo "$start" "$snp" "$stop"; fi; done; done; done; fi; done; done; done
 ```
 
 ## save and run as seq 0 20 | parallel bash ./curate_overlaps.sh {}
 in molecularecology@Chimborazo:/media/Summit/plink/Scaffolds_SNPs$ 


## determine SNPs in SVs in Genes:

```bash

bedtools intersect -a SNPS_bf_sig_5k_2.list -b CPB_SV_star_stop.list -wb | awk '{print $1"\t"$2"\t"$3}' | head
# wrote output to SNPS_within_SVS_positions.list


bedtools intersect -a SNPS_within_SVS_positions.list -b Linear_KS_genes_strtstop.list -wb  | awk '{print $4";"$5";"$6}' >> SNPS_within_SVS_within_Genes.list
## 293 genes, 193 unique genes 

## grep this against paf 

for j in `cat sort_uSNPS_within_SVS_within_Genes.list` ; do grep "$j" FKS_linear_genes_Semicolon.list; done | sort -u | sed 's/;/ /g' >> Sig_SNPS_SVS_Genelist.final
```
