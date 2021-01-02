- How to check the version of git installed on your system?
<details><summary>Ans.</summary>
<p>

```
$ git version
```
</p>
</details>

- How to create a new git repository on local computer?
<details><summary>Ans.</summary>
<p>

```
$ mkdir myDir
$ cd myDir
$ git init
```
</p>
</details>


- What does ```git init ``` command do?
<details><summary>Ans.</summary>
<p>

```
git init creates a .git folder in the folder from where the command was run. It creates the folder structure which it needs to track the various objects being checked in using git.
```
</p>
</details>


- Between a file creation and commiting the file which all areas does the file go into?
<details><summary>Ans.</summary>
<p>

```
1) Working Directory - This is where you ran git init command in and where you create the files. Exa. touch <fileName>
2) Staging Area - This is where file gets added using add command. Exa. git add <filename>
3) Git Repository - This is where file gets addded once an added file gets committed. Exa. git commit -m "Message"
```
</p>
</details>


- How to create a new file file1.txt and add it to staging area?
<details><summary>Ans.</summary>
<p>

```
$ touch file1.txt
$ git add file1.txt
```
</p>
</details>

- What does it mean if we say a file is untracked?
<details><summary>Ans.</summary>
<p>

```
It means that file exists in working directory but it is not part of the staging area. You can check if a file is untracked by doing git status.
```
</p>
</details>


- How to check if file1.txt exists in staging area?
<details><summary>Ans.</summary>
<p>

```
#this will show all the files which are currently untracked and the files which are to be committed. Files to be committed are the ones in staging area.
$ git status 

#this will check what files are present in staging area 
$ git ls-files -s 

#Perform below steps to see it in action
#create directory
$ mkdir test 
#move to directory
$ cd test 
#initialize repo
$ git init 
#create a blank file in test directory
$ touch file1.txt 
#check what files exist in working directory and untracked. Should show file1.txt in red and untracked
$ git status 
#check which files are in staging area. Should return blank as the file1.txt is only in working directory and not in staging area
$ git ls-files -s 
#create another blank file file2.txt in test directory
$ touch file2.txt 
#check what files exist in working directory and are untracked. Should show file1.txt and file2.txt in red and untracked
$ git status 
#add file1.txt to staging area
$ git add file1.txt 

#Check file1.txt should be in green meaning it is in staging area and file2.txt in red meaning untracked - in working directory and not in staging area
$ git status 

#Below command should show file1.txt but not file2.txt
$ git ls-files -s 

#Should have content something similar to below
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt

#add file2.txt to staging area
$ git add file2.txt 

#Check file1.txt and file2.txt should be in green meaning it is in staging area.
$ git status 

#Below command should show file1.txt and file2.txt
$ git ls-files -s 

#Should have content something similar to below
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file2.txt
```
</p>
</details>

