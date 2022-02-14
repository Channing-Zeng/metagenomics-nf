# Hybrid Assembly - Nextflow

De novo assembly using UniCycler, within a Nextflow workflow

## Quick Start
>The following commands presumes you have nextflow installed as above along with the `~/.nextflow/config` file set up as described above.
Alternatively, you can use "-C" flag to assign your nextflow config file.


Usage:

nextflow run Channing-Zeng/metagenomics-nf/assembly-hybrid/hybrid-nf  <ARGUMENTS>

Arguments:
  --sample_sheet       CSV file listing samples to analyze
  --output_folder      Folder to place outputs

Options:
  --short_reads        Sample sheet contains short read data (`short_R1` and `short_R2`)
  --long_reads         Sample sheet contains long read data (`long_reads`)
  --min_fasta_length   Minimum contig length (default: 100)
  --help


## Example 
nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/assembly-hybrid/hybrid-nf \
    --sample_sheet manifest.csv \
    --output_folder my_result


## input data
Sample Sheet:
  The sample_sheet is a CSV with a header indicating which samples correspond to which files.
  The file must contain the column `name`, and `long_reads`, `short_R1`, `short_R2` as appropriate.

