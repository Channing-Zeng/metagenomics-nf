# Pangenome Analysis using anvi'o
Analyze a set of genomes with the [anvi'o](http://merenlab.org/software/anvio/) pangenome pipeline

### Quick Start
>The following commands presumes you have nextflow installed as above along with the `~/.nextflow/config` file set up as described above.
Alternatively, you can use "-C" flag to assign your nextflow config file.

Usage:

nextflow run Channing-Zeng/metagenomics-nf/pan-genome/pan-nf  <ARGUMENTS>

### Example
nextflow \
    -C ~/nextflow.config \
    run Channing-Zeng/metagenomics-nf/pan-genome/pan-nf \
    --sample_sheet species_test.csv \
    --output_folder my_result \
    --output_name EXAMPLE_OUTPUT \
    --min_alignment_fraction 0 \
    --category_name species \
    --mcl_inflation 10


### Input Data

1. A set of genomes in FASTA format
2. A CSV text file describing each genome above with minimal two column: genome and name. See "tests/sample_sheet.txt".
