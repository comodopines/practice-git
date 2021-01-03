> Q. How to check the version of git installed on your system?
<details><summary>Ans.</summary>
<p>

```
$ git version
$ git --version
```
</p>
</details>


> Q. How to check help menu for a git command?
<details><summary>Ans.</summary>
<p>

```
$ git <command> help
$ git commit help
```
</p>
</details>

> Q. How to create a new git repository on local system?
<details><summary>Ans.</summary>
<p>

```
#Create a directory, move into it and run "git init"
$ mkdir -p /apps/myDir
$ cd /apps/myDir
$ git init
```
</p>
</details>

> Q. How to add files to staging area?
<details><summary>Ans.</summary>
<p>

```
#Using "git add" command
$ touch file1.txt
$ git add file1.txt
```
</p>
</details>

> Q. How to check if file exists in staging area i.e. is tracked file?
<details><summary>Ans.</summary>
<p>

```
#Using "git status" or "git ls-files -s"
$ git status
$ git ls-files -s

"git status" will show currently tracked (not committed) 
files (file1.txt) in green.

###Perform below steps to see it in action
###create directory using "mkdir"
###move to directory using "cd"

$ mkdir test 
$ cd test 

###initialize repo using "git init"
###create a blank file in test directory using "touch"
$ git init 
$ touch file1.txt 

###check what files exist in working directory and are untracked using "git status". 
###file1.txt should be in red(untracked).
$ git status 

###check which files are in staging area using "git ls-files -s". 
###Should return nothing. 
$ git ls-files -s 

###create another blank file file2.txt in test directory.
###check what files exist in working directory and are untracked. 
###file1.txt and file2.txt should be in red(untracked).
$ touch file2.txt 
$ git status 

###add file1.txt to staging area using "git add"
###"git status" should now show file1.txt in green (tracked) 
###and file2.txt in red (untracked)
$ git add file1.txt 
$ git status 

###Below command should show file1.txt but not file2.txt
$ git ls-files -s 

###Should have content something similar to below
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt

###add file2.txt to staging area
$ git add file2.txt 

###Check file1.txt and file2.txt should be in green font
###representing them being in staging area.
$ git status 

###Below command should show file1.txt and file2.txt
###This can only confirm if file is in staging area or not
###Only a good test if files are being staged for the first time
###As even after doing commit these files should be present here
$ git ls-files -s 

###Should have content something similar to below
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file2.txt
```
</p>
</details>

> Q. How to check what is the object type, size and content 
which is being used to generate the hash?
<details><summary>Ans.</summary>
<p>

```
Using "git cat-file" and the hash of the file we can get below (and other) info:
1) Content used for hash:
$ git cat-file -p e69de29bb2d1d6434b8b29ae775ad8c2e48c5391

2) Size of the file:
$ git cat-file -s e69de29bb2d1d6434b8b29ae775ad8c2e48c5391

3) Object type of the file:
$ git cat-file -t e69de29bb2d1d6434b8b29ae775ad8c2e48c5391
```
</p>
</details>

> Q. How to check what is the current user.name and user.email
configured on my system?
<details><summary>Ans.</summary>
<p>

```bash
#Using "git config" command
$ git config user.name
$ git config user.email
$ git config --list | grep user
```
</p>
</details>


> Q. How to set the user name and email on my system?
<details><summary>Ans.</summary>
<p>

```bash
#Using "git config" command
$ git config --global user.email "you@example.com"
$ git config --global user.name "your name"
```
</p>
</details>

> Q. How to commit a file to git repository?
<details><summary>Ans.</summary>
<p>

```bash
#Using "git commit" command
$ git commit -m "Message to add while commiting"
OR
$ git commit #Commit message will need to be put in vim editor
OR
$ git commit -m -a "Message to add while commiting" #if files are not already added to staging
```
</p>
</details>


> Q. How to check all the commits done to a repository?
<details><summary>Ans.</summary>
<p>

```bash
#Using "git log" command
$ git log
OR
$ git log --oneline #for concise log
```
</p>
</details>


> Q. How to delete a file which hasn't been staged as yet i.e. untracked?
<details><summary>Ans.</summary>
<p>

```bash
Since the file is untracked it can be removed by simple rm command.
```
</p>
</details>

> Q. How to delete a file from the tracked list, i.e. from staging area only?
<details><summary>Ans.</summary>
<p>

```bash
Since the file has been tracked and already "git add(ed)"
Hence it can be deleted by below options:

#This is essentially reset
$ git reset HEAD file3.txt

> Q. How to delete a file from the tracked list
i.e. from staging area and bring it to a previous commit state?
<details><summary>Ans.</summary>
<p>

```bash
The file (file3.txt) has been tracked and already "git add(ed)".
Since this needs to be brought to previous commit state, 
hence it can be done in following way:

#Head reset the file, essentailly delete the last commit and point the HEAD to previous commit
$ git reset HEAD file3.txt

