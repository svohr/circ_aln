# circ_aln
Simple scripts for circularizing alignments to a linear reference

## About
This repository contains scripts for mapping reads to the circular reference
using `bwa`, `samtools`, and a custom python script `circ_fix` that uses
[pysam](https://github.com/pysam-developers/pysam) to manipulate aligned reads.
The strategy used here is to align single reads to the original reference
sequence and a modified version where some of the sequence from the start are
appended to the end of the sequence. The `circ_fix` script then takes the
reads that map across the end and start of the original sequence and splits
them into two segments at this point and moves the second half to the beginning
of the sequence. These new segments are added to the alignments to the original
(linear) reference, after removing any existing alignments for these reads.

These scripts use `bwa mem` but any alignment tool that produces bam files
could be used in its place. The `circ_fix` script works well enough on human
mtDNA sequences, but has not been tested extensively, especially in cases
where indels and clipping span the end and start of the reference.

## Usage

```
circ_index mtDNA.fa

circ_aln mtDNA.fa reads.fq reads.mtDNA
```

