## generate variant graph using PGGB (pangenome)roughly as edyeet --> seqwish --> smoothxg (>260G used)

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg convert -g smoothed/aln5_smoothed.gfa -v > aln5_smooothed_gfa.vg
##xg index:
cohen@denali:/data2/zach_data$ nohup ./vg/variant_graph_refs/vg index -x aln5_smooothed_gfa.xg aln5_smooothed_gfa.vg -p -t 16
out:
Building XG index
Saving XG index to aln5_smooothed_gfa.xg
Memory usage: 8.24732 GB
    
## pre gcsa index pruning:
cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg prune -r aln5_smooothed_gfa.vg > pruned_aln5_smooothed_gfa.vg
