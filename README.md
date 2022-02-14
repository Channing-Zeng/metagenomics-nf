## Re-build metagenomics workflow with NextFlow DSL=2.0 to make it compatible with different computation platforms (e.g. local, HPC, cloud, or hybrid)
## NextFlow is a popular workflow management tool written in Groovy


# Quick Start

## Installing NextFlow
i) Install the java runtime environment (at least version 8)

ii) curl -s https://get.nextflow.io | bash

## Example
When running pipelines, first go to the directory where the input data is located.
### Assembling microbial genome (support hybird sequencing method)
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/assembly-hybrid/hybrid-nf/README.md

nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/assembly-hybrid/hybrid-nf \
    --sample_sheet manifest.csv \
    --output_folder my_result

### Circularising assembled genome
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/assembly-hybrid/circulator-nf/README.md

nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/assembly-hybrid/circulator-nf \
    --manifest manifest.csv \
    --output_folder my_result


### Annotating bacteria genome
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/annotation-bacteria/anno-nf/README.md

nextflow
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/annotation-bacteria/anno-nf \
    --sample_sheet sample_sheet.csv \
    --output_folder my_result


### Investigating pan-genome
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/pan-genome/pan-nf/README.md

nextflow \
    -C ~/nextflow.config \
    run Channing-Zeng/metagenomics-nf/pan-genome/pan-nf \
    --sample_sheet species_test.csv \
    --output_folder my_result \
    --output_name EXAMPLE_OUTPUT \
    --min_alignment_fraction 0 \
    --category_name species \
    --mcl_inflation 10

### Analyzing meta-RNASeq data
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/rnaseq-metagenome/rnaseq_meta-nf/README.md

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

### Analyzing meta-viral data (with reference or de-novo)
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/virus-metagenome/virus-nf/README.md

nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/virus-metagenome/virus-nf \
        --output_folder my_result \
        --output_prefix example \
        --manifest manifest.csv \
        --human_genome_tar human_mitochondrial_genome.fasta.tar.gz

### Analyzing 16SrRNA amplicon data
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/blob/master/16S-rRNA/16S-nf/README.md

nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/16S-rRNA/16S-nf \
    --manifest manifest.csv \
    --output my_result \
    --email example@email.com \
    --repo_fasta test.repo.fasta \
    --repo_si test.repo.seq_info.csv

### Sars-Cov-2 specific analysis
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/virus_Sars-Cov-2_specific/README.md

### Viral phylodaynamic analysis
Detailed usage see: https://github.com/Channing-Zeng/metagenomics-nf/tree/master/virus-phylodaynamic/README.md

# Running NextFlow with AWS and Docker
To run your pipeline on cloud with unlimited resource:
i) First, you need a AWS account

ii) Then, you need to setup your nextflow.config file.

iii) If you want use Docker to run these pipelines, you also need to have Docker installed.


For more detail, see:

https://www.nextflow.io/docs/latest/index.html

