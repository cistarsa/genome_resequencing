#### generate variant graph using PGGB (pangenome)roughly as edyeet --> seqwish --> smoothxg (>260G used)

```
cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg convert -g smoothed/aln5_smoothed.gfa -v > aln5_smooothed_gfa.vg

# chunk:
cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg chunk -x aln5_smooothed_gfa.vg -C -p "$j" > subgraph_aln5/"$j".vg; done

# mod each chunk:
cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg mod -X 256 subgraph_aln5/"$j".vg > subgraph_aln5/mod_"$j"_gfa.vg; done
## node id space?

#vg ids -j $(for i in $(seq 1 22; echo X; echo Y); do echo chr${i}.vg; done)
# echo ./vg/variant_graph_refs/vg ids -j $(for i in `cat F_Kansas_scaffs.list`; do echo subgraph_aln5/mod_"$j"_gfa.vg; done)

##xg index for each .vg chromosome:
#vg index -x all.xg $(for i in $(seq 1 22; echo X; echo Y); do echo chr${i}.vg; done)

cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg index -p -t 16 -b ./ -x subgraph_aln5/"$j"_aln5c.xg subgraph_aln5/mod_"$j"_gfa.vg; done

## prune:
#for i in $(seq 1 22; echo X; echo Y); do
#  vg prune chr${i}.vg > chr${i}.pruned.vg
#done

cohen@denali:/data2/zach_data$ for i in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg prune subgraph_aln5/mod_"$i"_gfa.vg > subgraph_aln5/pruned_mod_"$i"_gfa.vg; done


##gcsa index:

cohen@denali:/data2/zach_data$ for j in `cat F_Kansas_scaffs.list`; do ./vg/variant_graph_refs/vg index -t 16 -p -b ./ -k 11 -X 3 -g subgraph_aln5/"$j"_aln5c.gcsa subgraph_aln5/pruned_mod_"$j"_gfa.vg; done


-x _alln5c.xg subgraph_aln5/mod_"$j"_gfa.vg -p -t 16; done
out:
Building XG index
Saving XG index to aln5_smooothed_gfa.xg
Memory usage: 8.24732 GB
```

#### pre gcsa index pruning and mod:

```
##Found kmer with offset >= 1024. GCSA2 cannot handle nodes greater than 1024 bases long. To enable indexing, modify your graph using `vg mod -X 256 x.vg >y.vg`. AAAAAAACACAAGGAA	1898918:1024	A	A	1898918:1040

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg mod -X 256 pruned_aln5_smooothed_gfa.vg > mod_pruned_aln5_smooothed_gfa.vg 

cohen@denali:/data2/zach_data$ ./vg/variant_graph_refs/vg index -t 16 -p -b ./ -k 11 -X 3 -g aln5_smooothed_gfa.gcsa mod_pruned_aln5_smooothed_gfa.vg
```

## chunk graph by scaffold:
