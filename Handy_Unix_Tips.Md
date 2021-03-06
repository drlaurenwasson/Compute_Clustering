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
The example below will make a directory/folder called "lkw" in the folder /proj/users <br>
```> mkdir /proj/users/lkw```
<br> If you are already in the /proj/users directory, all you need to do is: <br>
```> mkdir lkw```
<br><br>

<b>rm</b> – remove files or directories. <br>
<b>rmdir</b> – remove a directory <br>
I dont recommend these for new users. Instead, make a directory called "trash" and move your bad files/directories into there. <br>
```
> mkdir trash
> mv badfile.txt baddirectory trash
```

<br><br>

## Navigational type Unix Commands
<b>cd</b>– change directory. <br>
The example below will change directories to /proj/users/lkw <br>
```> cd /proj/users/lkw```
<br><br>

<b>pwd</b> – display the name of your current directory. <br>
```> pwd```
<br><br>

<b>ls</b> – list names of files in a directory. The command ls -l will give you more information than just ls <br>
```> ls -l ```
<br><br>

## Display file content
<b>cat</b> – concatenate and display files. <br>
<b>more</b> – The more utility is a filter that displays the contents of a text file on the terminal, one screenful at a time. <br>
<b>less</b> – Less is a program similar to  more  (1), but  which  allows backward  movement  in the file as well as forward movement. Also, less does not have  to  read  the  entire  input  file before starting,so with large input files it starts up faster than text editors like vi <br>
<br><br>

## File Editing
nano – nano is a small, free and friendly editor. More information can be found here https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/
