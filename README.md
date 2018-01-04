# PEHaplo

PEHaplo is a *de novo* assembly tool for recovering virus haplotypes from virus quasispecies sequencing data. It utilizes overlap graph and paired-end information to recover virus haplotypes. 

It takes paired-end reads file as input and outputs contigs that are part of or full haplotypes.

PEHaplo does not need any reference genomes and thus can be applied for identifying new haplotyps or haplotypes that are remotely related to characterized ones. 

# Quick Start
To quickly test the core assembly algorithm, we have prepared the procssed data set (after error correction, removing duplicates, reads orientation adjustment, etc.) in folder processed_test_data. 

## Dependencies
1. Python 2.7.x
2. Python module: [networkx](https://networkx.github.io)
pip install networkx
3. [Apsp](https://github.com/chjiao/Apsp)
cd Apsp/
make
Copy the compiled binary file Apsp to your path.


# Dependencies
PEHaplo is developed based on Python 2.7

Python module: [networkx](https://networkx.github.io)

[Karect](https://github.com/aminallam/karect)

[Readjoiner](http://www.zbh.uni-hamburg.de/forschung/gi/software/readjoiner.html)

[Apsp](https://github.com/chjiao/Apsp)

[SGA](https://github.com/jts/sga)

For contigs correction based on alignment:

[Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)

# Usage
```python 
python pehaplo.py [-h] -f1 INPUT_F1 -f2 INPUT_F2 -l OVERLAP_LEN -r READ_LEN [-l1 OVERLAP_LEN1] [-F FRAGMENT_LEN] [-std FRAGMENT_STD] [-n DUP_N] [-correct CONTIG_CORRECT] [-t THREADS]
```

Arguments:

  -f1 INPUT_F1          input .1 part of paired-end fasta file
  
  -f2 INPUT_F2          input .2 part of paired-end fasta file
  
  -l OVERLAP_LEN, --overlap_len OVERLAP_LEN
                        overlap threshold between reads for overlap graph construction
                        
  -l1 OVERLAP_LEN1, --overlap_stage1 OVERLAP_LEN1
                        overlap cutoff to remove potentially error overlaps after merging linked cliques, default same as -l
                        
  -n DUP_N, --dup_n DUP_N
                        keep the reads that are duplicated at least n times
                        
  -r READ_LEN, --read_len READ_LEN
                        reads length
                        
  -F FRAGMENT_LEN, --fragment_len FRAGMENT_LEN
                        paired-end reads insert size, default as 2.5*read_len
                        
  -std FRAGMENT_STD     standard deviation of paired-end reads insert size,
                        default as 100
                        
  -n DUP_N, --dup_n DUP_N
                        the reads kept should be duplicated at least n times,
                        default as keep all the duplicates removed reads
                        
  -correct CONTIG_CORRECT
                        whether apply alignment based contigs
                        correction(yes/no), default: no
                        
  -t THREADS, --threads THREADS
                        threads for karect, sga, bowtie2
