# Making a text file on a computing cluster

Here is a quick tutorial on how to use vim (a text editor on the cluster) to generate text files. There are many options on Longleaf (nano, for example), but I use vim because that's what I was taught so that is what I'm familiar with. 

To generate a file:
```
vim testfile.txt
```

This will open a blank file called testfile.txt. You will see the file name in the bottom left corner. To make a csv file, call it testfile.csv. To make a shell script, call it testfile.sh. To make an R script, call it testfile.R. You have to specify the type of file by giving it the correct extension.

## Step 1: "INSERT"
First thing you need to do is hit I to change into "INSERT" mode. Once you hit "I" the bottom left will change from testfile.txt to --INSERT--. 

Now you can write or paste text. I find editing in vim to be a little clunky, so I usually write my file in my text editor (BBEdit) and then paste the text into the terminal.

To paste text on a cluster in Windows, instead of CTRL V, it's actually SHIFT + INS.

## Step 2: Save and quit
Once I have pasted my text, I want to get out of insert mode. To do that, hit ESC. You will no longer see --INSERT-- on the bottom left.

To save the file and quit, type ```:wq``` and hit ENTER
The : brings up the menu (like hitting the "file" button in word).
"w" stands for write to file.
"q" quits the text editor.

To quit without saving, type ```:q!``` and hit ENTER
