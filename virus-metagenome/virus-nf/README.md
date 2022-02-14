# Viral Metagenomics by Assembly and Alignment
Reproducible computational pipeline for viral metagenomics that is relatively portable between computational infrastructures.


## Quick Start
>The following commands presumes you have nextflow installed as above along with the `~/.nextflow/config` file set up as described above.
Alternatively, you can use "-C" flag to assign your nextflow config file.


Usage:

nextflow run Channing-Zeng/metagenomics-nf/virus-metagenome/virus-nf  <ARGUMENTS>

Required Arguments:
  --manifest            CSV file listing samples (see below)
  --output_folder       Folder to place analysis outputs
  --output_prefix       Text used as a prefix for output files
  --human_genome_tar    Indexed human genome, gzipped tarball


## Example
nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/virus-metagenome/virus-nf \
        --output_folder my_result \
        --output_prefix example \
        --manifest manifest.csv \
        --human_genome_tar human_mitochondrial_genome.fasta.tar.gz


## Input data
Manifest:
  The manifest is a CSV with a header indicating which samples correspond to which files.
  The file must contain the columns `specimen` and `fastq`. FASTQ files should be gzip-compressed.



## Approach

The analytical workflow will perform the following steps for each sample:

  1. Perform quality trimming and remove adapters
  2. Remove optical / PCR duplicates
  3. Remove human sequences by mapping against the human genome
  4. Assemble reads _de novo_ into contigs
  5. Map reads against contigs
  6. Calculate summary metrics for each contig
  7. Collect results across all samples

