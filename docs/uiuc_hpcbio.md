# nf-core/configs: UIUC HPCBio configurations

The [High Performance Computing in Biology group (HPCBio)](https://hpcbio.illinois.edu/) is a core data science and analysis group at the University of Illinois under the Roy J. Carver Biotechnology Center. 

## Getting Started

This is a collection of profiles for HPC resources that HPCBio commonly uses, but does have some basic configurations for UIUC HPC resources that may be of use to other campus researchers.

## Running Nextflow

There are several computing resources available at the University of Illinois, with each having specific requirements for deploying Nextflow workflows. HPCBio has access to most of these and makes general configurations available for UIUC researchers to deploy workflows on these systems, though in some of these cases researchers may want to modify the default settings if they don't quite match the resources available in their own queues.

In any of the below cases, consider making use of screen or tmux on the system. This is recommended prior to starting an interactive session.

### IGB Biocluster

There are two configurations currently set up:

* `hpcbio` - HPCBio-specific queue on the IGB Biocluster
* `biocluster` - Open queue on the IGB Biocluster

The way to call these for a workflow, e.g., for nf-core/rnaseq, would be:

```
nextflow run nf-core/rnaseq -r 3.0.0 -profile uiuc_hpcbio,hpcbio ...
```

for HPCBio group (CBC) jobs, and:

```
nextflow run nf-core/rnaseq -r 3.0.0 -profile uiuc_hpcbio,biocluster ...
```

for others. 

At the moment these have to be run from a login node since worker nodes do not have network access, so cannot download and cache singularity images. HPCBio has a separate dedicated login node, therefore this isn't an issue with our group, but if you are a non-HPCBio user using the `biocluster` profile above you should contact the IGB's [CNRG](https://biocluster.igb.illinois.edu) to inquire about running jobs on the common login nodes before starting.

<!-- ### UIUC Campus Cluster IN TESTING

This configuration is in an early testing phase. When using Nextflow on the UIUC Campus Cluster, you need to launch Nextflow as an interactive jobs on one of the worker/compute nodes instead of the login nodes. Because starting an interactive job may take time, consider making use of screen or tmux on the system to allow time to start an interactive job.

Once set up, you should be able to run a job like so:

```
nextflow run nf-core/rnaseq -r 3.0.0 -profile uiuc_hpcbio,campus_cluster -process.queue "aces" ...
```

Note the queue setting here; this is **required** for Campus Cluster jobs. You can also include multiple queues, for example: 

```
nextflow run nf-core/rnaseq -r 3.0.0 -profile uiuc_hpcbio,campus_cluster -process.queue "aces,secondary" ...
```

Campus Cluster uses Apptainer instead of Singularity but other than this all other settings are largely the sample. -->

### CBC Biotech 

The Biotech Center HPC is a private resource for CBC-related data processing, with the resources centered on supporting the work of the DNA Services sequencing core. This currently consists of one configuration:

* `biotech`

If you have access to this resource please contact [HPCBio or the DNA Services core](https://biotech.illinois.edu) prior to launching jobs.

<!--

### Creating a Nextflow environment (this may need to be per HPC)

### Environment Variables (this may need to be per HPC)

#### `NXF_SINGULARITY_CACHEDIR` (this may need to be per HPC)

This is a Nextflow specific environment variable that will let Nextflow know where you have or would like downloaded Singularity images to be downloaded.

```{bash}
export NXF_SINGULARITY_CACHEDIR="/path/to/your/singularity/image/cache"

# Example for 'healthdatasci'
export NXF_SINGULARITY_CACHEDIR="/project/healthdatasci/singularity"
```

#### Specifying a Partition (this may need to be per HPC)

#### Example: Running nf-core/fetchngs (this may need to be per HPC)

```{bash}
``` 
-->
