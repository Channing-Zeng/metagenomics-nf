# Maximum Likelihood Amplicon Pipeline: An amplicon (PCR / 16S) microbiome pipeline.

## Quick Start
>The following commands presumes you have nextflow installed as above along with the `~/.nextflow/config` file set up as described above.
Alternatively, you can use "-C" flag to assign your nextflow config file.


Usage:

nextflow run Channing-Zeng/metagenomics-nf/16S-rRNA/16S-nf  <ARGUMENTS>

Arguments:
  --manifest: the csv file telling us where to find files
  --repo_fasta: A fasta file of 16S rRNA genes
  --repo_si: A CSV file linking the 16S rRNA gene IDs in the fasta file with the NCBI taxonomy.
  --email: a valid email address to use with NCBI


Options:
  --short_reads        Sample sheet contains short read data (`short_R1` and `short_R2`)
  --long_reads         Sample sheet contains long read data (`long_reads`)
  --min_fasta_length   Minimum contig length (default: 100)
  --help


## Example
nextflow \
    -C nextflow.config \
    run Channing-Zeng/metagenomics-nf/16S-rRNA/16S-nf \
    --manifest manifest.csv \
    --output my_result \
    --email example@email.com \
    --repo_fasta test.repo.fasta \
    --repo_si test.repo.seq_info.csv


##iput data
### Manifest File
Minimal manifest CSV file contain three columns: specimen, R1, R2

See example manifest CSV file: "manifest.csv", or "manifest-minimal.csv"



## Output
There are four subdirectories in the output:
```
output-example/
├── classify
├── placement
├── refpkg
└── sv
```

### `sv` for sequence variants
```
output-example/sv/
├── dada2.combined.seqtabs.nochimera.csv
├── dada2.combined.seqtabs.nochimera.rds
├── dada2.specimen.sv.long.csv
├── dada2.sv.fasta
├── dada2.sv.map.csv
├── dada2.sv.shared.txt
├── dada2.sv.weights.csv
├── errM
│   ├── m22_p4
│   │   ├── m22_p4.R1.errM.csv
│   │   ├── m22_p4.R1.errM.rds
│   │   ├── m22_p4.R2.errM.csv
│   │   └── m22_p4.R2.errM.rds
│   ├── m23_p3
│   │   ├── m23_p3.R1.errM.csv
│   │   ├── m23_p3.R1.errM.rds
│   │   ├── m23_p3.R2.errM.csv
│   │   └── m23_p3.R2.errM.rds
│   └── m48_p4
│       ├── m48_p4.R1.errM.csv
│       ├── m48_p4.R1.errM.rds
│       ├── m48_p4.R2.errM.csv
│       └── m48_p4.R2.errM.rds
└── failed_specimens.csv
```
Some highlights here:
- `dada2.sv.fasta` contains the sequence variants in FASTA format.
- `dada2.specimen.sv.long.csv` contains the SV count by community in long format (i.e. a CSV file with columns community, sv, and count).
- `dada2.sv.shared.txt` contains the SV counts in a TSV format similar to `mothur` sharefile. 
- `failed_specimens.csv` contains all of the specimens that failed at some point (files empty, none survive filter-trim, merging, etc). The reason is listed as well. This is useful for troubleshooting.
- The `errM` subdirectory contains the error models for each batch. 
> By default, ignoring failed specimens and finish with as many specimens as possible.

### `refpkg` for the reference package
```
output-example/refpkg/
└── refpkg.tgz
```
A reference package is used for placement, and stored in tar-gzip format. Within the tar-gzip file is:
```
drwxr-xr-x  0 root   root        0 Sep 12 14:57 ./
-rw-r--r--  0 root   root     2217 Sep 12 14:57 ./CONTENTS.json
-rw-r--r--  0 root   root      381 Sep 12 14:57 ./phylo_modeldqujt6x8.json
-rw-r--r--  0 root   root     7402 Sep 12 14:57 ./RAxML_bestTree.refpkg
-rw-r--r--  0 root   root     2239 Sep 12 14:57 ./RAxML_info.refpkg
-rw-r--r--  0 root   root   207936 Sep 12 14:57 ./recruits.aln.fasta
-rw-r--r--  0 root   root   252268 Sep 12 14:57 ./recruits.aln.sto
-rw-r--r--  0 root   root  1012905 Sep 12 14:57 ./refpkg.cm
-rw-r--r--  0 root   root    28026 Sep 12 14:57 ./refpkg.seq_info.corr.csv
-rw-r--r--  0 root   root    27359 Sep 12 14:57 ./refpkg.taxtable.csv
-rw-r--r--  0 root   root     4340 Sep 12 14:57 ./treejkkusc5k.tre
```
- `CONTENTS.json` a manifest.
- `RAxML_bestTree.refpkg` a tree in newick format.
- `recruits.aln.fasta` an alignment of the full-length 16s rRNA gene recruits (FASTA format).
- `recruits.aln.sto` an alignment of the full-length 16s rRNA gene recruits (Stockholm format).
- `refpkg.cm` the covariance matrix used for the alignment.
- `refpkg.seq_info.corr.csv` A sequence information file telling us about the full length rRNA genes (inlcuding their taxonomic assignment)
- `refpkg.taxtable.csv` a mothur-style table of taxonomic information for each full-length 16s rRNA gene in the reference.

### . `placement` for the phylogenetic placement of sequence variants

```
output-example/placement/
├── adcl.csv.gz
├── alpha_diversity.csv.gz
├── dedup.jplace
├── edpl.csv.gz
├── kr_distance.csv.gz
├── pca
│   ├── epca.proj
│   ├── epca.trans
│   ├── epca.xml
│   ├── lpca.proj
│   ├── lpca.trans
│   └── lpca.xml
└── redup.jplace.gz
```
- `dedup.jplace` is the deduplicated placement file in JSON format.
- `redup.jplace.gz` is the reduplicated placement file.
- `alpha_diversity.csv.gz` has alpha diversity information for each community.
- `kr_distance.csv.gz` has the weighted pairwise phylogenetic distance between communities in long format.
- The `pca\` subdirectory has the PCA coordinates for each community.
- `adcl.csv.gz` and `edpl.csv.gz` contains information about each sequence variant's placement (Average distance to the closest leaf and pendant length respectively). High ADCL for a SV is indicative of poor representation in the reference package.

### `classify` for the taxonomic classifications of sequence variants and for each specimen / community
```
output-example/classify/
├── classify.mcc.db
└── tables
    ├── by_specimen.class.csv
    ├── by_specimen.family.csv
    ├── by_specimen.genus.csv
    ├── by_specimen.order.csv
    ├── by_specimen.phylum.csv
    ├── by_specimen.species.csv
    ├── by_taxon.class.csv
    ├── by_taxon.family.csv
    ├── by_taxon.genus.csv
    ├── by_taxon.order.csv
    ├── by_taxon.phylum.csv
    ├── by_taxon.species.csv
    ├── tallies_wide.class.csv
    ├── tallies_wide.family.csv
    ├── tallies_wide.genus.csv
    ├── tallies_wide.order.csv
    ├── tallies_wide.phylum.csv
    └── tallies_wide.species.csv
```
- `classify.mcc.db` contains all of the classification information in a sqlite3 database. The most important tables are `multiclass` and `multiclass_concat`. The documentation for `pplacer` contains further information.
- the `tables/` subdirectory contains by-community and by target-rank classification information. 
- `tables/tallies_wide.*` contains the by-community classified output in wide format.
- `tables/by_specimen.*` contains the by-community taxon counts and fractional abundance in long format. 
