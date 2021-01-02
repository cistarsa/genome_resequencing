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
install rmblast, trf database and dfam on CHTC @/staging/zcohen3/. build repeatmasker
h5py: https://docs.h5py.org/en/latest/build.html
rmblast: http://www.repeatmasker.org/rmblast-2.10.0+-x64-linux.tar.gz
trf: http://tandem.bu.edu/trf/trf409.linux64.download.html
dfam (15.9G): http://www.dfam.org/

#untar python38:
tar -xzf python38.tar.gz
export PATH=$PWD/python/bin:$PATH
#set path to python, install hy5
mkdir rptMsk
#python3 -m pip install --target=$PWD/rptMsk

python3 -m pip install h5py
#/RepeatMasker h5py
export PATH=$PWD/rptMsk/RepeatMasker:$PATH
#mv repeatmasker
cp RepeatMasker-open* rptMsk/
cd rptMsk
gunzip RepeatMask*

#mv prereqs:
#dfam 83G:
gunzip Dfam.h5.gz 
mv Dfam.h5 rptMsk/RepeatMasker/Libraries/
#trf(executable): 
cp trf* rptMsk/
#repeatmodeller:
tar -xzf rmblast-2.10.0+-x64-linux.tar.gz 

export PATH=$PWD/rptMsk:$PATH

mv Dfam.h5 repeatmsk/RepeatMasker/Libraries/

```bash
##trf path
/var/lib/condor/execute/slot1/dir_6792/repeatmsk/trf409.linux64
/var/lib/condor/execute/slot1/dir_6792/repeatmsk/rmblast-2.10.0/bin/
he program is installed with a the following repeat libraries:
Database: Dfam
Version: 3.2
Date: 2020-07-02

Dfam - A database of transposable element (TE) sequence alignments and HMMs.

Total consensus sequences: 273693
Total HMMs: 273655
```

#### finally build repeatmasker, properly:

### update 12/21/20:

## retry again using minigraph on chtc:
```bash
## rename all headers so they're unique: sed -i2 's/>/>F_KS_/g' F_Kansas_contigs_msked.fasta (ex)

./minigraph -xggs -t16 F_Kansas_contigs_mskd.fasta Mexi_24.fasta M_MD_contigs_mskd.fasta F_Oregon_contigs_mskd.fasta Ldec_2018_redundas_allpaths_mskd.fasta > Ldec_KSref_2.gfa

## remove leading s's at nodes, need to be integers:
sed -i1 's/s//g' Ldec_KSref_2.gfa 
sed -i2 's/caff/scaff/g' Ldec_KSref_2.gfa

## generate vg graph:
bash-4.2$ ./vg convert -g -a Ldec_KSref_2.gfa > graph.vg2
## index:
bash-4.2$ 
./vg index -x Ldec_vg.xg -g Ldec_vg.gcsa Ldec_vg.vg
./vg index graph.vg2 -x graph_vg2.xg

/vg index -x Ldec_vg.xg -g Ldec_vg.gcsa Ldec_vg.vg
Found kmer with offset >= 1024. GCSA2 cannot handle nodes greater than 1024 bases long. To enable indexing, modify your graph using `vg mod -X 256 x.vg >y.vg`. CTGAAAAAAATCGTCA	939878:1024939878:1040
bash-4.2$ vg mod -X 256 Ldec_vg.vg > Ldec_vg2.vg
bash: vg: command not found
bash-4.2$ ./vg mod -X 256 Ldec_vg.vg > Ldec_vg2.vg
#pruned 

vg prune graph.vg > graph.pruned.vg
cohen@denali:~/vg/variant_graph_refs$ nohup -c "./vg index -g graph.gcsa graph.pruned.vg -b /data2/tmp/ -p" &
rm -f graph.pruned.vg```

### sibelia to generate MAF, MAF-> MSA, MSA-VG (use vg -construct)

```bash

#missing sibelia code, but download msaconverter

# add forge to channel
#conda config --append channels conda-forge
molecularecology@molecular-ecology:~/Documents/ZachCohen/SibeliaZ/sibeliaz_out$ ./miniconda/bin/conda install msaconverter

```
### variantgraph generate vcfs:
```bash
#on augmented graph with cp13 variants:
# augment map with cp13 variants:
./vg augment Ldec_vg2.vg cp13.gam -A cp13_aug.gam > cp13_aug.vg
# pack for genome gam
./vg pack -x Ldec_vg.xg -g cp13.gam -Q 5 -o aln_13.pack
# vcf for genome graph calls:
./vg call Ldec_vg.xg -k aln_13.pack > graph_calls.vcf
#index augmented vg
./vg index -p cp13_aug.vg -x cp13_aug.xg
# pack augmented gam 
./vg pack -x cp13_aug.xg -g cp13_aug.gam -Q 5 -o aln_aug_13.pack
#vcf
./vg call cp13_aug.xg -k aln_aug_13.pack > calls_13.vcf

```

### 12/31/20 use seqwish on minimap2 (docker image), then try smoothxg (also docker)

```docker
on denali, create dockerfile:
#df:
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
  dialog \
  apt-utils \
  build-essential \
  cmake \
  libssl-dev \
  libffi-dev \
  python3-distutils \
  python3-dev \
  git \
  && rm -rf /var/lib/apt/lists/*

RUN git clone --recursive https://github.com/ekg/smoothxg.git

RUN cd smoothxg && cmake -H. -Bbuild && cmake --build build -- -j 4

ENV PATH="/smoothxg/bin:${PATH}"
cohen@denali:~/smooothxg$ sudo docker build -t kingcohn1/smoothxg .

#push image, not working. run on server:
#docker run -ti -v ${PWD}:/tmp DOCKER_IMAGE /bin/bash

docker run -it -v ${PWD}:/tmp kingcohn1/smoothxg /bin/bash

root@ec1ff8811f00:/tmp# rm nohup.out 
root@ec1ff8811f00:/tmp# nohup smoothxg -g Ldec_all5.gfa -V  -o smoothed_Ldec_all5.gfa -m msa_Ldec_all5.msa
/home/cohen/vg/variant_graph_refs/Ldec_all5.gfa
```
