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
git init creates a .git folder in the folder from where the command was run. 
It creates the folder structure which it needs to track the various objects being checked in using git.
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

- What does it mean if we say a file is untracked versus tracked?
<details><summary>Ans.</summary>
<p>

```
Untracked files - Files which have been created by user but not added to staging area using "git add".
Untracked files are shown in red in "git status" output.

Tracked files - Files which have been addded to staging area but haven't been committed as yet. 
Onlu "git add" has been performed on these files. "git commit" hasn't been initiated as yet.
Tracked files are shown in green in "git status" output.

```
</p>
</details>


- How to check if file1.txt exists in staging area i.e. is tracked file?
<details><summary>Ans.</summary>
<p>

```
$ git status
$ git ls-files -s

"git status" will show file1.txt in green meaning it is currently tracked (not committed).
"git ls-files -s" can be a test to see if a file is tracked, but what if it is already committed? 

###Perform below steps to see it in action
###create directory using "mkdir"
###move to directory using "cd"

$ mkdir test 
$ cd test 

###initialize repo using "git init"
###create a blank file in test directory using "touch"
$ git init 
$ touch file1.txt 

###check what files exist in working directory and are untracked using "git status". file1.txt should be in red(untracked).
$ git status 

###check which files are in staging area using "git ls-files -s". Should return nothing. 
$ git ls-files -s 

###create another blank file file2.txt in test directory.
###check what files exist in working directory and are untracked. file1.txt and file2.txt should be in red(untracked).
$ touch file2.txt 
$ git status 

###add file1.txt to staging area using "git add"
###"git status" should now show file1.txt in green (tracked) and file2.txt in red (untracked)
$ git add file1.txt 
$ git status 

###Below command should show file1.txt but not file2.txt
$ git ls-files -s 

###Should have content something similar to below
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt

###add file2.txt to staging area
$ git add file2.txt 

###Check file1.txt and file2.txt should be in green meaning it is in staging area.
$ git status 

###Below command should show file1.txt and file2.txt
$ git ls-files -s 

###Should have content something similar to below
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file2.txt
```
</p>
</details>

