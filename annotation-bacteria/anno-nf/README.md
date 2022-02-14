# Nextflow tool running the NCBI Prokaryotic Genome Annotation Pipeline

The goal of this tool is to run the NCBI Prokaryotic Genome Annotation Pipeline
on arbitrary sets of genomes using the Nextflow system for workflow management.


## Quick Start
>The following commands presumes you have nextflow installed as above along with the `~/.nextflow/config` file set up as described above.
Alternatively, you can use "-C" flag to assign your nextflow config file.


Usage:

nextflow run Channing-Zeng/metagenomics-nf/annotation-bacteria/anno-nf  <ARGUMENTS>


Required Arguments:
  --sample_sheet        Sample sheet linking each genome FASTA with its corresponding annotation YAML
  --output_folder       Folder to place analysis outputs


## Example

nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/annotation-bacteria/anno-nf \
    --sample_sheet sample_sheet.csv \
    --output_folder my_result



## Input Data

In order to run this tool, you will need to provide:

  1) Genome sequences in FASTA format (NOTE: files cannot be compressed in any way)
  2) Annotations for each genome in YAML format (example below)
  3) Sample sheet linking each genome FASTA with its corresponding annotation YAML


### Sample Sheet Format
The sample sheet linking each genome FASTA with its corresponding annotation YAML
must be formatted as a CSV with two named columns, `fasta` and `yaml`. 

CSV file content example:

```
fasta,yaml
local_folder/genome1.fasta,local_folder/genome1.yaml
local_folder/genome2.fasta,local_folder/genome2.yaml
```


