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
1) A .csv file that contains metadata information for your samples. I have linked an example [HERE](https://github.com/drlaurenwasson/Compute_Clustering/blob/master/bcbio-nextgen/xtrop_xen10_test_submission.csv)

