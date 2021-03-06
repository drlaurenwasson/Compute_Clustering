# Introduction to bcbio-nextgen
Full documentation can be found here:
https://bcbio-nextgen.readthedocs.io/en/latest/

Bcbio-nextgen is a set of scripts used to run Next-generation sequencing pipelines. It is essentially a set of python scripts that chain all steps together so that you can just set up one experiment, submit it, and the program will do the rest for you.

# Installation and getting started
Full details about installation can be found in the link above. However, I have installed bcbio-nextgen in the Conlon Lab directory

However, bcbio-nextgen is not installed on the Longleaf cluster as a module. Therefore, you do not load it using module load like other modules. Therefore, to access all of the scripts that bcbio has you must set your PATH to the right location.

A PATH is an environment variable on Unix-like operating systems that specifies a set of directories where executable programs are located. In general, each executing process or user session has its own PATH setting. If you do not set your path to the right location and try to run bcbio-nextgen, the commands will fail because it will say that the scripts are not installed. 

## Step 1: Log into the cluster and navagate to your working directory
```
ssh onyen@longleaf.unc.edu
```
enter your password
<br>
Change directories to where you want to run your script
```
cd /proj/conlonlb/users/YOURFOLDER
```
## Step 2: Set your PATH
The PATH is where I installed the tools you will need to run. So, type
```
export PATH=/proj/conlonlb/bcbio/anaconda/bin:/proj/conlonlb/bcbio/tools/bin:$PATH
```
You will need to do this EVERY TIME you log into the cluster to run this script, because once you log off the cluster, your PATH will reset to its default parameter. 

## Step 3: Set up your analysis
### Bulk RNA-seq
Bc-bio can perform multiple kinds of analysis. Let's look at bulk-RNA-seq:

