
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
