# Helpful unix commands
Started with help from https://www.tipsandtricks-hq.com/basic-unix-commands-list-366 
# THERE IS NO EASY WAY TO UNDO (like control Z), so please double check your work when you use these commands!

## File/Directory operation related Unix Commands
<b>cp</b> – copy a file. <br>
The example below copies the file "file.txt" from the directory /proj/ to /proj/lkw <br>
```> cp file.txt /proj/ proj/lkw```
<br><br>
 
<b>mv</b> – move or rename files or directories. <br>
The example below moves the file "file.txt" from the directory /proj/ to /proj/lkw <br>
```> mv file.txt /proj/ /proj/lkw``` 
<br>
The example below renames the file "file.txt" to "newfile.txt" <br>
```> mv file.txt file2.txt```
<br><br>

<b>tar</b> – create and use archives of files. <br>

<b>gzip</b> – compress a file. <br>

<b>mkdir</b> – make a directory. <br>
The example below will make a directory/folder called "lkw" in the folder /proj/users
```> mkdir /proj/users/lkw```
<br> If you are already in the /proj/users directory, all you need to do is: <br>
```mkdir lkw```
<br><br>

rm – remove files or directories
rmdir – remove a directory
mount – attaches a file system to the file system hierarchy at the mount_point, which is the pathname of a directory.
umount – unmounts a currently mounted file system.
Navigational type Unix Commands
cd – change directory
pwd – display the name of your current directory
ls – list names of files in a directory
Disk, File and Folder Size/Usage
du – Use this command to see the size/usage of the folder you are in. Example usage: du -sk *
df – Report file system disk space usage. Example usage: df -k
Display file content
cat – concatenate and display files.
more – The more utility is a filter that displays the contents of a text file on the terminal, one screenful at a time.
less – Less is a program similar to  more  (1), but  which  allows backward  movement  in the file as well as forward movement. Also, less does not have  to  read  the  entire  input  file before starting,so with large input files it starts up faster than text editors like vi
File Editing
vi – The vi (visual) utility is a display-oriented text editor.
nano – nano is a small, free and friendly editor.
