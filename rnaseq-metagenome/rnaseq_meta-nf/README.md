# Microbial RNAseq
Analysis of RNAseq data from (host-associated) microbial mixtures

## Quick Start
>The following commands presumes you have nextflow installed as above along with the `~/.nextflow/config` file set up as described above.
Alternatively, you can use "-C" flag to assign your nextflow config file.


Usage:

nextflow run Channing-Zeng/metagenomics-nf/rnaseq-metagenome/rnaseq_meta-nf  <ARGUMENTS>

## Example
nextflow 
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/rnaseq-metagenome/rnaseq_meta-nf \
    --batchfile batchfile.csv \
    --genome_list genome_list.csv \
    --host_genome ref_genomes/AY064377.1.fasta.tar \
    --min_cov_pct 10 \
    --output_folder my_results/ \
    -with-docker ubuntu:16.04 \
    -process.executor 'local'


## Input Files

### Batch file

A "batch" CSV file contains all the paths to sample fastq files, see example file "bactchfile.csv".

### Reference Genomes

Each reference genome has:

  * A unique name (probably best to avoid any whitespaces)
  * A gzipped FASTA file
  * A gzipped GFF3 file

See "test/genome_list.csv"

### Host Genome

A ".tar" format reference file to exclude host reads.



## Output files

This tool creates many CSV files in the `--output_folder`. These include:

  * `<output_prefix>.mapping_summary.csv`: Number of reads input, filtered against host, aligned against genomes.
  * `<output_prefix>.all.csv`: Depth of sequencing for every gene across all samples in all organisms (long format).
  * `<output_prefix>.CDS.csv`: The weighted average depth of sequencing across all CDS genes, broken out by organism and sample.
  * `<output_prefix>.rRNA.csv`: The weighted average depth of sequencing across all rRNA genes, broken out by organism and sample.
  * `<output_prefix>.rRNA_CDS_ratio.csv`: The weighted average depth of sequencing of the rRNA genes / CDS genes, broken out by organism and sample.
  * `<output_prefix>.<organism_name>.csv`: The depth of sequencing for each gene in a given organism, across all samples


