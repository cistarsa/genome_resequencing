## PF and PM synteny using Satsua on chtc
```
break up PM assembly into 530 scaffolds and run each against PF complete assembly as:
tar -xzf tig*tgz
cd tig*
frag=${PWD##*/}
cd ../
tar -xzf satsuma-code-0.tgz
echo=$frag
./satsuma-code-0/SatsumaSynteny -q F1-haplotypePF.contigs_v2.fasta -t $frag/$frag -o "$frag"_out -m 1 -ni 10 -n 1

tar -czf "$frag"_out.tgz "$frag"_out
cp "$frag"_out.tgz /home/zcohen3/Ldecs/test_1/

exit
```

some stats: 300 of 532 Male scaffolds (557,144,636 of 810,431,279) map to 309 of 643 female scaffolds (861,379,015 of 880,547,378)
these matches refer to 260,533,093 shared nucleotides 

try previous version 


## using rgaat locally, this takes gf3 anf fna files 

generate alignment of old to new using bowti2-2.4.1-linux-x86_64
