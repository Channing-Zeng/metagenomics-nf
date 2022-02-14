# Circulator-NF
Nextflow workflow running the Circulator tool for microbial genome assembly
For details on the Circulator tool, see [the documentation](https://sanger-pathogens.github.io/circlator/).

## Quick Start
>The following commands presumes you have nextflow installed as above along with the `~/.nextflow/config` file set up as described above.
Alternatively, you can use "-C" flag to assign your nextflow config file.


Usage:

nextflow run Channing-Zeng/metagenomics-nf/assembly-hybrid/circulator-nf  <ARGUMENTS>

Required Arguments:
  --manifest            File containing the location of all input genomes and reads to process
  --output_folder       Folder to place analysis outputs


## Example
nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/assembly-hybrid/circulator-nf \
    --manifest manifest.csv \
    --output_folder my_result


## Input data
### Manifest

The manifest is a comma-separated table (CSV) with three columns, name, fasta, and reads. For example:
```
    name,fasta,reads
    genomeA,assemblies/genomeA.fasta.gz,pacbio_reads/genomeA.fastq.gz
    genomeB,assemblies/genomeB.fasta.gz,pacbio_reads/genomeB.fastq.gz
```
