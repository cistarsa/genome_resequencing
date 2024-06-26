## population genetics of Long Island and Wisconsin pest populations

## clean reads
```
for pest in `cat Pest_samples.list`; do for R1 in `ls /media/molecularecology/My\ Book/daves_4tb/88_fastq"$pest"*R1*`; 
do for R2 in `ls /media/molecularecology/My\ Book/daves_4tb/88_fastq"$pest"*R2*`; 
do if [[ "$R1" == *"$pest"*R1* ]] && [[ "$R2" == *"$pest"*R2* ]] ; 
then bbmap/bbduk.sh -Xmx23g -t8 in1="$R1" in2="$R2" out1=cleaned/"$pest"_R1_CLEAN.fq out2=cleaned/"$pest"_R2_CLEAN.fq minlen=25 qtrim=rl trimq=10 ktrim=r k=23 
mink= 11 hdist= 1 tpe tbo; fi; done; done; done
```
java -ea -Xmx23g -Xms23g -cp /media/Summit/CHTC/staging/Modern_Museum/bbmap/current/ jgi.BBDuk -Xmx23g in1=CPB2015-499B_S648_L003_R1_001.fastq.gz in2=CPB2015-499B_S648_L003_R2_001.fastq.gz out1=CPB2015-499B_R1_CLEAN.fq out2=CPB2015-499B_R2_CLEAN.fq minlen=25 qtrim=rl trimq=10 ktrim=r k=23 mink=11 hdist=1 tpe tbo

Input:                  	29617910 reads 		4472304410 bases.
QTrimmed:               	26935 reads (0.09%) 	49926 bases (0.00%)
Trimmed by overlap:     	181610 reads (0.61%) 	8247282 bases (0.18%)
Total Removed:          	56 reads (0.00%) 	8297208 bases (0.19%)
Result:                 	29617854 reads (100.00%) 	4464007202 bases (99.81%)

Time:                         	304.696 seconds.
Reads Processed:      29617k 	97.20k reads/sec
Bases Processed:       4472m 	14.68m bases/sec

i.BBDuk [-Xmx23g, in1=CPB2015-499A_S647_L003_R1_001.fastq.gz, in2=CPB2015-499A_S647_L003_R2_001.fastq.gz, out1=CPB2015-499A_R1_CLEAN.fq, out2=CPB2015-499A_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]
Version 38.90

Input:                  	25093546 reads 		3789125446 bases.
QTrimmed:               	23006 reads (0.09%) 	41422 bases (0.00%)
Trimmed by overlap:     	157416 reads (0.63%) 	7305136 bases (0.19%)
Total Removed:          	38 reads (0.00%) 	7346558 bases (0.19%)
Result:                 	25093508 reads (100.00%) 	3781778888 bases (99.81%)

Time:                         	275.809 seconds.
Reads Processed:      25093k 	90.98k reads/sec
Bases Processed:       3789m 	13.74m bases/sec
Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-490B_S646_L003_R1_001.fastq.gz, in2=CPB2015-490B_S646_L003_R2_001.fastq.gz, out1=CPB2015-490B_R1_CLEAN.fq, out2=CPB2015-490B_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	26512250 reads 		4003349750 bases.
QTrimmed:               	24388 reads (0.09%) 	44790 bases (0.00%)
Trimmed by overlap:     	2411720 reads (9.10%) 	89577628 bases (2.24%)
Total Removed:          	52 reads (0.00%) 	89622418 bases (2.24%)
Result:                 	26512198 reads (100.00%) 	3913727332 bases (97.76%)

