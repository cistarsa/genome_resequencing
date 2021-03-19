## population genetics of Long Island and Wisconsin pest populations

## clean reads
for pest in `cat Pest_samples.list`; do for R1 in `ls /media/molecularecology/My\ Book/daves_4tb/88_fastq"$pest"*R1*`; 
do for R2 in `ls /media/molecularecology/My\ Book/daves_4tb/88_fastq"$pest"*R2*`; 
do if [[ "$R1" == *"$pest"*R1* ]] && [[ "$R2" == *"$pest"*R2* ]] ; 
then bbmap/bbduk.sh -Xmx23g -t8 in1="$R1" in2="$R2" out1=cleaned/"$pest"_R1_CLEAN.fq out2=cleaned/"$pest"_R2_CLEAN.fq minlen=25 qtrim=rl trimq=10 ktrim=r k=23 
mink= 11 hdist= 1 tpe tbo; fi; done; done; done
