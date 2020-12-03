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
```bash
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

./bin/GraphAligner -g Ldec_kansasRef/Ldec_Kansas_ref.gfa -f CPBWGS_54_CTGAAGCT-TAATCTTA_L006_R1_001.fastq.gz CPBWGS_54_CTGAAGCT-TAATCTTA_L006_R2_001.fastq.gz -a 54.gam --seeds-minimizer-density 5 --all-alignments -b 1

##

sed 's/s//g'
/vg convert -g Ldec_Kansas_ref.gfa

## error:

perl NovoGraph/scripts/FIND_GLOBAL_ALIGNMENTS.pl --alignmentsFile AlignmentInput.txt.sortedWithHeader --referenceFasta F_Kansas_contigs.fasta --outputFile forMAFFT.sam --outputTruncatedReads truncatedReads --outputReadLenghts postGlobalAlignment_readLengths
Can't locate List/MoreUtils.pm in @INC (@INC contains: /usr/local/lib64/perl5 /usr/local/share/perl5 /usr/lib64/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/lib64/perl5 /usr/share/perl5 .) at NovoGraph/scripts/FIND_GLOBAL_ALIGNMENTS.pl line 11.
BEGIN failed--compilation aborted at NovoGraph/scripts/FIND_GLOBAL_ALIGNMENTS.pl line 11.
```
  
try running with miniconda to resolve error, reinstall conda in job and run?

bash-4.2$ tar -xzf NovoGraph.tgz 
bash-4.2$ bash Miniconda3-latest-Linux-x86_64.sh 
bash-4.2$ miniconda3/bin/conda config --append channels conda-forge
miniconda3/bin/conda install -c bioconda/label/cf201901 perl-list-moreutils

###installing/running on macbook

1) install samtools from tarball, unzip (tar -xf) 

perl NovoGraph/scripts/FIND_GLOBAL_ALIGNMENTS.pl \ 
                              --alignmentsFile AlignmentInput.txt.sortedWithHeader \
                              --referenceFasta F_Kansas_contigs.fasta \
                              --outputFile forMAFFT.sam \
                              --outputTruncatedReads truncatedReads \
                              --samtools_path . \
                              --outputReadLengths postGlobalAlignment_readLengths

perl FIND_GLOBAL_ALIGNMENTS.pl --alignmentsFile ../intermediate_files/AlignmentInput.sortedWithHeader 
                               --referenceFasta GRCh38_full_plus_hs38d1_analysis_set_minus_alts.fa 
                               --outputFile forMAFFT.sam 
                               --outputTruncatedReads ../intermediate_files/truncatedReads 
                               --outputReadLengths ../intermediate_files/postGlobalAlignment_readLengths


## OK lets do cactus to generate MFA, and then vg:

LI, MD, KS, OR

## docker image on CHTC

```bash
#!/bin/bash

#tar -xzf tigs.tgz
mkdir tigs
mv *fa tigs
mv *fasta tigs
cactus ldec_tigs tigs.txt ldecs.hal
ls -lhS

chmod +x hal2vg
./hal2vg ldecs.hal --inMemory --chop 32 --progress > ldecs_hal2vg.pg

vg index ldecs_hal2vg.pg -x ldecs_hal2vg.xg

mkdir ldecs_hals_vg
cp -r jobs ldecs_hals_vg
cp *.hal ldecs_hals_vg
cp *.pg ldecs_hals_vg
cp *.xg ldecs_hals_vg
tar -czf ldecs_hals_vg.tgz ldecs_hals_vg

exit
```
submit:
```bash
universe = docker
log = doc_ldec.log
error = doc_ldec.err
docker_image = quay.io/comparative-genomics-toolkit/cactus:v1.2.3
executable = docker_cactus.sh
output = doc_ldec.out

## Specify that HTCondor should transfer files to and from the
##  computer where each job runs. The last of these lines *would* be
##  used if there were any other files needed for the executable to run.
should_transfer_files = YES


when_to_transfer_output = ON_EXIT

#transfer_input_files = hal2vg, tigs.txt, /staging/zcohen3/zcohen3/tigs.tgz
#transfer_input_files = http://proxy.chtc.wisc.edu/SQUID/chtc/python36.tar.gz,  Miniconda3-latest-Linux-x86_64.sh, AlignmentInput.txt.sortedWithHeader, sam2fasta.py, vg, mafft, /staging/zcohen3/zcohen3/F_Kansas_contigs.fasta, /staging/zcohen3/MmdForFLI_contigs.fa, /staging/zcohen3/allContigs_unsorted.bam, samtools, NovoGraph.tgz
transfer_input_files = vg, tigs.txt, hal2vg, /staging/zcohen3/zcohen3/F_Kansas_contigs.fasta, /staging/zcohen3/zcohen3/F_Oregon_contigs.fasta, /staging/zcohen3/zcohen3/Ldec_2018_redundas_allpaths.fa, /staging/zcohen3/zcohen3/M_MD_contigs.fasta
#
## IMPORTANT! Require execute servers that have Gluster and CentOS 7
requirements = (OpSysMajorVer == 7)

## Tell HTCondor what amount of compute resources
##  each job will need on the computer where it runs.
request_cpus = 4
request_memory = 16GB
request_disk = 8GB

# Tell HTCondor to run 1 instance of this job:
queue
```
## tigs.txt:
(Ldec_2018_redundas_allpaths.fa:1,M_MD_contigs.fasta:1,(F_Oregon_contigs.fasta:1,(F_Kansas_contigs.fasta:1):1):1);

F_Kansas_contigs.fasta tigs/
F_Oregon_contigs.fasta tigs/
Ldec_2018_redundas_allpaths.fa tigs/
M_MD_contigs.fasta tigs/


## soft repeat mask using dfam.h5