Time:                         	295.806 seconds.
Reads Processed:      26512k 	89.63k reads/sec
Bases Processed:       4003m 	13.53m bases/sec

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-490A_S645_L003_R1_001.fastq.gz, in2=CPB2015-490A_S645_L003_R2_001.fastq.gz, out1=CPB2015-490A_R1_CLEAN.fq, out2=CPB2015-490A_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	25459090 reads 		3844322590 bases.
QTrimmed:               	23206 reads (0.09%) 	44791 bases (0.00%)
Trimmed by overlap:     	386518 reads (1.52%) 	11975874 bases (0.31%)
Total Removed:          	64 reads (0.00%) 	12020665 bases (0.31%)
Result:                 	25459026 reads (100.00%) 	3832301925 bases (99.69%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-461_S644_L003_R1_001.fastq.gz, in2=CPB2015-461_S644_L003_R2_001.fastq.gz, out1=CPB2015-461_R1_CLEAN.fq, out2=CPB2015-461_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	23926234 reads 		3612861334 bases.
QTrimmed:               	21684 reads (0.09%) 	40856 bases (0.00%)
Trimmed by overlap:     	105076 reads (0.44%) 	5146376 bases (0.14%)
Total Removed:          	48 reads (0.00%) 	5187232 bases (0.14%)
Result:                 	23926186 reads (100.00%) 	3607674102 bases (99.86%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-419E_S633_L003_R1_001.fastq.gz, in2=CPB2015-419E_S633_L003_R2_001.fastq.gz, out1=CPB2015-419E_R1_CLEAN.fq, out2=CPB2015-419E_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	26538548 reads 		4007320748 bases.
QTrimmed:               	24468 reads (0.09%) 	48260 bases (0.00%)
Trimmed by overlap:     	397134 reads (1.50%) 	13577980 bases (0.34%)
Total Removed:          	68 reads (0.00%) 	13626240 bases (0.34%)
Result:                 	26538480 reads (100.00%) 	3993694508 bases (99.66%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-419D_S632_L003_R1_001.fastq.gz, in2=CPB2015-419D_S632_L003_R2_001.fastq.gz, out1=CPB2015-419D_R1_CLEAN.fq, out2=CPB2015-419D_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	24510348 reads 		3701062548 bases.
QTrimmed:               	22524 reads (0.09%) 	43294 bases (0.00%)
Trimmed by overlap:     	397986 reads (1.62%) 	12818364 bases (0.35%)
Total Removed:          	56 reads (0.00%) 	12861658 bases (0.35%)
Result:                 	24510292 reads (100.00%) 	3688200890 bases (99.65%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-417_S631_L003_R1_001.fastq.gz, in2=CPB2015-417_S631_L003_R2_001.fastq.gz, out1=CPB2015-417_R1_CLEAN.fq, out2=CPB2015-417_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	24656702 reads 		3723162002 bases.
QTrimmed:               	22224 reads (0.09%) 	44260 bases (0.00%)
Trimmed by overlap:     	91024 reads (0.37%) 	3964528 bases (0.11%)
Total Removed:          	70 reads (0.00%) 	4008788 bases (0.11%)
Result:                 	24656632 reads (100.00%) 	3719153214 bases (99.89%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-416F_S630_L003_R1_001.fastq.gz, in2=CPB2015-416F_S630_L003_R2_001.fastq.gz, out1=CPB2015-416F_R1_CLEAN.fq, out2=CPB2015-416F_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	21321220 reads 		3219504220 bases.
QTrimmed:               	19836 reads (0.09%) 	37665 bases (0.00%)
Trimmed by overlap:     	440940 reads (2.07%) 	15455738 bases (0.48%)
Total Removed:          	44 reads (0.00%) 	15493403 bases (0.48%)
Result:                 	21321176 reads (100.00%) 	3204010817 bases (99.52%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-416E_S629_L003_R1_001.fastq.gz, in2=CPB2015-416E_S629_L003_R2_001.fastq.gz, out1=CPB2015-416E_R1_CLEAN.fq, out2=CPB2015-416E_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	27081184 reads 		4089258784 bases.
QTrimmed:               	24893 reads (0.09%) 	44225 bases (0.00%)
Trimmed by overlap:     	331206 reads (1.22%) 	12383842 bases (0.30%)
Total Removed:          	40 reads (0.00%) 	12428067 bases (0.30%)
Result:                 	27081144 reads (100.00%) 	4076830717 bases (99.70%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-378F_S623_L003_R1_001.fastq.gz, in2=CPB2015-378F_S623_L003_R2_001.fastq.gz, out1=CPB2015-378F_R1_CLEAN.fq, out2=CPB2015-378F_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	26834720 reads 		4052042720 bases.
QTrimmed:               	24680 reads (0.09%) 	44641 bases (0.00%)
Trimmed by overlap:     	141596 reads (0.53%) 	6750690 bases (0.17%)
Total Removed:          	46 reads (0.00%) 	6795331 bases (0.17%)
Result:                 	26834674 reads (100.00%) 	4045247389 bases (99.83%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-378E_S622_L003_R1_001.fastq.gz, in2=CPB2015-378E_S622_L003_R2_001.fastq.gz, out1=CPB2015-378E_R1_CLEAN.fq, out2=CPB2015-378E_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	24905124 reads 		3760673724 bases.
QTrimmed:               	22670 reads (0.09%) 	42342 bases (0.00%)
Trimmed by overlap:     	177326 reads (0.71%) 	8079300 bases (0.21%)
Total Removed:          	54 reads (0.00%) 	8121642 bases (0.22%)
Result:                 	24905070 reads (100.00%) 	3752552082 bases (99.78%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-378D_S621_L003_R1_001.fastq.gz, in2=CPB2015-378D_S621_L003_R2_001.fastq.gz, out1=CPB2015-378D_R1_CLEAN.fq, out2=CPB2015-378D_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	22537552 reads 		3403170352 bases.
QTrimmed:               	20945 reads (0.09%) 	39799 bases (0.00%)
Trimmed by overlap:     	360664 reads (1.60%) 	12259238 bases (0.36%)
Total Removed:          	50 reads (0.00%) 	12299037 bases (0.36%)
Result:                 	22537502 reads (100.00%) 	3390871315 bases (99.64%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-378C_S620_L003_R1_001.fastq.gz, in2=CPB2015-378C_S620_L003_R2_001.fastq.gz, out1=CPB2015-378C_R1_CLEAN.fq, out2=CPB2015-378C_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	22767148 reads 		3437839348 bases.
QTrimmed:               	20972 reads (0.09%) 	38962 bases (0.00%)
Trimmed by overlap:     	380812 reads (1.67%) 	12655514 bases (0.37%)
Total Removed:          	48 reads (0.00%) 	12694476 bases (0.37%)
Result:                 	22767100 reads (100.00%) 	3425144872 bases (99.63%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-348F_S619_L003_R1_001.fastq.gz, in2=CPB2015-348F_S619_L003_R2_001.fastq.gz, out1=CPB2015-348F_R1_CLEAN.fq, out2=CPB2015-348F_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	23198612 reads 		3502990412 bases.
QTrimmed:               	21267 reads (0.09%) 	39540 bases (0.00%)
Trimmed by overlap:     	181432 reads (0.78%) 	8315654 bases (0.24%)
Total Removed:          	48 reads (0.00%) 	8355194 bases (0.24%)
Result:                 	23198564 reads (100.00%) 	3494635218 bases (99.76%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-504C_S651_L003_R1_001.fastq.gz, in2=CPB2015-504C_S651_L003_R2_001.fastq.gz, out1=CPB2015-504C_R1_CLEAN.fq, out2=CPB2015-504C_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	24418818 reads 		3687241518 bases.
QTrimmed:               	22001 reads (0.09%) 	40790 bases (0.00%)
Trimmed by overlap:     	190102 reads (0.78%) 	8030806 bases (0.22%)
Total Removed:          	44 reads (0.00%) 	8071596 bases (0.22%)
Result:                 	24418774 reads (100.00%) 	3679169922 bases (99.78%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-504B_S650_L003_R1_001.fastq.gz, in2=CPB2015-504B_S650_L003_R2_001.fastq.gz, out1=CPB2015-504B_R1_CLEAN.fq, out2=CPB2015-504B_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	22851116 reads 		3450518516 bases.
QTrimmed:               	20430 reads (0.09%) 	37461 bases (0.00%)
Trimmed by overlap:     	85742 reads (0.38%) 	3366070 bases (0.10%)
Total Removed:          	44 reads (0.00%) 	3403531 bases (0.10%)
Result:                 	22851072 reads (100.00%) 	3447114985 bases (99.90%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-504A_S649_L003_R1_001.fastq.gz, in2=CPB2015-504A_S649_L003_R2_001.fastq.gz, out1=CPB2015-504A_R1_CLEAN.fq, out2=CPB2015-504A_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	29520922 reads 		4457659222 bases.
QTrimmed:               	26651 reads (0.09%) 	49050 bases (0.00%)
Trimmed by overlap:     	87864 reads (0.30%) 	3600874 bases (0.08%)
Total Removed:          	56 reads (0.00%) 	3649924 bases (0.08%)
Result:                 	29520866 reads (100.00%) 	4454009298 bases (99.92%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-419J_S638_L003_R1_001.fastq.gz, in2=CPB2015-419J_S638_L003_R2_001.fastq.gz, out1=CPB2015-419J_R1_CLEAN.fq, out2=CPB2015-419J_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	23547938 reads 		3555738638 bases.
QTrimmed:               	21893 reads (0.09%) 	42527 bases (0.00%)
Trimmed by overlap:     	348268 reads (1.48%) 	11612960 bases (0.33%)
Total Removed:          	58 reads (0.00%) 	11655487 bases (0.33%)
Result:                 	23547880 reads (100.00%) 	3544083151 bases (99.67%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-419I_S637_L003_R1_001.fastq.gz, in2=CPB2015-419I_S637_L003_R2_001.fastq.gz, out1=CPB2015-419I_R1_CLEAN.fq, out2=CPB2015-419I_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	23251758 reads 		3511015458 bases.
QTrimmed:               	21657 reads (0.09%) 	39288 bases (0.00%)
Trimmed by overlap:     	223360 reads (0.96%) 	8225022 bases (0.23%)
Total Removed:          	42 reads (0.00%) 	8264310 bases (0.24%)
Result:                 	23251716 reads (100.00%) 	3502751148 bases (99.76%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-419H_S636_L003_R1_001.fastq.gz, in2=CPB2015-419H_S636_L003_R2_001.fastq.gz, out1=CPB2015-419H_R1_CLEAN.fq, out2=CPB2015-419H_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	23686894 reads 		3576720994 bases.
QTrimmed:               	21846 reads (0.09%) 	40044 bases (0.00%)
Trimmed by overlap:     	382812 reads (1.62%) 	12581742 bases (0.35%)
Total Removed:          	48 reads (0.00%) 	12621786 bases (0.35%)
Result:                 	23686846 reads (100.00%) 	3564099208 bases (99.65%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-419G_S635_L003_R1_001.fastq.gz, in2=CPB2015-419G_S635_L003_R2_001.fastq.gz, out1=CPB2015-419G_R1_CLEAN.fq, out2=CPB2015-419G_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	28263066 reads 		4267722966 bases.
QTrimmed:               	26163 reads (0.09%) 	49106 bases (0.00%)
Trimmed by overlap:     	888952 reads (3.15%) 	28634492 bases (0.67%)
Total Removed:          	62 reads (0.00%) 	28683598 bases (0.67%)
Result:                 	28263004 reads (100.00%) 	4239039368 bases (99.33%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-419F_S634_L003_R1_001.fastq.gz, in2=CPB2015-419F_S634_L003_R2_001.fastq.gz, out1=CPB2015-419F_R1_CLEAN.fq, out2=CPB2015-419F_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	28144944 reads 		4249886544 bases.
QTrimmed:               	26193 reads (0.09%) 	49374 bases (0.00%)
Trimmed by overlap:     	440938 reads (1.57%) 	16135896 bases (0.38%)
Total Removed:          	60 reads (0.00%) 	16185270 bases (0.38%)
Result:                 	28144884 reads (100.00%) 	4233701274 bases (99.62%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-416D_S628_L003_R1_001.fastq.gz, in2=CPB2015-416D_S628_L003_R2_001.fastq.gz, out1=CPB2015-416D_R1_CLEAN.fq, out2=CPB2015-416D_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	26124044 reads 		3944730644 bases.
QTrimmed:               	24051 reads (0.09%) 	44920 bases (0.00%)
Trimmed by overlap:     	912034 reads (3.49%) 	32885472 bases (0.83%)
Total Removed:          	54 reads (0.00%) 	32930392 bases (0.83%)
Result:                 	26123990 reads (100.00%) 	3911800252 bases (99.17%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-416C_S627_L003_R1_001.fastq.gz, in2=CPB2015-416C_S627_L003_R2_001.fastq.gz, out1=CPB2015-416C_R1_CLEAN.fq, out2=CPB2015-416C_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	24597146 reads 		3714169046 bases.
QTrimmed:               	22580 reads (0.09%) 	41311 bases (0.00%)
Trimmed by overlap:     	646394 reads (2.63%) 	22908948 bases (0.62%)
Total Removed:          	48 reads (0.00%) 	22950259 bases (0.62%)
Result:                 	24597098 reads (100.00%) 	3691218787 bases (99.38%)



Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-416B_S626_L003_R1_001.fastq.gz, in2=CPB2015-416B_S626_L003_R2_001.fastq.gz, out1=CPB2015-416B_R1_CLEAN.fq, out2=CPB2015-416B_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	27070354 reads 		4087623454 bases.
QTrimmed:               	24752 reads (0.09%) 	46180 bases (0.00%)
Trimmed by overlap:     	427718 reads (1.58%) 	14457186 bases (0.35%)
Total Removed:          	62 reads (0.00%) 	14503366 bases (0.35%)
Result:                 	27070292 reads (100.00%) 	4073120088 bases (99.65%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-416A_S625_L003_R1_001.fastq.gz, in2=CPB2015-416A_S625_L003_R2_001.fastq.gz, out1=CPB2015-416A_R1_CLEAN.fq, out2=CPB2015-416A_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	23975496 reads 		3620299896 bases.
QTrimmed:               	21762 reads (0.09%) 	39348 bases (0.00%)
Trimmed by overlap:     	398636 reads (1.66%) 	13627938 bases (0.38%)
Total Removed:          	42 reads (0.00%) 	13667286 bases (0.38%)
Result:                 	23975454 reads (100.00%) 	3606632610 bases (99.62%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-406C_S624_L003_R1_001.fastq.gz, in2=CPB2015-406C_S624_L003_R2_001.fastq.gz, out1=CPB2015-406C_R1_CLEAN.fq, out2=CPB2015-406C_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	22379346 reads 		3379281246 bases.
QTrimmed:               	20773 reads (0.09%) 	36509 bases (0.00%)
Trimmed by overlap:     	698674 reads (3.12%) 	22179828 bases (0.66%)
Total Removed:          	44 reads (0.00%) 	22216337 bases (0.66%)
Result:                 	22379302 reads (100.00%) 	3357064909 bases (99.34%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-348E_S618_L003_R1_001.fastq.gz, in2=CPB2015-348E_S618_L003_R2_001.fastq.gz, out1=CPB2015-348E_R1_CLEAN.fq, out2=CPB2015-348E_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	29016662 reads 		4381515962 bases.
QTrimmed:               	26792 reads (0.09%) 	50626 bases (0.00%)
Trimmed by overlap:     	254732 reads (0.88%) 	11352758 bases (0.26%)
Total Removed:          	66 reads (0.00%) 	11403384 bases (0.26%)
Result:                 	29016596 reads (100.00%) 	4370112578 bases (99.74%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-348D_S617_L003_R1_001.fastq.gz, in2=CPB2015-348D_S617_L003_R2_001.fastq.gz, out1=CPB2015-348D_R1_CLEAN.fq, out2=CPB2015-348D_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	23519202 reads 		3551399502 bases.
QTrimmed:               	21219 reads (0.09%) 	40265 bases (0.00%)
Trimmed by overlap:     	224144 reads (0.95%) 	10071278 bases (0.28%)
Total Removed:          	50 reads (0.00%) 	10111543 bases (0.28%)
Result:                 	23519152 reads (100.00%) 	3541287959 bases (99.72%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-348C_S616_L003_R1_001.fastq.gz, in2=CPB2015-348C_S616_L003_R2_001.fastq.gz, out1=CPB2015-348C_R1_CLEAN.fq, out2=CPB2015-348C_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	22131206 reads 		3341812106 bases.
QTrimmed:               	20277 reads (0.09%) 	39764 bases (0.00%)
Trimmed by overlap:     	132686 reads (0.60%) 	6212342 bases (0.19%)
Total Removed:          	60 reads (0.00%) 	6252106 bases (0.19%)
Result:                 	22131146 reads (100.00%) 	3335560000 bases (99.81%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-348B_S615_L003_R1_001.fastq.gz, in2=CPB2015-348B_S615_L003_R2_001.fastq.gz, out1=CPB2015-348B_R1_CLEAN.fq, out2=CPB2015-348B_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	25610362 reads 		3867164662 bases.
QTrimmed:               	23474 reads (0.09%) 	43109 bases (0.00%)
Trimmed by overlap:     	250840 reads (0.98%) 	11333284 bases (0.29%)
Total Removed:          	56 reads (0.00%) 	11376393 bases (0.29%)
Result:                 	25610306 reads (100.00%) 	3855788269 bases (99.71%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-348A_S614_L003_R1_001.fastq.gz, in2=CPB2015-348A_S614_L003_R2_001.fastq.gz, out1=CPB2015-348A_R1_CLEAN.fq, out2=CPB2015-348A_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	28265290 reads 		4268058790 bases.
QTrimmed:               	25787 reads (0.09%) 	50057 bases (0.00%)
Trimmed by overlap:     	275304 reads (0.97%) 	11723716 bases (0.27%)
Total Removed:          	72 reads (0.00%) 	11773773 bases (0.28%)
Result:                 	28265218 reads (100.00%) 	4256285017 bases (99.72%)

Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-241C_S613_L003_R1_001.fastq.gz, in2=CPB2015-241C_S613_L003_R2_001.fastq.gz, out1=CPB2015-241C_R1_CLEAN.fq, out2=CPB2015-241C_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	25173708 reads 		3801229908 bases.
QTrimmed:               	23058 reads (0.09%) 	41589 bases (0.00%)
Trimmed by overlap:     	144058 reads (0.57%) 	7093326 bases (0.19%)
Total Removed:          	42 reads (0.00%) 	7134915 bases (0.19%)
Result:                 	25173666 reads (100.00%) 	3794094993 bases (99.81%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-241B_S612_L003_R1_001.fastq.gz, in2=CPB2015-241B_S612_L003_R2_001.fastq.gz, out1=CPB2015-241B_R1_CLEAN.fq, out2=CPB2015-241B_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	24953348 reads 		3767955548 bases.
QTrimmed:               	22437 reads (0.09%) 	42254 bases (0.00%)
Trimmed by overlap:     	154740 reads (0.62%) 	7516452 bases (0.20%)
Total Removed:          	48 reads (0.00%) 	7558706 bases (0.20%)
Result:                 	24953300 reads (100.00%) 	3760396842 bases (99.80%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-241A_S611_L003_R1_001.fastq.gz, in2=CPB2015-241A_S611_L003_R2_001.fastq.gz, out1=CPB2015-241A_R1_CLEAN.fq, out2=CPB2015-241A_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	29988356 reads 		4528241756 bases.
QTrimmed:               	27219 reads (0.09%) 	49638 bases (0.00%)
Trimmed by overlap:     	179022 reads (0.60%) 	8504754 bases (0.19%)
Total Removed:          	48 reads (0.00%) 	8554392 bases (0.19%)
Result:                 	29988308 reads (100.00%) 	4519687364 bases (99.81%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-209B_S610_L003_R1_001.fastq.gz, in2=CPB2015-209B_S610_L003_R2_001.fastq.gz, out1=CPB2015-209B_R1_CLEAN.fq, out2=CPB2015-209B_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	25811502 reads 		3897536802 bases.
QTrimmed:               	23918 reads (0.09%) 	48132 bases (0.00%)
Trimmed by overlap:     	260924 reads (1.01%) 	11585224 bases (0.30%)
Total Removed:          	74 reads (0.00%) 	11633356 bases (0.30%)
Result:                 	25811428 reads (100.00%) 	3885903446 bases (99.70%)


Executing jgi.BBDuk [-Xmx23g, in1=CPB2015-209A_S609_L003_R1_001.fastq.gz, in2=CPB2015-209A_S609_L003_R2_001.fastq.gz, out1=CPB2015-209A_R1_CLEAN.fq, out2=CPB2015-209A_R2_CLEAN.fq, minlen=25, qtrim=rl, trimq=10, ktrim=r, k=23, mink=11, hdist=1, tpe, tbo]

Input:                  	31469366 reads 		4751874266 bases.
QTrimmed:               	28833 reads (0.09%) 	50216 bases (0.00%)
Trimmed by overlap:     	337392 reads (1.07%) 	12000676 bases (0.25%)
Total Removed:          	52 reads (0.00%) 	12050892 bases (0.25%)
Result:                 	31469314 reads (100.00%) 	4739823374 bases (99.75%)
## map to linear reference Curated.fa in CHTC

## map to reference, rehead (referee)[https://gwct.github.io/referee/walkthrough.html] 

### took around 22hrs:
```
molecularecology@Chimborazo:/media/Summit/CHTC/staging/Modern_Museum/fastqs$ for j in `cat root.list`; do for R1 in `ls "$j"*R1*`; do for R2 in `ls "$j"*R2*`; do if [[ "$R1" == "$j"* ]] && [[ "$R2" == "$j"* ]]; then bwa mem -t 28 F_Kansas_60.fasta "$R1" "$R2" > "$j"_1.sam ; fi; done; done; done
```

## create .dict file for reheading

```
 java -jar picard.jar CreateSequenceDictionary R=F_Kansas_60.fasta O=F_Kansas.dict

#test on one

for java -jar picard.jar ReplaceSamHeader I=CPB2015-209A_1.sam HEADER=F_Kansas.dict O=new_hd1_CPB2015-209A_1.sam
CPB2015-209A_1.sam

#/media/Summit/88_fastq/cleaned/Linear_Bams

## run ANGSD per sample, sliding window selection test

```
### copy CPB WI and LI and rehead:
```
for sam in `ls C*sam`; do for root in `ls C*sam | sed 's/.sam//g'`; do if [[ "$sam" == "$root"* ]]; then java -jar picard.jar ReplaceSamHeader I="$sam" HEADER=F_Kansas.dict O=reheaded_1_"$root".sam; fi; done ;done
```

## compress and sort
```
for sam in `ls rehead*sam`; do for root in `ls C*sam | sed 's/.sam//g'`; do if [[ "$sam" == *"$root"* ]]; then samtools view -b "$sam" > "$root".bam; fi; done; done 

#sort

for bam in `ls C*bam`; do for root in `ls C*bam | sed 's/.bam//g'`; do if [[ "$bam" == *"$root"* ]]; then samtools sort "$bam" -o sorted_"$bam"; fi; done; done 


```

## test with two: /media/Summit/CHTC/staging/Modern_Museum/fastqs
```
ls sorted*209*bam >> test_2.list
#./angsd/angsd -nThreads 28 -nQueueSize 50 -doMaf 1 -dosaf 1 -GL 2 -doGlf 2 -doMajorMinor 1 -doCounts 1 -anc F_Kansas_60.fasta2 -remove_bads 1 -minMapQ #30 -minQ 20 -minInd 57 -minMaf 0.05 -setMinDepthInd 2 -setMinDepth 110 -setMaxDepth 550 -skipTriallelic 1 -SNP_pval 1e-3 -b plains_pest_bam_noNJ.list


#851 sites (way high coverage):
./angsd/angsd -nThreads 28 -nQueueSize 50 -dovcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 -doGlf 2 -doMajorMinor 1 -doCounts 1 -anc F_Kansas_60.fasta -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 2 -setMinDepth 110 -setMaxDepth 550 -skipTriallelic 1 -SNP_pval 1e-6 -b test_2.list -out test2

./angsd/angsd -nThreads 28 -nQueueSize 50 -dovcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 -doGlf 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doGlf 2 -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 2 -setMinDepth 2 -setMaxDepth 10 -skipTriallelic 1 -SNP_pval 1e-6 -b test_2.list -out test3

## on all 58: 

./angsd/angsd -nThreads 28 -nQueueSize 50 -dovcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 -doGlf 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 2 -setMinDepth 100 -setMaxDepth 1000 -skipTriallelic 1 -SNP_pval 1e-6 -b sorted_bam.list -out WI_LI_58

-> Tue Apr 20 17:37:02 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 779728311
	-> Number of sites retained after filtering: 28968444 
	[ALL done] cpu-time used =  97612.86 sec
	[ALL done] walltime used =  21957.00 sec


molecularecology@Chimborazo:/media/Summit/CHTC/staging/Modern_Museum/fastqs$ ./angsd/angsd -nThreads 28 -nQueueSize 50 -dobcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 -doGlf 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 2 -setMinDepth 100 -setMaxDepth 1000 -skipTriallelic 1 -SNP_pval 1e-6 -b sorted_bam.list -out WI_LI_58

```
## sort index then merge all samples:
```
molecularecology@Chimborazo:/media/Summit/88_fastq/cleaned/AUG_GAMS$ bcftools merge -m all *vcf.gz -o 60pest_vg.bcf --force-samples

```

## RAiSD:
```
molecularecology@Chimborazo:/media/Summit/CHTC/staging/Modern_Museum/fastqs/RAiSD/raisd-master$ ./bin/release/RAiSD -n FKS_all_run -I ../../nofields_WI_LI_58.vcf -P -D -A 0.995
```

## break up by population, generate vcfs and sfs:
```
## WI then LI
./angsd/angsd -nThreads 28 -nQueueSize 50 -dobcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 -doGlf 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 2 -setMinDepth 100 -setMaxDepth 1000 -skipTriallelic 1 -SNP_pval 1e-6 -b sorted_bam.list -out WI_LI_58
```

```
./angsd/angsd -nThreads 28 -nQueueSize 50 -dobcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doGlf 2 -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 2 -skipTriallelic 1 -SNP_pval 1e-6 -b WI_bam.list -out WI_25
-> Wed Apr 28 21:06:57 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 768000034
	-> Number of sites retained after filtering: 32632454 
	[ALL done] cpu-time used =  64669.69 sec
	[ALL done] walltime used =  23812.00 sec

./angsd/angsd -nThreads 28 -nQueueSize 50 -dobcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doGlf 2 -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 2 -skipTriallelic 1 -SNP_pval 1e-6 -b LI_bam.list -out LI_25
	-> Wed Apr 28 21:51:00 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 764728250
	-> Number of sites retained after filtering: 33712139 
	[ALL done] cpu-time used =  69175.77 sec
	[ALL done] walltime used =  26549.00 sec

```

## pyrho:
```optimize after generating lookuptables: hyprm_50_LI; hyprm_46_WI

conda activate my-pyrho-env
for z in `cat last_45_wi.list`; do pyrho optimize --vcffile /media/molecularecology/Summit/CHTC/staging/Modern_Museum/fastqs/"$z" --windowsize 90 --blockpenalty 15 --tablefile WI_lookuptable_46.hdf --ploidy 2 --outfile optimize_"$z".rho --numthreads 15; done

for z in `cat last_28_li.list`; do pyrho optimize --vcffile /media/molecularecology/Summit/CHTC/staging/Modern_Museum/fastqs/"$z" --windowsize 90 --blockpenalty 15 --tablefile LI_lookuptable_50.hdf --ploidy 2 --outfile optimize_"$z".rho --numthreads 15; done

```
## redo WI with 88 samples:
```
# dummy:
./angsd/angsd -b LI_bam.list -gl 2 -anc F_Kansas_60.fasta -ref F_Kansas_60.fasta -rf rf_agenic_regions_FKS.list -dosaf 1 -doCounts 1 -setMinDepth 125 -baq 1 -C 50 -minMapQ 30 -minQ 20 -P 20 -out LI_25_518 -fold 1 -dobcf 1 -doMajorMinor 1 -doPost 1 -doMaf 1 -dogeno 1 


./angsd/angsd -nThreads 28 -nQueueSize 50 -dobcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doGlf 2 -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 3 -setMinDepth 84 -setMaxDepth 280 -skipTriallelic 1 -SNP_pval 1e-6 -b WI_bams_update.list -out WI_28_64_snps
-> Fri Jun  4 19:40:59 2021
	-> Arguments and parameters for all analysis are located 
	in .arg file
	-> Total number of sites analyzed: 771302985
	-> Number of sites retained after filtering: 11870483 
	[ALL done] cpu-time used =  29651.48 sec
	[ALL done] walltime used =  8906.00 sec

./angsd/angsd -nThreads 28 -nQueueSize 50 -dobcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doGlf 2 -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 3 -setMinDepth 75 -setMaxDepth 250 -skipTriallelic 1 -SNP_pval 1e-6 -b LI_bam.list -out LI_25_64_snps
-> Fri Jun  4 16:08:27 2021
-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 764728250
	-> Number of sites retained after filtering: 12428611 
	[ALL done] cpu-time used =  33719.42 sec
	[ALL done] walltime used =  9656.00 sec

# for SFS:
./angsd/angsd -b LI_bam.list -gl 2 -anc F_Kansas_60.fasta -ref F_Kansas_60.fasta -rf rf_agenic_regions_FKS.list -dosaf 1 -doCounts 1 -setMinDepthInd 3 -setMinDepth 75 -setMaxDepth 250 -baq 1 -C 50 -minMapQ 30 -minQ 20 -P 20 -out LI_25_64 -fold 1
-> Sat Jun  5 18:42:13 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 749452643
	-> Number of sites retained after filtering: 152017697 
	[ALL done] cpu-time used =  57360.21 sec
	[ALL done] walltime used =  105389.00 sec

## rerun with greater min coverage:
./angsd/angsd -b LI_bam.list -gl 2 -anc F_Kansas_60.fasta -ref F_Kansas_60.fasta -rf rf_agenic_regions_FKS.list -dosaf 1 -doCounts 1 -setMinDepthInd 5 -setMinDepth 125 -setMaxDepth 250 -baq 1 -C 50 -minMapQ 30 -minQ 20 -P 20 -out LI_25_67 -fold 1

-> Tue Jun  8 17:17:36 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 749452643
	-> Number of sites retained after filtering: 2421857 
	
./angsd/angsd -b WI_bams_update.list -gl 2 -anc F_Kansas_60.fasta -ref F_Kansas_60.fasta -rf rf_agenic_regions_FKS.list -dosaf 1 -doCounts 1 -setMinDepthInd 3 -setMinDepth 84 -setMaxDepth 250 -baq 1 -C 50 -minMapQ 30 -minQ 20 -P 20 -out WI_28_64_pruned_sfs -fold 1
-> Sat Jun  5 19:34:57 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 756084479
	-> Number of sites retained after filtering: 136785813 
	[ALL done] cpu-time used =  61582.83 sec
	[ALL done] walltime used =  108592.00 sec
	
## rerun with greater min coverage:
./angsd/angsd -b WI_bams_update.list -gl 2 -anc F_Kansas_60.fasta -ref F_Kansas_60.fasta -rf rf_agenic_regions_FKS.list -dosaf 1 -doCounts 1 -setMinDepthInd 5 -setMinDepth 140 -setMaxDepth 280 -baq 1 -C 50 -minMapQ 30 -minQ 20 -P 20 -out WI_28_67_pruned_sfs -fold 1
-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 756084479
	-> Number of sites retained after filtering: 1940286 
	[ALL done] cpu-time used =  54910.11 sec
	[ALL done] walltime used =  107761.00 sec


## redo SFS for these folded spectra now:
./angsd/misc/realSFS WI_28_64_pruned_sfs.saf.idx
130220822.903196 1745838.471290 1452524.392505 89.870898 824163.412282 545503.179285 154422.886774 48050.092423 278924.805313 219224.322110 189897.613812 95469.700656 47534.789611 107072.892167 78181.479312 107651.174927 78945.956195 59517.093802 51004.237046 74623.769265 28323.249887 68545.986047 47160.651103 66065.441200 31895.994982 41708.979510 30586.404091 68150.817959 23912.432259 

./angsd/misc/realSFS LI_25_64.saf.idx
144866642.296978 2025697.410711 1028039.426052 1024572.644550 73074.709766 825372.501435 140744.267764 232395.573115 231575.522661 250249.022986 100275.666490 119540.505915 165723.188058 72277.109795 113787.311823 115171.627191 32176.285868 110849.173735 35545.151758 158546.538284 2731.271602 39692.169016 124442.519525 23208.967912 60502.295761 44863.841142

./angsd/misc/realSFS LI_25_67.saf.idx
2172805.170480 93502.975072 47197.913153 25570.061219 18664.781578 10405.010159 9933.615111 5318.223989 6974.010255 2078.184251 5302.306359 2183.856913 1997.569976 3278.354482 445.390105 3256.638358 839.878270 1158.949238 1483.137017 1490.535563 1224.322593 1515.039821 622.245344 1427.021917 674.667181 2507.141596

./angsd/misc/realSFS WI_28_67_pruned_sfs.saf.idx
1753081.088420 63566.982860 36336.191748 20012.805936 13067.244239 8956.730560 8804.218274 2252.888625 6568.686253 1843.315248 3122.986048 2036.498996 2957.371839 901.732853 2078.892155 1046.905746 1332.730411 827.028026 1360.362979 1102.825709 1289.585854 637.691565 550.160954 1673.181141 573.255905 298.487313 449.488895 1331.887789 2224.773659 

## rerun stairway plot WIblueprint
(delete first value)
molecularecology@Chimborazo:/media/molecularecology/Summit/Chapter_3/stairway_plot_v2.1.1$ java -cp stairway_plot_es/ Stairbuilder WI.blueprint


## rerun pyrho (with demographic history here)
```

## run RAiSD on each scaffold using *snps vcf: LI_25_64_snps & WI_28_64_snps
```
# break up each scaffold?
molecularecology@Chimborazo:/media/Summit/CHTC/staging/Modern_Museum/fastqs/RAiSD/raisd-master$ ./bin/release/RAiSD -n FKS_all_run -I ../../nofields_WI_LI_58.vcf -P -D -A 0.995

#remove formats 
molecularecology@Chimborazo:/media/molecularecology/Summit/CHTC/staging/Modern_Museum/fastqs$ bcftools annotate -x FORMAT LI_25_64_snps.bcf --threads 10 >> nofield_LI_25_64_snps.vcf


WI_28_64_snps.bcf >> nofield_WI_28_64_snps.vcf

## run 
./bin/release/RAiSD -n New_LI -I ../../nofield_LI_25_64_snps.vcf -P -D -A 0.995
-n (output prefix)
-I input
-P generates R output
-D Generates a site report, e.g., total, discarded, imputed etc.
-A 0.995 is probability used, generates Manhattan plot

Command: ./bin/release/RAiSD -n New_LI -I ../../nofield_LI_25_64_snps.vcf -P -D -A 0.995 

 Samples: 25
 Format:  vcf
 Total execution time 6960.64531 seconds

 Command: ./bin/release/RAiSD -n New_WI -I ../../nofield_WI_28_64_snps.vcf -P -D -A 0.995 
```
## run angsd for folded with no upper limit, get more sites
```molecularecology@Chimborazo:/media/molecularecology/Summit/CHTC/staging/Modern_Museum/fastqs$ ./angsd/angsd -b WI_bams_update.list -gl 2 -anc F_Kansas_60.fasta -ref F_Kansas_60.fasta -rf rf_agenic_regions_FKS.list -dosaf 1 -doCounts 1 -setMinDepthInd 5 -setMinDepth 140 -setMaxDepth 2800 -baq 1 -C 50 -minMapQ 30 -minQ 20 -P 20 -out WI_28_69_pruned_sfs -fold 1

 Thu Jun 10 20:56:06 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 756084479
	-> Number of sites retained after filtering: 2950966 
	
molecularecology@Chimborazo:/media/molecularecology/Summit/CHTC/staging/Modern_Museum/fastqs$ ./angsd/angsd -b LI_bam.list -gl 2 -anc F_Kansas_60.fasta -ref F_Kansas_60.fasta -rf rf_agenic_regions_FKS.list -dosaf 1 -doCounts 1 -setMinDepthInd 5 -setMinDepth 125 -setMaxDepth 2500 -baq 1 -C 50 -minMapQ 30 -minQ 20 -P 20 -out LI_25_69 -fold 1

-> Thu Jun 10 19:56:50 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 749452643
	-> Number of sites retained after filtering: 3487833 

./angsd/misc/realSFS WI_28_69_pruned_sfs.saf.idx
2704318.109317 86382.569709 45679.342434 25629.031310 18327.176978 10734.271206 10906.643441 2735.517904 7863.275736 4764.908034 2513.636641 2427.971970 2568.808915 3703.444623 1711.832291 1585.193135 1757.211743 1027.068678 1734.443771 2293.723041 465.361128 544.124323 2753.978644 673.377248 1409.189501 174.773558 35.318316 1390.446658 4847.249748

./angsd/misc/realSFS LI_25_69.saf.idx
3147255.393600 134795.770261 62369.120939 36468.022746 22161.546664 15405.173744 11367.740804 8087.595641 7229.199204 5188.755748 4950.445953 3063.663642 3492.626614 2780.255365 2807.263252 2080.772292 2017.649145 2013.433219 1503.158263 2214.150637 1161.956133 1690.546003 1525.059647 1957.690660 1509.217856 2732.791972
```

## dadi joint, folded sfs

```
-b WI_bams_update.list & LI_bam.list

./angsd/angsd -nThreads 28 -nQueueSize 50 -dobcf 1 -doMaf 1 -dopost 1 -dosaf 1 -gl 2 --ignore-RG 0 -dogeno 1 -anc F_Kansas_60.fasta -doGlf 2 -doMajorMinor 1 -doCounts 1 -remove_bads 1 -minMapQ 30 -minQ 20 -minMaf 0.05 -setMinDepthInd 3 -setMinDepth 84 -setMaxDepth 2800 -skipTriallelic 1 -SNP_pval 1e-6 -b WI_LI_update_bams.list -out WI_LI_611_snps


```
-> Fri Jun 11 20:47:26 2021
	-> Arguments and parameters for all analysis are located in .arg file
	-> Total number of sites analyzed: 778608467
	-> Number of sites retained after filtering: 27647075 
```


```
## break up vcf for pyrho:
```
sed -i 's/_/-/g' WI_28_64_snps.bcf
sed -i 's/_/-/g' LI_25_64_snps.bcf

bgzip -c WI_28_64_snps.bcf > WI_28_64_snps.bcf.vcf.gz
bgzip -c LI_25_64_snps.bcf > LI_25_64_snps.bcf.vcf.gz

tabix -p vcf WI_28_64_snps.bcf.vcf.gz
tabix -p vcf LI_25_64_snps.bcf.vcf.gz

for z in `cat wi_scaffold.list`; do echo tabix -h LI_25_64_snps.bcf.vcf.gz "$z" > LI_"$z".vcf
for z in `cat wi_scaffold.list`; do echo tabix -h WI_28_64_snps.bcf.vcf.gz "$z" > WI_"$z".vcf


```
# optimize
```
pyrho optimize --vcffile <data> --windowsize <w> --blockpenalty <bpen> \
--tablefile <make_table_output> --ploidy <ploidy> --outfile <output_file> \
--numthreads <par>

