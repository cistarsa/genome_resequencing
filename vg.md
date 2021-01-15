## generate variant graph using PGGB (pangenome)roughly as edyeet --> seqwish --> smoothxg (>260G used)

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg convert -g smoothed/aln5_smoothed.gfa -v > aln5_smooothed_gfa.vg
##xg index:
cohen@denali:/data2/zach_data$ nohup ./vg/variant_graph_refs/vg index -x aln5_smooothed_gfa.xg aln5_smooothed_gfa.vg -p -t 16
out:
Building XG index
Saving XG index to aln5_smooothed_gfa.xg
Memory usage: 8.24732 GB
    
## pre gcsa index pruning and mod:

##Found kmer with offset >= 1024. GCSA2 cannot handle nodes greater than 1024 bases long. To enable indexing, modify your graph using `vg mod -X 256 x.vg >y.vg`. AAAAAAACACAAGGAA	1898918:1024	A	A	1898918:1040

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg mod -X 256 pruned_aln5_smooothed_gfa.vg > mod_pruned_aln5_smooothed_gfa.vg 

cohen@denali:/data2/zach_data$ nohup ./vg/variant_graph_refs/vg index -g aln5_smooothed_gfa.gcsa mod_pruned_aln5_smooothed_gfa.vg -t 16 -p
