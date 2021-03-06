# Using the SLURM job scheduler
https://its.unc.edu/research-computing/techdocs/getting-started-on-longleaf/#Job%20Submission

There are two main ways to submit jobs on the compute cluster. The first is to submit a script from the login mode. The second is to use a compute node to work interactively. I use both.

## Method one: Submit a script from the login node:

Say we had a script to run bcbio-nextgen (a set of python scripts that will perform alignment of fastq files for RNA-seq). An example script would look like this
```
#!/bin/bash

#SBATCH -p general
#SBATCH --job-name=xentro9_test_bcbionextgen
#SBATCH --mail-user=example@ad.unc.edu
#SBATCH --mail-type=END
#SBATCH -c 6
#SBATCH -t 72:00:00
#SBATCH --mem=64G
#SBATCH -e xentro9_test_bcbionextgen_%j.err
#SBATCH -o xentro9_test_bcbionextgen_%j.out

export PATH=/proj/conlonlb/bcbio/anaconda/bin:/proj/conlonlb/bcbio/tools/bin:$PATH


bcbio_nextgen.py ../config/xtrop_xen9_test_submission.yaml -n 20
```

Every shell script starts with that first line. It is specifying that we are using bash.
The next few lines are specific to your individual cluster and jobs.
<br> -p is the partition that you are submitting to. UNC longleaf cluster has a number of partitions but the one that we always use is general
<br>--job_name is the name you want for your job.
<br> --mail-user will send an email to the address specified if the "type" has been reached. In this example, the mail-type is END. So, when its done for any reason, it will send you an email.
<br>-c is the number of cores you want to utilize for your job
<br>-t is a time limit for your job. If you go over the time limit your job will be killed by the cluster.
<br>--mem is the amount of memory you are asking for. If your job takes up too much memory, your job will be killed by the cluster
<br>-e is the name of the error file that is generated upon submission (%j will add the job number to the end of your name so that you can keep track of them
<br>-o is the name of the output file that is generated upon submission.
<br><br>
All of the commands that are not commented out (#) will then run. Here we have two commands. One sets the PATH, and one runs the python scripts.

# Checking your jobs
```
sacct
```
This is the command to check the status of your job.
