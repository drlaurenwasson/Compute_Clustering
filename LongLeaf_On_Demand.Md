
# Getting on the cluster- On Demand

There is a new way to get onto UNC's Longleaf cluster through a web browser. It is called "Open On Demand"

https://ondemand.rc.unc.edu/

Log in with your ONYEN and password.

Across the top you will see a menu: Files, Jobs, Clusters, Interactive Apps, My interactive Sessions
## Files
Under this header you should see
1. Home Directory. This is your home directory ```/nas/longleaf/home/<onyen>```
2. Project Directory. ```/proj``` 
3. A common data directory that I have never seen before ```/datacommons```
4. Temporary scratch space ```/pine/scr/<firstinitial>/<lastinitial>/<onyen>```. This has up to 30TB of storage space, and should be where we do many of our computation. Some things to keep in mind. <br><br>
  a. <b>Scratch file deletion will be enforced with files older than 36 days being removed. Any file not used or modified in the last 36 days will be deleted. </b><br><br>
  b. Scratch space is a shared, temporary work space. Please note that scratch space is <b>not backed up</b> and is, therefore, not intended for permanent data storage. Use Mass Storage to store permanent data.

## Jobs
Under this header you see
1. Active Jobs. This shows jobs actively running in the cluster
2. Job composer.

## Clusters
1. Longleaf Cluster: Clicking on this will open your terminal.

## Interactive Apps
1. Opening this dropdown menu shows you all of the "apps" available on the cluster. Here you can open things like R Studio, which gives you all the compute power of the cluster but you can still use R Studio like on your desktop.

# Using the Cluster
1. on this page: https://ondemand.rc.unc.edu/pun/sys/dashboard locate the Files panel, click down to /proj. Navagate to  ```/proj/conlonlb/users/lauren/robbe_et_al/resubmission/```
2. On the top of the page you should see <b>>_ Open in terminal </b> . Click that.
3. You have landed on a login node. A login node is designed to be a landing place, but the node itself has very little RAM and very little memory. You cant run too many commands on here, so I immediately move onto a compute node. To do this type: <br>
 ``` srun -t 5:00:00 -p interact -N 1 -n 1 --mem=20G --pty /bin/bash ``` <br>

 t = Amount of time requested. In this case I asked for 5 days. <br>
 p = partition. Which part of the cluster do you want to submit your job to? If you want to do interactive things, choose interactive. If you want to submit jobs to the cluster, use general. <br>
 N = number of nodes. Our jobs do not require a lot of computing power so I use 1. <br>
 n = number of tasks. How many computers per Node do you want. Again, since we do not need a lot we default to 1. <br>
 mem = memory allotment. I use 20G and then if I run out I ask for more. <br>
 pty = pseudo-terminal that allows you to run bash scripts <br>
 
4. Load your modules: If you dont know which modules are available type ```module spider <NAME>>```. It will tell you which versions of modules are already installed on Longleaf. Here we will install samtools, deeptools, and bedtools. <br> 
```module load samtools/1.14 deeptools/3.2.0 bedtools/2.29```


 
 
 
 