#Then checkout the previous version
$ git checkout -- file3.txt
```
</p>
</details>


> Q. How to delete a file from the repository which was previously committed and if staging area is clean?
Scenario being "git status" mentions working tree as clean since file had been committed earlier.
Do not remove the file from working directory though.
<details><summary>Ans.</summary>
<p>

```bash
The file (file3.txt) has been committed earlier hence it is part of repo (cached).
Since there are currently no changes  in it, hence it is also present in wokring directory.

In this scenario you will have to remove only the cached version which is the committed file.

This can be done in following way:

#git rm <file> --cache
$ git rm file3.txt --cache

```
</p>
</details>

> Q. How to delete a file, which was previously committed, from the repository  and
if it is the same file which has been added to staging area just now?
Scenario being file was committeed earlier.
Modifications were made to file and "git add(ed)". Now remove the file from repo.
Do not remove the file from working directory though.
<details><summary>Ans.</summary>
<p>

```bash
The same command as above can be run. Difference is that now it will have the side affect of
file being removed from not just the repo but also the staged area.
File will be unstaged. In previous question since 
we hadn't made any changes that were "git add(ed)" hence it didn't matter.

#git rm <file> --cache
$ git rm file3.txt --cache

```
</p>
</details>

> Q. How to delete a file, which was previously committed, from the repository and
from the hard disk?
Scenario being file was committeed earlier.
Modifications were made to file and "git add(ed)". Now remove the file from repo, staging area
and the hard disk.
<details><summary>Ans.</summary>
<p>

```bash
The same command as above can be run. Difference is that now it will have the side affect of
file being removed from not just the repo but also the staged area.
File will be unstaged. In previous question since 
we hadn't made any changes that were "git add(ed)" hence it didn't matter.

#git rm <file> 
$ git rm file3.txt

```
</p>
</details>

> Q. How to recover a file which you just "rm(ed)" causing it to go away from local?
If the file was already added to staging area how will you recover the staged version?
<details><summary>Ans.</summary>
<p>

```bash
Since rm will remove file from local only, you can checkout the file back from repo.
Since staging area already has a version it will be that version which git checkout returns.

#Checkout the previous version
$ git checkout -- file3.txt
```
</p>
</details>


> Q. How to recover a file which you just "rm(ed)" causing it to go away from local?
You didn't stage your changes, then which version will be returned and how?
<details><summary>Ans.</summary>
<p>

```bash
Since rm will remove file from local only, you can checkout the file back.
Since you didnt stage your latest changes hence checkout will return last committed version.

#Checkout the previous version
$ git checkout -- file3.txt
```
</p>
</details>

> Q. How to recover a file which you just "git rm(ed)" causing it to go away from everywhere?
<details><summary>Ans.</summary>
<p>

```bash
Since git rm will remove file from staging, index, repo and local hence only way we can
bring it back by going back to a previous commit version of it. git revert will not work
as the file has been removed from repo, staging etc. The onyl course of action is to reset the head
to a previous version.


#Head reset the file, essentailly delete the last commit and point the HEAD to previous commit
$ git reset HEAD file3.txt

#Then checkout the previous version
$ git checkout -- file3.txt
```
</p>
</details>

> Q. How to recover a file's older version if you just "committed" a newer version by mistake?
<details><summary>Ans.</summary>
<p>

```bash
Since new version is already committed, hence checkout will checkout the recent version.
Also resetting the head will not work as file is already committed.
Best option is to revert the last commit using git revert.


#Head reset the file, essentailly delete the last commit and point the HEAD to previous commit
$ git revert --no-edit HEAD

#File is already checkdout at older version right now.
#Git added a commit message automatically in git log mentioning the rever that it was performing
```
</p>
</details>


> Q. How to commit a file without adding additional commit.
Perhaps reusing the last commit object?
<details><summary>Ans.</summary>
<p>

```bash
The same command as above can be run. Difference is that now it will have the side affect of
file being removed from not just the repo but also the staged area.
File will be unstaged. In previous question since 
we hadn't made any changes that were "git add(ed)" hence it didn't matter.

#git rm <file> --cache
$ git rm file3.txt --cache

```
</p>
</details>

> Q. How to create a branch?
<details><summary>Ans.</summary>
<p>

```bash
$ git branch <branchName>
$ git branch feature-1
```
</p>
</details>

> Q. How to move to a branch?
<details><summary>Ans.</summary>
<p>

```bash
$ git checkout <branchName>
$ git checkout feature-1

You can create the branch and checkout at same time with -b flag
$ git checkout -b feature-1

```
</p>
</details>

> Q. How to list all the branches available?
<details><summary>Ans.</summary>
<p>

```bash
$ git branch
```
</p>
</details>

> Q. How to know your current branch you are in?
<details><summary>Ans.</summary>
<p>

```bash
$ git rev-parse --abbrev-ref HEAD

OR
$ cat .git/HEAD | awk -F"heads\/" '{print $2}'
```
</p>
</details>
