# nf-core/sarek: Usage <!-- omit in toc -->

- [Running the pipeline](#running-the-pipeline)
  - [Updating the pipeline](#updating-the-pipeline)
  - [Reproducibility](#reproducibility)
- [Core Nextflow arguments](#core-nextflow-arguments)
  - [-profile](#-profile)
  - [-resume](#-resume)
  - [-c](#-c)
    - [Custom resource requests](#custom-resource-requests)
  - [Running in the background](#running-in-the-background)
    - [Nextflow memory requirements](#nextflow-memory-requirements)
- [Pipeline specific arguments](#pipeline-specific-arguments)
  - [--step](#--step)
  - [--input](#--input)
    - [--input &lt;FASTQ&gt; --step mapping](#--input-fastq---step-mapping)
    - [--input &lt;uBAM&gt; --step mapping](#--input-ubam---step-mapping)
    - [--input &lt;sample/&gt; --step mapping](#--input-sample---step-mapping)
    - [--input &lt;TSV&gt; --step prepare_recalibration](#--input-tsv---step-prepare_recalibration)
    - [--input &lt;TSV&gt; --step prepare_recalibration --skip_markduplicates](#--input-tsv---step-prepare_recalibration---skip_markduplicates)
    - [--input &lt;TSV&gt; --step recalibrate](#--input-tsv---step-recalibrate)
    - [--input &lt;TSV&gt; --step recalibrate --skip_markduplicates](#--input-tsv---step-recalibrate---skip_markduplicates)
    - [--input &lt;TSV&gt; --step variant_calling](#--input-tsv---step-variant_calling)
    - [--input &lt;TSV&gt; --step Control-FREEC](#--input-tsv---step-control-freec)
    - [--input &lt;VCF&gt; --step annotate](#--input-vcf---step-annotate)
  - [--help](#--help)
  - [--no_intervals](#--no_intervals)
  - [--nucleotides_per_second](#--nucleotides_per_second)
  - [--sentieon](#--sentieon)
    - [Alignment](#alignment)
    - [Germline SNV/INDEL Variant Calling - DNAseq](#germline-snvindel-variant-calling---dnaseq)
    - [Germline SNV/INDEL Variant Calling - DNAscope](#germline-snvindel-variant-calling---dnascope)
    - [Somatic SNV/INDEL Variant Calling - TNscope](#somatic-snvindel-variant-calling---tnscope)
    - [Structural Variant Calling](#structural-variant-calling)
  - [--skip_qc](#--skip_qc)
  - [--target_bed](#--target_bed)
  - [--tools for Variant Calling](#--tools-for-variant-calling)
    - [Germline variant calling](#germline-variant-calling)
    - [Somatic variant calling with tumor - normal pairs](#somatic-variant-calling-with-tumor---normal-pairs)
    - [Somatic variant calling with tumor only samples](#somatic-variant-calling-with-tumor-only-samples)
  - [--tools --sentieon](#--tools---sentieon)
  - [--tools for Annotation](#--tools-for-annotation)
    - [Annotation tools](#annotation-tools)
    - [Using genome specific containers](#using-genome-specific-containers)
    - [Download cache](#download-cache)
    - [Using downloaded cache](#using-downloaded-cache)
    - [Using VEP CADD plugin](#using-vep-cadd-plugin)
    - [Downloading CADD files](#downloading-cadd-files)
    - [Using VEP GeneSplicer plugin](#using-vep-genesplicer-plugin)
- [Modify fastqs (trim/split)](#modify-fastqs-trimsplit)
  - [--trim_fastq](#--trim_fastq)
  - [--clip_r1](#--clip_r1)
  - [--clip_r2](#--clip_r2)
  - [--three_prime_clip_r1](#--three_prime_clip_r1)
  - [--three_prime_clip_r2](#--three_prime_clip_r2)
  - [--trim_nextseq](#--trim_nextseq)
  - [--save_trimmed](#--save_trimmed)
  - [--split_fastq](#--split_fastq)
- [Preprocessing](#preprocessing)
  - [--aligner](#--aligner)
  - [--markdup_java_options](#--markdup_java_options)
  - [--no_gatk_spark](#--no_gatk_spark)
  - [--save_bam_mapped](#--save_bam_mapped)
  - [--skip_markduplicates](#--skip_markduplicates)
- [Variant Calling](#variant-calling)
  - [--ascat_ploidy](#--ascat_ploidy)
  - [--ascat_purity](#--ascat_purity)
  - [--cf_coeff](#--cf_coeff)
  - [--cf_ploidy](#--cf_ploidy)
  - [--cf_window](#--cf_window)
  - [--no_gvcf](#--no_gvcf)
  - [--no_strelka_bp](#--no_strelka_bp)
  - [--pon](#--pon)
  - [--pon_index](#--pon_index)
  - [--ignore_soft_clipped_bases](#--ignore_soft_clipped_bases)
  - [--umi](#--umi)
  - [--read_structure1](#--read_structure1)
  - [--read_structure2](#--read_structure2)
- [Annotation](#annotation)
  - [--annotate_tools](#--annotate_tools)
  - [--annotation_cache](#--annotation_cache)
  - [--snpeff_cache](#--snpeff_cache)
  - [--vep_cache](#--vep_cache)
  - [--cadd_cache](#--cadd_cache)
  - [--cadd_indels](#--cadd_indels)
  - [--cadd_indels_tbi](#--cadd_indels_tbi)
  - [--cadd_wg_snvs](#--cadd_wg_snvs)
  - [--cadd_wg_snvs_tbi](#--cadd_wg_snvs_tbi)
  - [--genesplicer](#--genesplicer)
- [Reference genomes](#reference-genomes)
  - [--genome (using iGenomes)](#--genome-using-igenomes)
  - [--igenomes_base](#--igenomes_base)
  - [--igenomes_ignore](#--igenomes_ignore)
  - [--genomes_base](#--genomes_base)
  - [--save_reference](#--save_reference)
  - [--ac_loci](#--ac_loci)
  - [--ac_loci_gc](#--ac_loci_gc)
  - [--bwa](#--bwa)
  - [--chr_dir](#--chr_dir)
  - [--chr_length](#--chr_length)
  - [--dbsnp](#--dbsnp)
  - [--dbsnp_index](#--dbsnp_index)
  - [--dict](#--dict)
  - [--fasta](#--fasta)
  - [--fasta_fai](#--fasta_fai)
  - [--germline_resource](#--germline_resource)
  - [--germline_resource_index](#--germline_resource_index)
  - [--intervals](#--intervals)
  - [--known_indels](#--known_indels)
  - [--known_indels_index](#--known_indels_index)
  - [--mappability](#--mappability)
  - [--snpeff_db](#--snpeff_db)
  - [--species](#--species)
  - [--vep_cache_version](#--vep_cache_version)
- [Other command line parameters](#other-command-line-parameters)
  - [--outdir](#--outdir)
  - [--publish_dir_mode](#--publish_dir_mode)
  - [--sequencing_center](#--sequencing_center)
  - [--multiqc_config](#--multiqc_config)
  - [--monochrome_logs](#--monochrome_logs)
  - [--email](#--email)
  - [--email_on_fail](#--email_on_fail)
  - [--plaintext_email](#--plaintext_email)
  - [--max_multiqc_email_size](#--max_multiqc_email_size)
  - [-name](#-name)
  - [--custom_config_version](#--custom_config_version)
  - [--custom_config_base](#--custom_config_base)
- [Job resources](#job-resources)
  - [Automatic resubmission](#automatic-resubmission)
  - [--max_memory](#--max_memory)
  - [--max_time](#--max_time)
  - [--max_cpus](#--max_cpus)
  - [--single_cpu_mem](#--single_cpu_mem)
- [Containers](#containers)
  - [Building your owns](#building-your-owns)
    - [Build with Conda](#build-with-conda)
    - [Build with Docker](#build-with-docker)
    - [Pull with Docker](#pull-with-docker)
    - [Pull with Singularity](#pull-with-singularity)
- [AWSBatch specific parameters](#awsbatch-specific-parameters)
  - [--awsqueue](#--awsqueue)
  - [--awsregion](#--awsregion)
  - [--awscli](#--awscli)
- [Troubleshooting](#troubleshooting)
  - [Spark related issues](#spark)

## Running the pipeline

The typical command for running the pipeline is as follows:

```bash
nextflow run nf-core/sarek --input <sample.tsv> -profile docker
```

This will launch the pipeline with the `docker` configuration profile.
See below for more information about profiles.

Note that the pipeline will create the following files in your working directory:

```bash
work            # Directory containing the nextflow working files
results         # Finished results (configurable, see below)
.nextflow_log   # Log file from Nextflow
# Other nextflow hidden files, eg. history of pipeline runs and old logs.
```

The nf-core/sarek pipeline comes with more documentation about running the pipeline, found in the `docs/` directory:

- [Output and how to interpret the results](output.md)

### Updating the pipeline

When you run the above command, `Nextflow` automatically pulls the pipeline code from `GitHub` and stores it as a cached version.
When running the pipeline after this, it will always use the cached version if available - even if the pipeline has been updated since.
To make sure that you're running the latest version of the pipeline, make sure that you regularly update the cached version of the pipeline:

```bash
nextflow pull nf-core/sarek
```

### Reproducibility

It's a good idea to specify a pipeline version when running the pipeline on your data.
This ensures that a specific version of the pipeline code and software are used when you run your pipeline.
If you keep using the same tag, you'll be running the same version of the pipeline, even if there have been changes to the code since.

First, go to the [nf-core/sarek releases page](https://github.com/nf-core/sarek/releases) and find the latest version number - numeric only (eg. `2.6.1`).
Then specify this when running the pipeline with `-r` (one hyphen) - eg. `-r 2.6.1`.

This version number will be logged in reports when you run the pipeline, so that you'll know what you used when you look back in the future.

## Core Nextflow arguments

> **NB:** These options are part of `Nextflow` and use a _single_ hyphen (pipeline parameters use a double-hyphen).

### -profile

Use this parameter to choose a configuration profile.
Profiles can give configuration presets for different compute environments.

Several generic profiles are bundled with the pipeline which instruct the pipeline to use software packaged using different methods (`Docker`, `Singularity`, `Conda`) - see below.

> We highly recommend the use of `Docker` or `Singularity` containers for full pipeline reproducibility, however when this is not possible, `Conda` is also supported.

The pipeline also dynamically loads configurations from [github.com/nf-core/configs](https://github.com/nf-core/configs) when it runs, making multiple config profiles for various institutional clusters available at run time.
For more information and to see if your system is available in these configs please see the [nf-core/configs documentation](https://github.com/nf-core/configs#documentation).

Note that multiple profiles can be loaded, for example: `-profile test,docker` - the order of arguments is important!
They are loaded in sequence, so later profiles can overwrite earlier profiles.

If `-profile` is not specified, the pipeline will run locally and expect all software to be installed and available on the `PATH`.
This is _not_ recommended.

- `docker`
  - A generic configuration profile to be used with [Docker](http://docker.com/)
  - Pulls software from DockerHub: [`nfcore/sarek`](http://hub.docker.com/r/nfcore/sarek/)
- `singularity`
  - A generic configuration profile to be used with [Singularity](https://sylabs.io/docs/)
  - Pulls software from DockerHub: [`nfcore/sarek`](http://hub.docker.com/r/nfcore/sarek/)
- `conda`
  - Please only use `Conda` as a last resort i.e. when it's not possible to run the pipeline with `Docker` or `Singularity`.
  - A generic configuration profile to be used with [conda](https://conda.io/docs/)
  - Pulls most software from [Bioconda](https://bioconda.github.io/)
- `test`
  - A profile with a complete configuration for automated testing
  - Includes links to test data so needs no other parameters
- `test_annotation`
  - A profile with a complete configuration for automated testing
  - Input data is a `VCF` for testing annotation
- `test_no_gatk_spark`
  - A profile with a complete configuration for automated testing
  - Specify `--no_gatk_spark`
- `test_split_fastq`
  - A profile with a complete configuration for automated testing
  - Specify `--split_fastq 500`
- `test_targeted`
  - A profile with a complete configuration for automated testing
  - Include link to a target `BED` file and use `Manta` and `Strelka` for Variant Calling
- `test_tool`
  - A profile with a complete configuration for automated testing
  - Test directly Variant Calling with a specific TSV file and `--step variantcalling`
- `test_trimming`
  - A profile with a complete configuration for automated testing
  - Test trimming options
- `test_umi_qiaseq`
  - A profile with a complete configuration for automated testing
  - Test a specific `UMI` structure
- `test_umi_tso`
  - A profile with a complete configuration for automated testing
  - Test a specific `UMI` structure

### -resume

Specify this when restarting a pipeline.
`Nextflow` will used cached results from any pipeline steps where the inputs are the same, continuing from where it got to previously.

You can also supply a run name or a session ID to resume a specific run: `-resume [run-name/session id]`.
Use the `nextflow log` command to show previous run names and session IDs.

### -c

Specify the path to a specific config file (this is a core `Nextflow` command).
See the [nf-core website documentation](https://nf-co.re/usage/configuration) for more information.

#### Custom resource requests

Each step in the pipeline has a default set of requirements for number of CPUs, memory and time.
For most of the steps in the pipeline, if the job exits with an error code of `143` (exceeded requested resources), it will automatically resubmit with higher requests (2 x original, then 3 x original).
If it still fails after three times then the pipeline is stopped.

Whilst these default requirements will hopefully work for most people with most data, you may find that you want to customise the compute resources that the pipeline requests.
You can do this by creating a custom config file.
For example, to give the workflow process `VEP` 32GB of memory, you could use the following config:

```nextflow
process {
  withName: VEP {
    memory = 32.GB
  }
}
```

See the main [Nextflow documentation](https://www.nextflow.io/docs/latest/config.html) for more information.

If you are likely to be running `nf-core` pipelines regularly it may be a good idea to request that your custom config file is uploaded to the `nf-core/configs` git repository.
Before you do this please can you test that the config file works with your pipeline of choice using the `-c` parameter see [-c section](#-c).
You can then create a pull request to the `nf-core/configs` repository with the addition of your config file, associated documentation file (see examples in [`nf-core/configs/docs`](https://github.com/nf-core/configs/tree/master/docs)), and amending [`nfcore_custom.config`](https://github.com/nf-core/configs/blob/master/nfcore_custom.config) to include your custom profile.

If you have any questions or issues please send us a message on [Slack](https://nf-co.re/join/slack) on the [`#configs` channel](https://nfcore.slack.com/channels/configs).

### Running in the background

`Nextflow` handles job submissions and supervises the running jobs.
The `Nextflow` process must run until the pipeline is finished.

The `Nextflow` `-bg` flag launches Nextflow in the background, detached from your terminal so that the workflow does not stop if you log out of your session. The logs are saved to a file.

Alternatively, you can use `screen` / `tmux` or similar tool to create a detached session which you can log back into at a later time.
Some HPC setups also allow you to run nextflow within a cluster job submitted your job scheduler (from where it submits more jobs).

#### Nextflow memory requirements

In some cases, the `Nextflow` Java virtual machines can start to request a large amount of memory.
We recommend adding the following line to your environment to limit this (typically in `~/.bashrc` or `~./bash_profile`):

```bash
NXF_OPTS='-Xms1g -Xmx4g'
```

## Pipeline specific arguments

### --step

> **NB** only one step must be specified

Use this to specify the starting step

Default: `mapping`

Available: `mapping`, `prepare_recalibration`, `recalibrate`, `variant_calling`, `annotate`, `Control-FREEC`

> **NB** step can be specified with no concern for case, or the presence of `-` or `_`

### --input

Use this to specify the location of your input `TSV` (Tab Separated Values) file.

> **NB** Delimiter is the tab (`\t`) character, and no header is required

There are different kinds of `TSV` files that can be used as input, depending on the input files available (`FASTQ`, `unmapped BAM`, `recalibrated BAM`...).
The `TSV` file should correspond to the correct step, see [`--step`](#--step) for more information.
For all possible `TSV` files, described in the next sections, here is an explanation of what the columns refer to:

`Sarek` auto-generates `TSV` files for all and for each individual samples, depending of the options specified.

- `subject` designates the subject, it should be the ID of the subject, and it must be unique for each subject, but one subject can have multiple samples (e.g.
normal and tumor)
- `sex` are the sex chromosomes of the subject, (ie `XX`, `XY`...)
- `status` is the status of the measured sample, (`0` for Normal or `1` for Tumor)
- `sample` designates the sample, it should be the ID of the sample (it is possible to have more than one tumor sample for each subject, i.e.
a tumor and a relapse), it must be unique, but samples can have multiple lanes (which will later be merged)
- `lane` is used when the sample is multiplexed on several lanes, it must be unique for each lane in the same sample (but does not need to be the original lane name), and must contain at least one character
- `fastq1` is the path to the first pair of the `FASTQ` file
- `fastq2` is the path to the second pair of the `FASTQ` file
- `bam` is the path to the `BAM` file
- `bai` is the path to the `BAM` index file
- `recaltable` is the path to the recalibration table
- `mpileup` is the path to the mpileup file

It is recommended to add the absolute path of the files, but relative path should also work.

If necessary, a tumor sample can be associated to a normal sample as a pair, if specified with the same `subject`and a different `sample`.
An additional tumor sample (such as a relapse for example), can be added if specified with the same `subject` and a different `sample`.

`Sarek` will output results in a different directory for each sample.
If multiple samples are specified in the `TSV` file, `Sarek` will consider all files to be from different samples.
Multiple `TSV` files can be specified if the path is enclosed in quotes.

Output from Variant Calling and/or Annotation will be in a specific directory for each sample (or normal/tumor pair if applicable).

#### --input &lt;FASTQ&gt; --step mapping

The `TSV` file to start with the step mapping with paired-end `FASTQs` should contain the columns:

`subject sex status sample lane fastq1 fastq2`

In this example (`example_fastq.tsv`), there are 3 read groups.

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID|1|/samples/normal1_1.fastq.gz|/samples/normal1_2.fastq.gz|
|SUBJECT_ID|XX|0|SAMPLE_ID|2|/samples/normal2_1.fastq.gz|/samples/normal2_2.fastq.gz|
|SUBJECT_ID|XX|0|SAMPLE_ID|3|/samples/normal3_1.fastq.gz|/samples/normal3_2.fastq.gz|

```bash
--input example_fastq.tsv
```

Or, for a normal/tumor pair:

In this example (`example_pair_fastq.tsv`), there are 3 read groups for the normal sample and 2 for the tumor sample.

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|1|/samples/normal1_1.fastq.gz|/samples/normal1_2.fastq.gz|
|SUBJECT_ID|XX|0|SAMPLE_ID1|2|/samples/normal2_1.fastq.gz|/samples/normal2_2.fastq.gz|
|SUBJECT_ID|XX|0|SAMPLE_ID1|3|/samples/normal3_1.fastq.gz|/samples/normal3_2.fastq.gz|
|SUBJECT_ID|XX|1|SAMPLE_ID2|1|/samples/tumor1_1.fastq.gz|/samples/tumor1_2.fastq.gz|
|SUBJECT_ID|XX|1|SAMPLE_ID2|2|/samples/tumor2_1.fastq.gz|/samples/tumor2_2.fastq.gz|

```bash
--input example_pair_fastq.tsv
```

#### --input &lt;uBAM&gt; --step mapping

The `TSV` file for starting the mapping from `unmapped BAM` files should contain the columns:

- `subject sex status sample lane bam`

In this example (`example_ubam.tsv`), there are 3 read groups.

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID|1|/samples/normal_1.bam|
|SUBJECT_ID|XX|0|SAMPLE_ID|2|/samples/normal_2.bam|
|SUBJECT_ID|XX|0|SAMPLE_ID|3|/samples/normal_3.bam|

```bash
--input example_ubam.tsv
```

Or, for a normal/tumor pair:

In this example (`example_pair_ubam.tsv`), there are 3 read groups for the normal sample and 2 for the tumor sample.

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|1|/samples/normal_1.bam|
|SUBJECT_ID|XX|0|SAMPLE_ID1|2|/samples/normal_2.bam|
|SUBJECT_ID|XX|0|SAMPLE_ID1|3|/samples/normal_3.bam|
|SUBJECT_ID|XX|1|SAMPLE_ID2|1|/samples/tumor_1.bam|
|SUBJECT_ID|XX|1|SAMPLE_ID2|2|/samples/tumor_2.bam|

```bash
--input example_pair_ubam.tsv
```

#### --input &lt;sample/&gt; --step mapping

Use this to specify the location to a directory with `FASTQ` files for the `mapping` step of a single germline sample only.
For example:

```bash
--input </path/to/directory>
```

> **NB** All of the found `FASTQ` files are considered to belong to the same sample.

The input folder, containing the `FASTQ` files for one subject (ID) should be organized into one sub-folder for every sample.
The given directory is searched recursively for `FASTQ` files that are named `*_R1_*.fastq.gz`, and a matching pair with the same name except `_R2_` instead of `_R1_` is expected to exist alongside.
All `FASTQ` files for that sample should be collected here.

```text
ID
+--sample1
+------sample1_<lib>_<flowcell-index>_lane1_R1_1000.fastq.gz
+------sample1_<lib>_<flowcell-index>_lane1_R2_1000.fastq.gz
+------sample1_<lib>_<flowcell-index>_lane2_R1_1000.fastq.gz
+------sample1_<lib>_<flowcell-index>_lane2_R2_1000.fastq.gz
+--sample2
+------sample2_<lib>_<flowcell-index>_lane1_R1_1000.fastq.gz
+------sample2_<lib>_<flowcell-index>_lane1_R2_1000.fastq.gz
+--sample3
+------sample3_<lib>_<flowcell-index>_lane1_R1_1000.fastq.gz
+------sample3_<lib>_<flowcell-index>_lane1_R2_1000.fastq.gz
+------sample3_<lib>_<flowcell-index>_lane2_R1_1000.fastq.gz
+------sample3_<lib>_<flowcell-index>_lane2_R2_1000.fastq.gz
```

`FASTQ` filename structure:

- `<sample>_<lib>_<flowcell-index>_<lane>_R1_<XXX>.fastq.gz` and
- `<sample>_<lib>_<flowcell-index>_<lane>_R2_<XXX>.fastq.gz`

Where:

- `sample` = sample id
- `lib` = identifier of library preparation
- `flowcell-index` = identifier of flow cell for the sequencing run
- `lane` = identifier of the lane of the sequencing run

Read group information will be parsed from `FASTQ` file names according to this:

- `RGID` = "sample_lib_flowcell_index_lane"
- `RGPL` = "Illumina"
- `PU` = sample
- `RGLB` = lib

Each `FASTQ` file pair gets its own read group (`@RG`) in the resulting `BAM` file in the following way.

- The sample name (`SM`) is derived from the the last component of the path given to `--input`.
That is, you should make sure that that directory has a meaningful name! For example, with `--input=/my/fastqs/sample123`, the sample name will be `sample123`.
- The read group id is set to *flowcell.samplename.lane*.
The flowcell id and lane number are auto-detected from the name of the first read in the `FASTQ` file.

#### --input &lt;TSV&gt; --step prepare_recalibration

To start from the preparation of the recalibration step (`--step prepare_recalibration`), a `TSV` file needs to be given as input containing the paths to the `non-recalibrated BAM` files.
The `Sarek`-generated `TSV` file is stored under `results/Preprocessing/TSV/duplicates_marked_no_table.tsv` and will automatically be used as an input when specifying the parameter `--step prepare_recalibration`.

The `TSV` contains the following columns:

- `subject sex status sample bam bai`

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID|/samples/normal.md.bam|/samples/normal.md.bai|

Or, for a normal/tumor pair:

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|/samples/normal.md.bam|/samples/normal.md.bai|
|SUBJECT_ID|XX|1|SAMPLE_ID2|/samples/tumor.md.bam|/samples/tumor.md.bai|

#### --input &lt;TSV&gt; --step prepare_recalibration --skip_markduplicates

The `Sarek`-generated `TSV` file is stored under `results/Preprocessing/TSV/mapped.tsv` and will automatically be used as an input when specifying the parameter `--step prepare_recalibration --skip_markduplicates`.
The `TSV` file contains the same columns, but the content is slightly different:

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID|/samples/normal.bam|/samples/normal.bai|

Or, for a normal/tumor pair:

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|/samples/normal.bam|/samples/normal.bai|
|SUBJECT_ID|XX|1|SAMPLE_ID2|/samples/tumor.bam|/samples/tumor.bai|

#### --input &lt;TSV&gt; --step recalibrate

To start from the recalibrate step (`--step recalibrate`), a `TSV` file needs to be given as input containing the paths to the `non-recalibrated BAM` file and the associated recalibration table.
The `Sarek`-generated `TSV` file is stored under `results/Preprocessing/TSV/duplicates_marked.tsv` and will automatically be used as an input when specifying the parameter `--step recalibrate`.

The `TSV` contains the following columns:

- `subject sex status sample bam bai recaltable`

| | | | | | | |
|-|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID|/samples/normal.md.bam|/samples/normal.md.bai|/samples/normal.recal.table|

Or, for a normal/tumor pair:

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|/samples/normal.md.bam|/samples/normal.md.bai|/samples/normal.recal.table|
|SUBJECT_ID|XX|1|SAMPLE_ID2|/samples/tumor.md.bam|/samples/tumor.md.bai|/samples/tumor.recal.table|

#### --input &lt;TSV&gt; --step recalibrate --skip_markduplicates

The `Sarek`-generated `TSV` file is stored under `results/Preprocessing/TSV/mapped_no_duplicates_marked.tsv` and will automatically be used as an input when specifying the parameter `--step recalibrate --skip_markduplicates`.
The `TSV` file contains the same columns, but the content is slightly different:

| | | | | | | |
|-|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID|/samples/normal.bam|/samples/normal.bai|/samples/normal.recal.table|

Or, for a normal/tumor pair:

| | | | | | | |
|-|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|/samples/normal.bam|/samples/normal.bai|/samples/normal.recal.table|
|SUBJECT_ID|XX|1|SAMPLE_ID2|/samples/tumor.bam|/samples/tumor.bai|/samples/tumor.recal.table|

#### --input &lt;TSV&gt; --step variant_calling

To start from the variant calling step (`--step variant_calling`), a `TSV` file needs to be given as input containing the paths to the `recalibrated BAM` file and the associated index.
The `Sarek`-generated `TSV` file is stored under `results/Preprocessing/TSV/recalibrated.tsv` and will automatically be used as an input when specifying the parameter `--step variant_calling`.

The `TSV` file should contain the columns:

- `subject sex status sample bam bai`

Here is an example for two samples from the same subject:

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID|/samples/normal.recal.bam|/samples/normal.recal.bai|

Or, for a normal/tumor pair:

| | | | | | |
|-|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|/samples/normal.recal.bam|/samples/normal.recal.bai|
|SUBJECT_ID|XX|1|SAMPLE_ID2|/samples/tumor.recal.bam|/samples/tumor.recal.bai|

#### --input &lt;TSV&gt; --step Control-FREEC

To start from the Control-FREEC step (`--step Control-FREEC`), a `TSV` file needs to be given as input containing the paths to the mpileup files.
The `Sarek`-generated `TSV` file is stored under `results/VariantCalling/TSV/control-freec_mpileup.tsv` and will automatically be used as an input when specifying the parameter `--step Control-FREEC`.

The `TSV` file should contain the columns:

- `subject sex status sample mpileup`

Here is an example for one normal/tumor pair from one subjects:

| | | | | |
|-|-|-|-|-|
|SUBJECT_ID|XX|0|SAMPLE_ID1|/samples/normal.pileup|
|SUBJECT_ID|XX|1|SAMPLE_ID2|/samples/tumor.pileup|

#### --input &lt;VCF&gt; --step annotate

Input files for Sarek can be specified using the path to a `VCF` file given to the `--input` command only with the annotation step (`--step annotate`).
As `Sarek` will use `bgzip` and `tabix` to compress and index `VCF` files annotated, it expects `VCF` files to be sorted.
Multiple `VCF` files can be specified, using a [glob path](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html#glob), if enclosed in quotes.
For example:

```bash
--step annotate --input "results/VariantCalling/*/{HaplotypeCaller,Manta,Mutect2,Strelka,TIDDIT}/*.vcf.gz"
```

### --help

Will display the help message.

### --no_intervals

Disable usage of [`intervals`](#--intervals) file.

### --nucleotides_per_second

Use this to estimate of how many seconds it will take to call variants on any interval, the default value is `1000` when not specified in the [`intervals`](#--intervals) file.

### --sentieon

[Sentieon](https://www.sentieon.com/) is a commercial solution to process genomics data with high computing efficiency, fast turnaround time, exceptional accuracy, and 100% consistency.

If [Sentieon](https://www.sentieon.com/) is available, use this `--sentieon` params to enable with `Sarek` to use some `Sentieon Analysis Pipelines & Tools`.
Adds the following tools for the [`--tools`](#--tools---sentieon) options: `DNAseq`, `DNAscope` and `TNscope`.

Please refer to the [nf-core/configs](https://github.com/nf-core/configs#adding-a-new-pipeline-specific-config) repository on how to make a pipeline-specific configuration file based on the [munin-sarek specific configuration file](https://github.com/nf-core/configs/blob/master/conf/pipeline/sarek/munin.config).

Or ask us on the [nf-core Slack](http://nf-co.re/join/slack) on the following channels: [#sarek](https://nfcore.slack.com/channels/sarek) or [#configs](https://nfcore.slack.com/channels/configs).

The following `Sentieon Analysis Pipelines & Tools` are available within `Sarek`:

#### Alignment

> Sentieon BWA matches BWA-MEM with > 2X speedup.

This tool is enabled by default within `Sarek` if `--sentieon` is specified and if the pipeline is started with the `mapping` [step](usage.md#--step).

#### Germline SNV/INDEL Variant Calling - DNAseq

> Precision FDA award-winning software.
> Matches GATK 3.3-4.1, and without down-sampling.
> Results up to 10x faster and 100% consistent every time.

This tool is enabled within `Sarek` if `--sentieon` is specified and if `--tools DNAseq` is specified cf [--tools --sentieon](#--tools--sentieon).

#### Germline SNV/INDEL Variant Calling - DNAscope

> Improved accuracy and genome characterization.
> Machine learning enhanced filtering producing top variant calling accuracy.

This tool is enabled within `Sarek` if `--sentieon` is specified and if `--tools DNAscope` is specified cf [--tools --sentieon](#--tools--sentieon).

#### Somatic SNV/INDEL Variant Calling - TNscope

> Winner of ICGC-TCGA DREAM challenge.
> Improved accuracy, machine learning enhanced filtering.
> Supports molecular barcodes and unique molecular identifiers.

This tool is enabled within `Sarek` if `--sentieon` is specified and if `--tools TNscope` is specified cf [--tools --sentieon](#--tools--sentieon).

#### Structural Variant Calling

> Germline and somatic SV calling, including translocations, inversions, duplications and large INDELs

This tool is enabled within `Sarek` if `--sentieon` is specified and if `--tools DNAscope` is specified cf [--tools --sentieon](#--tools--sentieon).

### --skip_qc

Use this to disable specific QC and Reporting tools.
Multiple tools can be specified, separated by commas.

Available: `all`, `bamQC`, `BaseRecalibrator`, `BCFtools`, `Documentation`, `FastQC`, `MarkDuplicates`, `MultiQC`, `samtools`, `vcftools`, `versions`

Default: `None`

> **NB** `--skip_qc MarkDuplicates` does not skip `MarkDuplicates` but prevent the collection of duplicate metrics that slows down performance

### --target_bed

Use this to specify the target `BED` file for targeted or whole exome sequencing.

The `--target_bed` parameter does _not_  imply that the workflow is running alignment or variant calling only for the supplied targets.
Instead, we are aligning for the whole genome, and selecting variants only at the very end by intersecting with the provided target file.
Adding every exon as an interval in case of `WES` can generate >200K processes or jobs, much more forks, and similar number of directories in the Nextflow work directory.
Furthermore, primers and/or baits are not 100% specific, (certainly not for MHC and KIR, etc.), quite likely there going to be reads mapping to multiple locations.
If you are certain that the target is unique for your genome (all the reads will certainly map to only one location), and aligning to the whole genome is an overkill, better to change the reference itself.

The recommended flow for targeted sequencing data is to use the workflow as it is, but also provide a `BED` file containing targets for all steps using the `--target_bed` option.
The workflow will pick up these intervals, and activate any `--exome` flag in any tools that allow it to process deeper coverage.
It is advised to pad the variant calling regions (exons or target) to some extent before submitting to the workflow.
To add the target `BED` file configure the command line like:

```bash
--target_bed <target.bed>
```

### --tools for Variant Calling

Use this parameter to specify the variant calling and annotation tools to be used.
Multiple tools can be specified, separated by commas.
For example:

```bash
--tools Strelka,mutect2,SnpEff
```

Available variant callers: `ASCAT`, `Control-FREEC`, `FreeBayes`, `HaplotypeCaller`, `Manta`, `mpileup`, `MSIsensor`, `Mutect2`, `Strelka`, `TIDDIT`.

> **NB** Tools can be specified with no concern for case

For more information on the individual variant callers, and where to find the variant calling results, check the [output](output.md) documentation.

> **WARNING** Not all variant callers are available for both germline and somatic variant calling.

For more information, please read the following documentation on [Germline variant calling](#germline-variant-calling), [Somatic variant calling with tumor - normal pairs](#somatic-variant-calling-with-tumor---normal-pairs) and [Somatic variant calling with tumor only samples](#somatic-variant-calling-with-tumor-only-samples)

#### Germline variant calling

Using `Sarek`, germline variant calling will always be performed if a variant calling tool with a germline mode is selected.
Germline variant calling can currently only be performed with the following variant callers:

- *FreeBayes*
- *HaplotypeCaller*
- *Manta*
- *mpileup*
- *Sentieon*
- *Strelka*
- *TIDDIT*

For more information on the individual variant callers, and where to find the variant calling results, check the [output](output.md) documentation.

#### Somatic variant calling with tumor - normal pairs

Using `Sarek`, somatic variant calling will be performed, if your input tsv file contains tumor / normal pairs (see [input](#--input) documentation for more information).
Different samples belonging to the same patient, where at least one is marked as normal (`0` in the `Status` column) and at least one is marked as tumor (`1` in the `Status` column) are treated as tumor / normal pairs.

If tumor-normal pairs are provided, both germline variant calling and somatic variant calling will be performed, provided that the selected variant caller allows for it.
If the selected variant caller allows only for somatic variant calling, then only somatic variant calling results will be generated.

Here is a list of the variant calling tools that support somatic variant calling:

- *ASCAT*
- *Control-FREEC*
- *FreeBayes*
- *Manta*
- *MSIsensor*
- *Mutect2*
- *Sentieon*
- *Strelka*

For more information on the individual variant callers, and where to find the variant calling results, check the [output](output.md) documentation.

#### Somatic variant calling with tumor only samples

Somatic variant calling with only tumor samples (no matching normal sample), is not recommended by the `GATK best practices`.
This is just supported for a limited variant callers.

Here is a list of the variant calling tools that support tumor-only somatic variant calling:

- *Manta*
- *mpileup*
- *Mutect2*
- *TIDDIT*

### --tools --sentieon

> **WARNING** Only with `--sentieon`

If [Sentieon](https://www.sentieon.com/) is available, use this `--sentieon` params to enable with `Sarek` to use some `Sentieon Analysis Pipelines & Tools`.
Adds the following tools for the [`--tools`](#--tools) options: `DNAseq`, `DNAscope` and `TNscope`.

### --tools for Annotation

Available annotation tools: `VEP`, `SnpEff`, `merge`.
For more details, please check the [annotation](#annotation-tools) documentation.

#### Annotation tools

With `Sarek`, annotation is done using `snpEff`, `VEP`, or even both consecutively:

- `--tools snpEff`
  - To annotate using `snpEff`
- `--tools VEP`
  - To annotate using `VEP`
- `--tools snpEff,VEP`
  - To annotate using `snpEff` and `VEP`
- `--tools merge`
  - To annotate using `snpEff` followed by `VEP`

`VCF` produced by `Sarek` will be annotated if `snpEff` or `VEP` are specified with the `--tools` command.
As Sarek will use `bgzip` and `tabix` to compress and index VCF files annotated, it expects VCF files to be sorted.

In these examples, all command lines will be launched starting with `--step annotate`.
It can of course be started directly from any other step instead.

#### Using genome specific containers

`Sarek` has already designed containers with `snpEff` and `VEP` files for Human (`GRCh37`, `GRCh38`), Mouse (`GRCm38`), Dog (`CanFam3.1`) and Roundworm (`WBcel235`).

Default settings will run using these containers.
The main `Sarek` container has also `snpEff` and `VEP` installed, but without the cache files that can be downloaded separately.
See [containers documentation](#containers) for more information.

#### Download cache

A `Nextflow` helper script has been designed to help downloading `snpEff` and `VEP` caches.
Such files are meant to be shared between multiple users, so this script is mainly meant for people administrating servers, clusters and advanced users.

```bash
nextflow run download_cache.nf --snpeff_cache </path/to/snpEff/cache> --snpeff_db <snpEff DB version> --genome <GENOME>
nextflow run download_cache.nf --vep_cache </path/to/VEP/cache> --species <species> --vep_cache_version <VEP cache version> --genome <GENOME>
```

#### Using downloaded cache

Both `snpEff` and `VEP` enable usage of cache.
If cache is available on the machine where `Sarek` is run, it is possible to run annotation using cache.
You need to specify the cache directory using `--snpeff_cache` and `--vep_cache` in the command lines or within configuration files.
The cache will only be used when `--annotation_cache` and cache directories are specified (either in command lines or in a configuration file).

Example:

```bash
nextflow run nf-core/sarek --tools snpEff --step annotate --sample <file.vcf.gz> --snpeff_cache </path/to/snpEff/cache> --annotation_cache
nextflow run nf-core/sarek --tools VEP --step annotate --sample <file.vcf.gz> --vep_cache </path/to/VEP/cache> --annotation_cache
```

#### Using VEP CADD plugin

To enable the use of the `VEP` `CADD` plugin:

- Download the `CADD` files
- Specify them (either on the command line, like in the example or in a configuration file)
- use the `--cadd_cache` flag

Example:

```bash
nextflow run nf-core/sarek --step annotate --tools VEP --sample <file.vcf.gz> --cadd_cache \
    --cadd_indels </path/to/CADD/cache/InDels.tsv.gz> \
    --cadd_indels_tbi </path/to/CADD/cache/InDels.tsv.gz.tbi> \
    --cadd_wg_snvs </path/to/CADD/cache/whole_genome_SNVs.tsv.gz> \
    --cadd_wg_snvs_tbi </path/to/CADD/cache/whole_genome_SNVs.tsv.gz.tbi>
```

#### Downloading CADD files

An helper script has been designed to help downloading `CADD` files.
Such files are meant to be share between multiple users, so this script is mainly meant for people administrating servers, clusters and advanced users.

```bash
nextflow run download_cache.nf --cadd_cache </path/to/CADD/cache> --cadd_version <CADD version> --genome <GENOME>
```

#### Using VEP GeneSplicer plugin

To enable the use of the `VEP` `GeneSplicer` plugin:

- use the `--genesplicer` flag

Example:

```bash
nextflow run nf-core/sarek --step annotate --tools VEP --sample <file.vcf.gz> --genesplicer
```

## Modify fastqs (trim/split)

### --trim_fastq

Use this to perform adapter trimming with [Trim Galore](https://github.com/FelixKrueger/TrimGalore/blob/master/Docs/Trim_Galore_User_Guide.md)

### --clip_r1

Instructs `Trim Galore` to remove a number of bp from the 5' end of read 1 (or single-end reads).
This may be useful if the qualities were very poor, or if there is some sort of unwanted bias at the 5' end.

### --clip_r2

Instructs `Trim Galore` to remove a number of bp from the 5' end of read 2 (paired-end reads only).
This may be useful if the qualities were very poor, or if there is some sort of unwanted bias at the 5' end.

### --three_prime_clip_r1

Instructs `Trim Galore` to remove a number of bp from the 3' end of read 1 (or single-end reads) AFTER adapter/quality trimming has been performed.
This may remove some unwanted bias from the 3' end that is not directly related to adapter sequence or basecall quality.

### --three_prime_clip_r2

Instructs `Trim Galore` to remove a number of bp from the 3' end of read 2 AFTER adapter/quality trimming has been performed.
This may remove some unwanted bias from the 3' end that is not directly related to adapter sequence or basecall quality.

### --trim_nextseq

This enables the option `--nextseq-trim=3'CUTOFF` within `Cutadapt`, which will set a quality cutoff (that is normally given with `-q` instead), but qualities of G bases are ignored.
This trimming is common for the `NextSeq` and `NovaSeq` platforms, where basecalls without any signal are called as high-quality G bases.

### --save_trimmed

Option to keep trimmed `FASTQs`

### --split_fastq

Use the `Nextflow` [`splitFastq`](https://www.nextflow.io/docs/latest/operator.html#splitfastq) operator to specify how many reads should be contained in the split fastq file.
For example:

```bash
--split_fastq 10000
```

## Preprocessing

### --aligner

To control which aligner is used for mapping the reads.

Available: `bwa-mem` and `bwa-mem2`

Default: `bwa-mem`

Example:

```bash
--aligner "bwa-mem"
```

> **WARNING** Current indices for `bwa` in AWS iGenomes are not compatible with `bwa-mem2`.
> Use `--bwa=false` to have `Sarek` build them automatically.
>
> **WARNING** BWA-mem2 is in active development
> Sarek might not be able to require the right amount of resources for it at the moment
> We recommend to use pre-built indexes

Example:

```bash
--aligner "bwa-mem2" --bwa=false
```

### --markdup_java_options

To control the java options necessary for the `GATK MarkDuplicates` process, you can set this parameter.

Default: "-Xms4000m -Xmx7g"
For example:

```bash
--markdup_java_options "-Xms4000m -Xmx7g"
```

### --no_gatk_spark

Use this to disable usage of `Spark` implementation of the `GATK` tools in local mode.

### --save_bam_mapped

Will save `mapped BAMs`.

### --skip_markduplicates

Will skip `GATK MarkDuplicates`.
This params will also save the `mapped BAMS`, to enable restart from step `prepare_recalibration`

## Variant Calling

### --ascat_ploidy

Use this parameter to overwrite default behavior from `ASCAT` regarding `ploidy`.
Requires that [`--ascat_purity`](#--ascat_purity) is set.

### --ascat_purity

Use this parameter to overwrite default behavior from `ASCAT` regarding `purity`.
Requires that [`--ascat_ploidy`](#--ascat_ploidy) is set.

### --cf_coeff

Use this parameter to overwrite default behavior from `Control-FREEC` regarding `coefficientOfVariation`

Default: `0.05`

### --cf_ploidy

Use this parameter to overwrite default behavior from `Control-FREEC` regarding `ploidy`

Default: `2`

### --cf_window

Use this parameter to overwrite default behavior from `Control-FREEC` regarding `window size`
It is recommended to use a window size of 0 for exome data.

Default: Disabled

### --no_gvcf

Use this to disable g.vcf output from `GATK HaplotypeCaller`.

### --no_strelka_bp

Use this not to use `Manta` `candidateSmallIndels` for `Strelka` (not recommended by Broad Institute's Best Practices).

### --pon

When a [panel of normals (PON)](https://gatk.broadinstitute.org/hc/en-us/articles/360035890631-Panel-of-Normals-PON) is defined, it will be use to filter somatic calls.
Without `PON`, there will be no calls with `PASS` in the `INFO` field, only an _unfiltered_ `VCF` is written.
It is recommended to make your own `PON`, as it depends on sequencer and library preparation.
For tests in `iGenomes` there is a dummy `PON` file in the Annotation/GermlineResource directory, but it _should not be used_ as a real panel-of-normals file.
Provide your `PON` with:

```bash
--pon </path/to/PON.vcf.gz>
```

`PON` file should be bgzipped.

### --pon_index

Tabix index of the `PON` bgzipped VCF file.
If none provided, will be generated automatically from the `PON` bgzipped VCF file.

### --ignore_soft_clipped_bases

Do not analyze soft clipped bases in the reads for `GATK Mutect2` with the `--dont-use-soft-clipped-bases` params.

### --umi

If provided, `Unique Molecular Identifiers (UMIs)` steps will be run to extract and annotate the reads with `UMIs` and create consensus reads.
This part of the pipeline uses [fgbio](https://github.com/fulcrumgenomics/fgbio) to convert the `FASTQ` files into a `unmapped BAM`, where reads are tagged with the `UMIs` extracted from the `FASTQ` sequences.
In order to allow the correct tagging, the `UMI` sequence must be contained in the read sequence itself, and not in the `FASTQ` filename.
Following this step, the `unmapped BAM` is aligned and reads are then grouped based on mapping position and `UMI` tag.
Finally, reads in the same groups are collapsed to create a consensus read.
To create consensus, we have chosen to use the *adjacency method* [ref](https://cgatoxford.wordpress.com/2015/08/14/unique-molecular-identifiers-the-problem-the-solution-and-the-proof/).
In order for the correct tagging to be performed, a read structure needs to be  specified as indicated below.

### --read_structure1

When processing `UMIs`, a read structure should always be provided for each of the `FASTQ` files, to allow the correct annotation of the `BAM` file.
If the read does not contain any `UMI`, the structure will be +T (i.e. only template of any length).
The read structure follows a format adopted by different tools, and described [here](https://github.com/fulcrumgenomics/fgbio/wiki/Read-Structures)

### --read_structure2

When processing `UMIs`, a read structure should always be provided for each of the `FASTQ` files, to allow the correct annotation of the `BAM` file.
If the read does not contain any UMI, the structure will be +T (i.e. only template of any length).
The read structure follows a format adopted by different tools, and described [here](https://github.com/fulcrumgenomics/fgbio/wiki/Read-Structures)

## Annotation

### --annotate_tools

Specify from which tools `Sarek` should look for `VCF` files to annotate, only for step `Annotate`.

Available: `HaplotypeCaller`, `Manta`, `Mutect2`, `Strelka`, `TIDDIT`

Default: `None`

### --annotation_cache

Enable usage of annotation cache, and disable usage of already built containers within `Sarek`.
For more information, follow the [downloaded cache guidelines](#using-downloaded-cache).

### --snpeff_cache

To be used conjointly with [`--annotation_cache`](#--annotation_cache), specify the cache `snpEff` directory:

```bash
--snpeff_cache </path/to/snpeff_cache>
```

### --vep_cache

To be used conjointly with [`--annotation_cache`](#--annotation_cache), specify the cache `VEP` directory:

```bash
--vep_cache </path/to/vep_cache>
```

### --cadd_cache

Enable `CADD` cache.

### --cadd_indels

Path to `CADD InDels` file.

### --cadd_indels_tbi

Path to `CADD InDels` index.

### --cadd_wg_snvs

Path to `CADD SNVs` file.

### --cadd_wg_snvs_tbi

Path to `CADD SNVs` index.

### --genesplicer

Enable `genesplicer` within `VEP`.

## Reference genomes

The pipeline config files come bundled with paths to the `Illumina iGenomes` reference index files.
The configuration is set up to use the [AWS-iGenomes](https://ewels.github.io/AWS-iGenomes/) resource.

### --genome (using iGenomes)

Sarek is using [AWS iGenomes](https://ewels.github.io/AWS-iGenomes/), which facilitate storing and sharing references.
To run the pipeline, you must specify which to use with the `--genome` flag.

You can find the keys to specify the genomes in the [iGenomes config file](../conf/igenomes.config)).
Genomes that are supported are:

- Homo sapiens
  - `--genome GRCh37` (GATK Bundle)
  - `--genome GRCh38` (GATK Bundle)

- Mus musculus
  - `--genome GRCm38` (Ensembl)

Limited support for:

- Arabidopsis thaliana
  - `--genome TAIR10` (Ensembl)

- Bacillus subtilis 168
  - `--genome EB2` (Ensembl)

- Bos taurus
  - `--genome UMD3.1` (Ensembl)
  - `--genome bosTau8` (UCSC)

- Caenorhabditis elegans
  - `--genome WBcel235` (Ensembl)
  - `--genome ce10` (UCSC)

- Canis familiaris
  - `--genome CanFam3.1` (Ensembl)
  - `--genome canFam3` (UCSC)

- Danio rerio
  - `--genome GRCz10` (Ensembl)
  - `--genome danRer10` (UCSC)

- Drosophila melanogaster
  - `--genome BDGP6` (Ensembl)
  - `--genome dm6` (UCSC)

- Equus caballus
  - `--genome EquCab2` (Ensembl)
  - `--genome equCab2` (UCSC)

- Escherichia coli K 12 DH10B
  - `--genome EB1` (Ensembl)

- Gallus gallus
  - `--genome Galgal4` (Ensembl)
  - `--genome galgal4` (UCSC)

- Glycine max
  - `--genome Gm01` (Ensembl)

- Homo sapiens
  - `--genome hg19` (UCSC)
  - `--genome hg38` (UCSC)

- Macaca mulatta
  - `--genome Mmul_1` (Ensembl)

- Mus musculus
  - `--genome mm10` (Ensembl)

- Oryza sativa japonica
  - `--genome IRGSP-1.0` (Ensembl)

- Pan troglodytes
  - `--genome CHIMP2.1.4` (Ensembl)
  - `--genome panTro4` (UCSC)

- Rattus norvegicus
  - `--genome Rnor_6.0` (Ensembl)
  - `--genome rn6` (UCSC)

- Saccharomyces cerevisiae
  - `--genome R64-1-1` (Ensembl)
  - `--genome sacCer3` (UCSC)

- Schizosaccharomyces pombe
  - `--genome EF2` (Ensembl)

- Sorghum bicolor
  - `--genome Sbi1` (Ensembl)

- Sus scrofa
  - `--genome Sscrofa10.2` (Ensembl)
  - `--genome susScr3` (UCSC)

- Zea mays
  - `--genome AGPv3` (Ensembl)

Note that you can use the same configuration setup to save sets of reference files for your own use, even if they are not part of the `AWS iGenomes` resource.
See the [Nextflow documentation](https://www.nextflow.io/docs/latest/config.html) for instructions on where to save such a file.

The syntax for this reference configuration is as follows:

```nextflow
params {
  genomes {
    '<GENOME>' {
      ac_loci                  = '</path/to/reference.loci>'
      ac_loci_gc               = '</path/to/ac_loci_gc file>'
      bwa                      = '</path/to/bwa indexes>'
      chr_dir                  = '</path/to/chromosomes/>'
      chr_length               = '</path/to/reference.len>'
      dbsnp                    = '</path/to/dbsnp.vcf.gz>'
      dbsnp_index              = '</path/to/dbsnp.vcf.gz.tbi>'
      dict                     = '</path/to/reference.dict>'
      fasta                    = '</path/to/reference.fasta>'
      fasta_fai                = '</path/to/reference.fasta.fai>'
      germline_resource        = '</path/to/germline_resource.vcf.gz>'
      germline_resource_index  = '</path/to/germline_resource.vcf.gz.tvi>'
      intervals                = '</path/to/reference.intervals>'
      known_indels             = '</path/to/known_indels.vcf.gz>'
      known_indels_index       = '</path/to/known_indels.vcf.gz.tbi>'
      mappability              = '</path/to/reference.gem>'
      snpeff_db                = '<snpEff DB>'
      species                  = '<species>'
      vep_cache_version        = '<VEP cache version'
    }
    // Any number of additional genomes, key is used with --genome
  }
}
```

### --igenomes_base

Specify base path to AWS iGenomes

Default: `s3://ngi-igenomes/igenomes/`

### --igenomes_ignore

Do not load `igenomes.config` when running the pipeline.
You may choose this option if you observe clashes between custom parameters and those supplied in `igenomes.config`.
This option will load the `genomes.config` file instead.
You can then specify the `--genome custom` and specify any reference file on the command line or within a config file.

### --genomes_base

Specify base path to reference genome

### --save_reference

Enable saving reference indexes and other files built within `Sarek`.

### --ac_loci

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--ac_loci <path/to/reference.loci>
```

### --ac_loci_gc

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--ac_loci_gc <path/to/reference.loci.gc>
```

### --bwa

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

> If none provided, will be generated automatically from the fasta reference.

```bash
--bwa <path/to/BWA/indexes>
```

### --chr_dir

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--chr_dir <path/to/chromosomes/>
```

### --chr_length

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--chr_length <path/to/chromosomes.len>
```

### --dbsnp

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--dbsnp <path/to/dbsnp.vcf.gz>
```

### --dbsnp_index

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

> If none provided, will be generated automatically from dbsnp `VCF` file.

```bash
--dbsnp_index <path/to/dbsnp.vcf.gz.tbi>
```

### --dict

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

> If none provided, will be generated automatically from the fasta reference.

```bash
--dict <path/to/reference.dict>
```

### --fasta

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--fasta <path/to/reference.fasta>
```

### --fasta_fai

> If none provided, will be generated automatically from the fasta reference.

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--fasta_fai <path/to/reference.fasta.fai>
```

### --germline_resource

The [germline resource VCF file](https://software.broadinstitute.org/gatk/documentation/tooldocs/current/org_broadinstitute_hellbender_tools_walkers_mutect_Mutect2.php#--germline-resource) (bgzipped and tabixed) needed by GATK4 Mutect2 is a collection of calls that are likely present in the sample, with allele frequencies.
The `AF` info field must be present.
You can find a smaller, stripped gnomAD `VCF` file (most of the annotation is removed and only calls signed by PASS are stored) in the `AWS iGenomes` `Annotation/GermlineResource` folder.
If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--germline_resource </path/to/resource.vcf.gz>
```

### --germline_resource_index

Tabix index of the germline resource specified at [`--germline_resource`](#--germline_resource).
If you prefer, you can specify the full path to your reference genome when you run the pipeline:

> If none provided, will be generated automatically from the germline resource `VCF` file.

```bash
--germline_resource_index </path/to/resource.vcf.gz.tbi>
```

### --intervals

To speed up some preprocessing and variant calling processes, the reference is chopped into smaller pieces.
The intervals are chromosomes cut at their centromeres (so each chromosome arm processed separately) also additional unassigned contigs.
We are ignoring the `hs37d5` contig that contains concatenated decoy sequences.
Parts of preprocessing and variant calling are done by these intervals, and the different resulting files are then merged.
This can parallelize processes, and push down wall clock time significantly.

The calling intervals can be defined using a `.list` or a `.bed` file.
A `.list` file contains one interval per line in the format `chromosome:start-end` (1-based coordinates).

When the intervals file is in `BED` format, the file must be a tab-separated text file with one interval per line.
There must be at least three columns: chromosome, start, and end.
In `BED` format, the coordinates are 0-based, so the interval `chrom:1-10` becomes `chrom<tab>0<tab>10`.

Additionally, the `score` column of the `BED` file can be used to provide an estimate of how many seconds it will take to call variants on that interval.
The fourth column remains unused.

||||||
|-|-|-|-|-|
|chr1|10000|207666|NA|47.3|

This indicates that variant calling on the interval chr1:10001-207666 takes approximately 47.3 seconds.

The runtime estimate is used in two different ways.
First, when there are multiple consecutive intervals in the file that take little time to compute, they are processed as a single job, thus reducing the number of processes that needs to be spawned.
Second, the jobs with largest processing time are started first, which reduces wall-clock time.
If no runtime is given, a time of 1000 nucleotides per second is assumed.
Actual figures vary from 2 nucleotides/second to 30000 nucleotides/second.
If you prefer, you can specify the full path to your reference genome when you run the pipeline:

> If none provided, will be generated automatically from the fasta reference.
> Use [--no_intervals](#--no_intervals) to disable automatic generation

```bash
--intervals <path/to/reference.intervals>
```

### --known_indels

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

```bash
--known_indels <path/to/known_indels.vcf.gz>
```

### --known_indels_index

If you prefer, you can specify the full path to your reference genome when you run the pipeline:

> If none provided, will be generated automatically from the known indels `VCF` file.

```bash
--known_indels_index  <path/to/known_indels.vcf.gz.tbi>
```

### --mappability

If you prefer, you can specify the full path to your Control-FREEC mappability when you run the pipeline:

```bash
--mappability <path/to/reference.gem>
```

### --snpeff_db

If you prefer, you can specify the DB version when you run the pipeline:

```bash
--snpeff_db <snpEff DB>
```

### --species

This specifies the species used for running `VEP` annotation.
If you use iGenomes or a local resource with `genomes.conf`, this has already been set for you appropriately.

```bash
--species <snpEff species>
```

### --vep_cache_version

If you prefer, you can specify the cache version when you run the pipeline:

```bash
--vep_cache_version <VEP cache version>
```

## Other command line parameters

### --outdir

The output directory where the results will be saved.

Default: `results/`

### --publish_dir_mode

The file publishing method.

Available: `symlink`, `rellink`, `link`, `copy`, `copyNoFollow`, `move`

Default: `copy`

### --sequencing_center

The sequencing center that will be used in the `BAM` `CN` field

### --multiqc_config

Specify a path to a custom `MultiQC` configuration file.

### --monochrome_logs

Set to disable colourful command line output and live life in monochrome.

### --email

Set this parameter to your e-mail address to get a summary e-mail with details of the run sent to you when the workflow exits.
If set in your user config file (`~/.nextflow/config`) then you don't need to specify this on the command line for every run.

### --email_on_fail

This works exactly as with `--email`, except emails are only sent if the workflow is not successful.

### --plaintext_email

Set to receive plain-text e-mails instead of HTML formatted.

### --max_multiqc_email_size

Threshold size for `MultiQC` report to be attached in notification email.
If file generated by pipeline exceeds the threshold, it will not be attached.

Default: `25MB`.

### -name

Name for the pipeline run.
If not specified, `Nextflow` will automatically generate a random mnemonic.

This is used in the `MultiQC` report (if not default) and in the summary HTML / e-mail (always).

**NB:** Single hyphen (core `Nextflow` option)

### --custom_config_version

Provide git commit id for custom Institutional configs hosted at `nf-core/configs`.
This was implemented for reproducibility purposes.

Default is set to `master`.

```bash
## Download and use config file with following git commid id
--custom_config_version d52db660777c4bf36546ddb188ec530c3ada1b96
```

### --custom_config_base

If you're running offline, `Nextflow` will not be able to fetch the institutional config files
from the internet.
If you don't need them, then this is not a problem.
If you do need them, you should download the files from the repository and tell `Nextflow` where to find them with the `custom_config_base` option.
For example:

```bash
NXF_OPTS='-Xms1g -Xmx4g'
```

> Note that the nf-core/tools helper package has a `download` command to download all required pipeline files + singularity containers + institutional configs in one go for you, to make this process easier.

## Job resources

### Automatic resubmission

Each step in the pipeline has a default set of requirements for number of CPUs, memory and time.
For most of the steps in the pipeline, if the job exits with an error code of `143` (exceeded requested resources) it will automatically resubmit with higher requests (2 x original, then 3 x original).
If it still fails after three times then the pipeline is stopped.

### --max_memory

Use to set a top-limit for the default memory requirement for each process.
Should be a string in the format integer-unit eg. `--max_memory '8.GB'`

### --max_time

Use to set a top-limit for the default time requirement for each process.
Should be a string in the format integer-unit eg. `--max_time '2.h'`

### --max_cpus

Use to set a top-limit for the default CPU requirement for each process.
Should be a string in the format integer-unit eg. `--max_cpus 1`

### --single_cpu_mem

Use to set memory for a single CPU.
Should be a string in the format integer-unit eg. `--single_cpu_mem '8.GB'`

## Containers

`sarek`, our main container is designed using [Conda](https://conda.io/).

[![sarek-docker status](https://img.shields.io/docker/automated/nfcore/sarek.svg)](https://hub.docker.com/r/nfcore/sarek)

Based on [nfcore/base:1.10.2](https://hub.docker.com/r/nfcore/base/tags), it contains:

- **[ASCAT](https://github.com/Crick-CancerGenomics/ascat)** 2.5.2
- **[AlleleCount](https://github.com/cancerit/alleleCount)** 4.0.2
- **[BCFTools](https://github.com/samtools/bcftools)** 1.9
- **[bwa](https://github.com/lh3/bwa)** 0.7.17
- **[bwa-mem2](https://github.com/bwa-mem2/bwa-mem2)** 2.0
- **[CNVkit](https://github.com/etal/cnvkit)** 0.9.6
- **[Control-FREEC](https://github.com/BoevaLab/FREEC)** 11.5
- **[FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/)** 0.11.9
- **[fgbio](https://github.com/fulcrumgenomics/fgbio)** 1.1.0
- **[FreeBayes](https://github.com/ekg/freebayes)** 1.3.2
- **[GATK4-spark](https://github.com/broadinstitute/gatk)** 4.1.6.0
- **[GeneSplicer](https://ccb.jhu.edu/software/genesplicer/)** 1.0
- **[ggplot2](https://github.com/tidyverse/ggplot2)** 3.3.0
- **[HTSlib](https://github.com/samtools/htslib)** 1.9
- **[Manta](https://github.com/Illumina/manta)** 1.6.0
- **[msisensor](https://github.com/ding-lab/msisensor)** 0.5
- **[MultiQC](https://github.com/ewels/MultiQC/)** 1.8
- **[Qualimap](http://qualimap.bioinfo.cipf.es)** 2.2.2d
- **[SAMBLASTER](https://github.com/GregoryFaust/samblaster)** 0.1.24
- **[samtools](https://github.com/samtools/samtools)** 1.9
- **[snpEff](http://snpeff.sourceforge.net/)** 4.3.1t
- **[Strelka2](https://github.com/Illumina/strelka)** 2.9.10
- **[TIDDIT](https://github.com/SciLifeLab/TIDDIT)** 2.7.1
- **[pigz](https://zlib.net/pigz/)** 2.3.4
- **[Trim Galore](https://github.com/FelixKrueger/TrimGalore)** 0.6.5
- **[VCFanno](https://github.com/brentp/vcfanno)** 0.3.2
- **[VCFtools](https://vcftools.github.io/index.html)** 0.1.16
- **[VEP](https://github.com/Ensembl/ensembl-vep)** 99.2

For annotation, the main container can be used, but the cache has to be downloaded, or additional containers are available with cache (see [annotation documentation](#using-downloaded-cache)):

`sareksnpeff`, our `snpeff` container is designed using [Conda](https://conda.io/).

[![sareksnpeff-docker status](https://img.shields.io/docker/automated/nfcore/sareksnpeff.svg)](https://hub.docker.com/r/nfcore/sareksnpeff)

Based on [nfcore/base:1.10.2](https://hub.docker.com/r/nfcore/base/tags), it contains:

- **[snpEff](http://snpeff.sourceforge.net/)** 4.3.1t
- Cache for `GRCh37`, `GRCh38`, `GRCm38`, `CanFam3.1` or `WBcel235`

`sarekvep`, our `vep` container is designed using [Conda](https://conda.io/).

[![sarekvep-docker status](https://img.shields.io/docker/automated/nfcore/sarekvep.svg)](https://hub.docker.com/r/nfcore/sarekvep)

Based on [nfcore/base:1.10.2](https://hub.docker.com/r/nfcore/base/tags), it contains:

- **[GeneSplicer](https://ccb.jhu.edu/software/genesplicer/)** 1.0
- **[VEP](https://github.com/Ensembl/ensembl-vep)** 99.2
- Cache for `GRCh37`, `GRCh38`, `GRCm38`, `CanFam3.1` or `WBcel235`

### Building your owns

Our containers are designed using [Conda](https://conda.io/).
The [`environment.yml`](../environment.yml) file can be modified if particular versions of tools are more suited to your needs.

The following commands can be used to build/download containers on your own system:

- Adjust `VERSION` for sarek version (typically a release or `dev`).

#### Build with Conda

```Bash
conda env create -f environment.yml
```

#### Build with Docker

- `sarek`

```Bash
docker build -t nfcore/sarek:<VERSION> .
```

- `sareksnpeff`

Adjust arguments for `GENOME` version and snpEff `CACHE_VERSION`

```Bash
docker build -t nfcore/sareksnpeff:<VERSION>.<GENOME> containers/snpeff/. --build-arg GENOME=<GENOME> --build-arg CACHE_VERSION=<CACHE_VERSION>
```

- `sarekvep`

Adjust arguments for `GENOME` version, `SPECIES` name and VEP `VEP_VERSION`

```Bash
docker build -t nfcore/sarekvep:<VERSION>.<GENOME> containers/vep/. --build-arg GENOME=<GENOME> --build-arg SPECIES=<SPECIES> --build-arg VEP_VERSION=<VEP_VERSION>
```

#### Pull with Docker

- `sarek`

```Bash
docker pull nfcore/sarek:<VERSION>
```

- `sareksnpeff`

Adjust arguments for `GENOME` version

```Bash
docker pull nfcore/sareksnpeff:<VERSION>.<GENOME>
```

- `sarekvep`

Adjust arguments for `GENOME` version

```Bash
docker pull nfcore/sarekvep:<VERSION>.<GENOME>
```

#### Pull with Singularity

You can directly pull singularity image, in the path used by the Nextflow ENV variable `NXF_SINGULARITY_CACHEDIR`, ie:

```Bash
cd $NXF_SINGULARITY_CACHEDIR
singularity build ...
```

- `sarek`

```Bash
singularity build nfcore-sarek-<VERSION>.img docker://nfcore/sarek:<VERSION>
```

- `sareksnpeff`

Adjust arguments for `GENOME` version

```Bash
singularity build nfcore-sareksnpeff-<VERSION>.<GENOME>.img docker://nfcore/sareksnpeff:<VERSION>.<GENOME>
```

- `sarekvep`

Adjust arguments for `GENOME` version

```Bash
singularity build nfcore-sarekvep-<VERSION>.<GENOME>.img docker://nfcore/sarekvep:<VERSION>.<GENOME>
```

## AWSBatch specific parameters

Running the pipeline on AWSBatch requires a couple of specific parameters to be set according to your AWSBatch configuration.
Please use [`-profile awsbatch`](https://github.com/nf-core/configs/blob/master/conf/awsbatch.config) and then specify all of the following parameters.

### --awsqueue

The JobQueue that you intend to use on AWSBatch.

### --awsregion

The AWS region to run your job in.

Default is set to `eu-west-1` but can be adjusted to your needs.

### --awscli

The [AWS CLI](https://www.nextflow.io/docs/latest/awscloud.html#aws-cli-installation) path in your custom AMI.

Default: `/home/ec2-user/miniconda/bin/aws`.

Please make sure to also set the `-w/--work-dir` and `--outdir` parameters to a S3 storage bucket of your choice - you'll get an error message notifying you if you didn't.

## Troubleshooting

### Spark related issues

If you have problems running processes that make use of Spark such as ```MarkDuplicates```.
You are probably experiencing issues with the limit of open files in your system.
You can check your current limit by typing the following:

```bash
ulimit -n
```

The default limit size is usually 1024 which is quite low to run Spark jobs.
In order to increase the size limit permanently you can:

Edit the file ```/etc/security/limits.conf``` and add the lines:

```bash
*     soft   nofile  65535
*     hard   nofile  65535
```

Edit the file ```/etc/sysctl.conf``` and add the line:

```bash
fs.file-max = 65535
```

Edit the file ```/etc/sysconfig/docker``` and add the new limits to OPTIONS like this:

```bash
OPTIONS=”—default-ulimit nofile=65535:65535"
```

Re-start your session.

Note that the way to increase the open file limit in your system may be slightly different or require additional steps.
