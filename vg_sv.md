#
# vg surject -x x.xg -b aln.gam > aln.bam
for base in `ls *pg | sed 's/.gam.pg//g'; do for aug in `ls aug*aug`; do for pg in `ls *pg`; do if do if [[ "$gam" == *"$base"* ]] && [[ "$pg" == *"$base"* ]]; then ./vg surject -x "$pg" -b "$aug" > "$base".bam; fi; done; done; done
