# wtdbg

De novo assembler for long noisy sequences

Author: Jue Ruan <ruanjue@gmail.com>

## Usage
`wtdbg` [options]
## Options:

```
 -t <int>    Number of threads, 0: all cores, [1]
 -i <string> Long reads sequences file, + *
 -I <string> Accurate contig sequences file, +
 -r          Search nodes on accurate contig sequences only
 -T <int>    Limitation of total base-pairs in Mb, usually for test [0]
 -R          Rapid subsampling instead of aligning all intervals
 -j <int>    Expected length of node, [1000] bp
 -J <int>    Distance of next node start, 0: the same as <-j> [0] bp
 -X <float>  Max overlapped fraction of two adjacent nodes in a read, [0.2]
 -e <int>    Min cov of edges, [3]
 -n <int>    Min cov of nodes, 0: the same as <-e> [0]
 -N <int>    Max cov of nodes, remove too-high coverage nodes [200]
 -L <string> Load graph from "<your_prefix>.nodes" instead of build, [NULL]
 -b <int>    Max steps of bubble, [20]
 -d <int>    Max steps of tips, [5]
 -o <string> Prefix of output files, *
 -f          Force overwrite
 -v          Verbose
 -0          Output as less files as it can
 -----------parameters of node alignment-----------
 -H          Trun on homopolymer compression
 -k <int>    Kmer size, 5 <= value <= 32, [15]
 -W <int>    Max size of insertion in the middle of kmer when querying, [0]
             PART1|ins|PART2, PART1 + PART2 = ksize, PART2 = ksize/2, ins <= max_kgap, max_kgap + ksize <= 32
 -K <float>  Filter high frequency kmers, maybe repetitive, [0.05]
             if K >= 1, take the integer value as cutoff
             else, mask the top fraction part high frequency kmers
 -E <int>    Min kmer frequency, [2]
 -S <float>  Subsampling kmers, 1/(int((<-S> * 100) % 100) * int(<-S>)) kmers are indexed, [1.01]
             Decimal part is used for minimizer window size
             Fraction part is used for HASH based subsampling
 -x <int>    Intra-block: Max gap  [256]
 -y <int>    Intra-block: Max deviation [128]
 -z <int>    Intra-block: Min kmer [3]
 -w <int>    Inter-block: deviation penalty [1.0]
 -u <int>    Inter-block: gap penalty [0.1]
 -l <float>  Min fraction of alignment:aligned / <expected_node_length>, [0.7]
 -m <float>  Min fraction of alignment:matched / <expected_node_length>, [0.1]
 -s <float>  Max length variation of two aligned fragments, [0.2]
 ------------parameters of refine alignment-------
 -Z <int>    Try to align selected nodes against potential matched reads, [0]
             5 <= value <= 27, suggested 10, like -k, set to 0 to disable refinement
             All align parameters after -Z is set to realignment parameters
             default: -Z 0 -K 0 -S 1.01 -x 256 -y 64 -z 3 -w 1.0 -u 0.1 -l 0.70 -m 0.20 -s 0.2
 -------------------------------------------------
 -M <int>    Test functions, +
             1: don't skip to align a new node when it conflicts with previous repetitive nodes
             2: output alignments to <prefix>.alignments
             3: filter tip-like nodes
             4: don't keep low coverage edges in graph
             5: don't filter nodes are likely to be repetitive by local subgraph analysis
```