To run bulk RNA-seq you need to create two files:
1) A .csv file that contains metadata information for your samples. I have linked an example [HERE.](https://github.com/drlaurenwasson/Compute_Clustering/blob/master/bcbio-nextgen/xtrop_xen10_test_submission.csv)

I use a free text-editor for all of my coding. I believe the newest version is called BBEdit
CSV stands for comma separated value, so your file should look like this:

```
samplename,description,sex,genome,user
X-Trop-1_R1_001.fastq.gz,xtrop-1,male,XenTro10,Kerry
X-Trop-1_R2_001.fastq.gz,xtrop-1,male,XenTro10,Kerry
```

The first line will always have samplename and description as its first two parameters, and then after that you can decide what parameters to add. Here, I added sex (the study was comparing male versus female), the genome I want to align to, and who I am doing the analysis for. Other things you can add includ genotype, cellline, mutation, gene, timepoint, drug dose. Whatever.

For more information about making a textfile in the cluster, see my page [HERE.](https://github.com/drlaurenwasson/Compute_Clustering/blob/master/04-Making%20text%20files%20via%20command%20line.md)

2. a template, named something like submission-template.yaml. I have linked an example [HERE.](https://github.com/drlaurenwasson/Compute_Clustering/blob/master/bcbio-nextgen/xtrop_xen10_test_submission-template.yaml)

```
# Template for xenopus RNA-seq using Illumina prepared samples
---
details:
  - analysis: RNA-seq
    genome_build: XenTro10
    algorithm:
      aligner: star
      quality_format: standard
      trim_reads: False
upload:
  dir: ../final
```

I have installed genome_builds hg38, XenTro9, XenTro10, and mm10. I have installed STAR, BWA and hisat2 aligners. If you want more options, let me know and I can install them. 

STAR is my preferred aligner for RNA_seq data. trim_reads is a parameter where you run Trimmomatic to trim the ends off of reads. I assume that the ends are trimmed when we receive samples from the HTSF, so here I have set it to FALSE. 

#### Finish set up
After you establish your PATH, the first command you will run is: 

```bcbio_nextgen.py -w template <<template.yaml>> <<csv.csv>> <<ALL THE FASTQ files>>```
As an example: 
```
bcbio_nextgen.py -w template xtrop_xen10_test_submission-template.yaml xtrop_xen10_test_submission.csv *.fastq.gz
```
The ```*.fastq.gz``` command at the end is saying "All files in this folder that END in fastq.gz". So the fastq files need to be in the same folder where you are running this command. Or, you can do it like this 

```
bcbio_nextgen.py -w template xtrop_xen10_test_submission-template.yaml xtrop_xen10_test_submission.csv /proj/conlonlb/users/wasson/fastq/*fastq.gz
```
Here it is saying, "All the files in the folder /proj/conlonlb/users/wasson/fastq/ that END in "fastq.gz"". So it can be a path to the fastq files or the actual fastq files in the folder. 

## Step 4: Check the setup is correct
The previous command will set up a folder with the same name as what you named the csv file. Change directories into that folder. You will now see two folders: config and work.
Change into the config folder. You will see your original csv and submission template yaml file, but there will also be another yaml file. This is the file that bcbionextgen will use to run the analysis.

```
less xtrop_xen10_test_submission.yaml
```

You can see that bcbio has used the csv and the template we provided to make this file. But, sometimes it does a bad job with this if your fastq files are not ending like R1.fast.gz and R2.fastq.gz. You might have to manually edit this file so that R1 and R2 are paired (I had to do this with files that ended in R1_001.fastq.gz and R2_001.fastq.gz). View the fixed example [HERE.](https://github.com/drlaurenwasson/Compute_Clustering/blob/master/bcbio-nextgen/xtrop_xen10_test_submission.yaml) This is what the first few lines look like, and this block of text repeats for each sample.

```
details:
- algorithm:
    aligner: star
    quality_format: standard
    trim_reads: false
  analysis: RNA-seq
  description: xtrop-1
  files:
  - /proj/conlonlb/users/wasson/X-Trop-1_R1_001.fastq.gz
  - /proj/conlonlb/users/wasson/X-Trop-1_R2_001.fastq.gz
  genome_build: XenTro10
  metadata:
    sex: male
    genome: XenTro10
    user: Kerry
```

## Step 5: Run bcbio-nextgen

Change to the "work" directory. Here we will write a basic shell script to submit to the cluster. For more information on how to submit jobs to the cluster using the SLURM schedule, see my page [HERE.](https://github.com/drlaurenwasson/Compute_Clustering/blob/master/03-SLURM.md) 

Type:
```
vim submit_bcbio.sh
```
This opens up a text editor. Paste the following text, filling in your specific details. See the SLURM page above for information about the parameters
```
#!/bin/bash

#SBATCH -p general
#SBATCH --job-name=xentro10_test_bcbionextgen
#SBATCH -c 6
#SBATCH -t 48:00:00
#SBATCH --mem=64G
#SBATCH -e xentro10_test_bcbionextgen.err

#Set the PATH (we probably already did this, but better safe than sorry)
export PATH=/proj/conlonlb/bcbio/anaconda/bin:/proj/conlonlb/bcbio/tools/bin:$PATH

bcbio_nextgen.py ../config/xtrop_xen10_test_submission.yaml -n 20
```

Here, we are running the bcbio_nextgen.py script using the YAML file that was just created. This should submit your job to the cluster. 

# Bcbio-nextgen output
Once your job is finished, you should see a new folder called "final". If you look in that directory, you will see individual folders for each sample, and one folder with a different name (this is the combined folder). If you look in the folder for each sample, there will be directories called "qc", "salmon", and "star", and then bam files. 

the "qc" folder contains the quality control metrics for each tool that was run in the pipeline. Heres an example of other files that are in the folder (in this example, the sample is called "S1"
```
S1
├── S1-ready.bam -- coordinate-sorted whole genome alignments
├── S1-ready.counts -- featureCounts counts
├── S1-transcriptome.bam -- alignments to the transcriptome
├── salmon
│   ├── abundance.h5 -- h5 object, usable with sleuth
│   └── quant.sf -- salmon quantifications, usable with tximport
└── STAR
    ├── S1-SJ.bed -- STAR junction file in BED format
    └── S1-SJ.tab -- STAR junction file in tabular format
```

The combined folder contains all of the same information but for all sample. For DESEQ2, the file we want was aligned with STAR and counted/annotated using FeatureCounts. This file is found in the combinedfolder/featureCounts/ and is called annotated_combined.counts. Download this file to import into DESEQ (vignette found [HERE.](https://github.com/drlaurenwasson/R_tutorials/blob/master/DESeq2/DESeq2_vignette.md)
