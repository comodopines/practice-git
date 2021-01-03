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


> Q. What is a working directory?
<details><summary>Ans.</summary>
<p>

```
It is the directory from where "git init" was run.
If "git init" was run from within "/apps/myDir" then "/apps/myDir/" is working directory.
$ pwd
/apps/
$ mkdir myDir
$ cd /apps/myDir
$ git init
```
</p>
</details>


> Q. What does ```git init ``` command do?
<details><summary>Ans.</summary>
<p>

```
git init creates a .git folder inside the folder from where the "git init" was run.
If "git init" was run from "/apps/myDir" then 
we will see "/apps/myDir/.git" folder after running init.
.git is the folder which git uses to track the 
various objects within a working directory (/apps/myDir/ in our case).
```
</p>
</details>


> Q. Are working directory, staging area and git repository same?
<details><summary>Ans.</summary>
<p>

```
Different. Between a file creation and until its committed it in git repo,
it is present in either one or more of these directories:

1) Working Directory:
This is where you ran git init command (has .git folder)
This is where you create the files/folders. Basically your code folder.

2) Staging Area:
This is where file gets added by using add command.
Exa. git add <filename> adds file to staging area.

3) Git Repository:
This is where file gets addded once an added file gets committed using commit command.
Exa. git commit -m "Message"
```
</p>
</details>


> Q. How to create a new file file1.txt and add it to staging area?
<details><summary>Ans.</summary>
<p>

```
#Using "git add" command
$ touch file1.txt
$ git add file1.txt
```
</p>
</details>

> Q. What is an untracked versus a tracked file?
<details><summary>Ans.</summary>
<p>

```
1) Untracked files:
Files which have been created by user but not added
to staging area using "git add". Untracked files are
shown in red in "git status" output.

2) Tracked files:
Files which have been addded to staging area but
haven't been committed as yet. Only "git add" has
been performed on these files, not "git commit".
Tracked files are shown in green in "git status" output.
```
</p>
</details>


> Q. How to check if file1.txt exists in staging area i.e. is tracked file?
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


> Q. Explain the fields of "git ls-files -s" output?
<details><summary>Ans.</summary>
<p>

```
c1     c2                                       c3      c4
100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt

Below are explanation of c1, c2, c3 and c4:
1) 100644    - c1 defines type of file and its permission
               (100 being regular file 644 being it permission out of 777)
2) e69de2... - c2 this is the hash of the file1.txt
3) 0         - c3 denotes how many versions of files exist in 
               the repo. 0 denotes 0th version (only one version)
4) file1.txt - c4 is the file name in staging area.
```
</p>
</details>

> Q. What hashing function git uses to generate column2 (c2) above?
<details><summary>Ans.</summary>
<p>

```
SHA1. Its output is a 40 characters long hexadecimal string
```
</p>
</details>


> Q. Can the sha1 hash string output be more than 40 characters?
<details><summary>Ans.</summary>
<p>

```
No. Since SHA1 generates 160 bits long hash and each character 
in hash string is a hexadecimal char (4 bits), hence
the hashing string can't be greater or less than 40 characters.
160 bits hash output / 4 bits to represent one hexadecimal character = 40 hexadecimal characters.
```
</p>
</details>

> Q. What is this input to sha1 hash function to generate these hashes?
<details><summary>Ans.</summary>
<p>

```
The hash is generated using 4 elements:
- type of object being staged/tracked.
- size of object
- padding null character '\0'
- file content.
```
</p>
</details>

> Q. Can two files have same hash?
<details><summary>Ans.</summary>
<p>

```
Yes, if the object type, size and content of two files is same then their hash will be equal.
```
</p>
</details>

> Q. How can I check what is the object type, size and content 
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


> Q. How many object types exist in git?
<details><summary>Ans.</summary>
<p>

```
There are four types of object:
1) blob - is used to store file data- it is generally a file.
2) commit - holds metadata for each change introduced in the repos. 
            It includes author, committer, commit-data, and log- messages.
3) tree - this is to reference filenames for the object types (files) and their hashes.
4) tag - arbitrary human-readable name to a specific object usually a commit.
```
</p>
</details>

> Q. My files have already been added to staging area, did something change in .git directory at this point?
I havent committed any files only did "git add file1.txt file2.txt".
<details><summary>Ans.</summary>
<p>

```
Once "git add" has been run, we saw the hash of the file objects has been created when we ran "git ls-files -s" to check staging area.
For every hash (therefore object) a directory/file gets created in .git/ folder. 
The naming convention of the file is as follows (keeping our file hash e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 in mind):

$ workingDirectory/.git/<firstTwoHashCharacters/<Last38HasCharactersFileName>

In our example by adding file to staging area git created below directory and file as our file hash was e69de29bb2d1d6434b8b29ae775ad8c2e48c5391:
/apps/myDir/.git/objects/e6/9de29bb2d1d6434b8b29ae775ad8c2e48c5391

Since both files had same hash, hence only one file exists.
```
</p>
</details>

> Q. If only two hexadecimal characters from file hash are being used to create a directory under .git/objects/ folder,
then how many unique folders can be created in .git/objects directory?
Remember that files havent been committed as yet only "git add file1.txt file2.txt" was done.
<details><summary>Ans.</summary>
<p>

```
Bit of bit theory first:

Let's say you have one bit "X" to represent folder name, 
then you have only two options, either 0 or 1, which can be stored in "X". 
Hence only two folderNames are possible with a single bit "X".
i.e folderName 0 and folderName 1.

If you had 2 bits "XY" to represent folder name, 
now you can assign four folder names i.e. 00, 01, 10 and 11.

3 bits "XYZ", can assign eight folder names. 
i.e. 000, 001, 010, 011, 100, 101, 110, 111.

So having a total of N placeholders ( length("XYZ....") = N) 
where each one of these N placeholders can carry one out of M values
( M=2 in case of bit i.e. 0 or 1), will
make (M exponent N) naming values.

In above examples of "X", "XY" and "XYZ" we got
2 exp 1= 2 for "X" where M=2 (either 0 or 1) and N=1 length of "X"
2 exp 2= 4 for "XY" where M=2 (either 0 or 1) and N=3 length of "XY"
2 exp 3= 8 for "XYZ"... and so on 

With that under belt we know in case of git, it chooses first two hexadecimal
characters as folder name. Since each hexadecimal character is 4 bits long,
so in total git can use 4+4 = 8 bits to represent each folder. 

Hence total folders will be 2 exp N = 2 exp 8 = 256 folders.
$ workingDirectory/.git/<firstTwoHashCharacters/<Last38HasCharactersFileName>

In our example by adding file to staging area git 
created below directory and put a single file in it. 
Since the hash for our file was e69de29bb2d1d6434b8b29ae775ad8c2e48c5391, 
hence filename was created as:
/apps/myDir/.git/objects/e6/9de29bb2d1d6434b8b29ae775ad8c2e48c5391

where "e6" is folder and remaining 38 were used as filename.
```
</p>
</details>


> Q. If only two hexadecimal characters from file hash 
are being used to create a directory under .git/objects/ folder, then :
  a) How many unique file hashes can be created in a single .git/objects/<aGivenDirectory>?
  b) How many unique files can be in each of the above unique folders?
  c) How many total unique files can sha1 hash represent?
<details><summary>Ans.</summary>
<p>

```
If two char are used for folder name from the file hash
hence we have 
M = 2 (either 0 or 1)
N = 2 char * 4 bits per hex char

Hence, a total of 2 exp 8 = 256 folders.


Number of unique files per folder will be:
M = 2
N = 38 char * 4 bits per hex char

Hence a toal of 2 exp 152 unique files per folder.

Total number of unique folder/file combination will then be:
Total unique folders * Total unique files per folder
= (256) * (2 exp 152) ...... (xx)


Not surpisingly this is actually 2 exp 160 where 160 bits
was how long a sha1 hash was.

Since 256 = 2 exp 8
hence (xx) above becomes (2 exp 8) * (2 exp 152) = 2 exp (8+152) = 2 exp 160
```
</p>
</details>


> Q. I have added files using "git add", can I commit files now using "git commit"?
Or do I need to check some pre-requisite?
<details><summary>Ans.</summary>
<p>

```
If user.name and user.email is already configured then there is no pre-req needed
to commit files. If not, we need to configure user name and email.
```
</p>
</details>

> Q. How can I check what is the current user.name and user.email
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


> Q. How do I set the user name and email on my system?
<details><summary>Ans.</summary>
<p>

```bash
#Using "git config" command
$ git config --global user.email "you@example.com"
$ git config --global user.name "your name"
```
</p>
</details>


> Q. Once user and email is set what does "git commit" command achieve?
<details><summary>Ans.</summary>
<p>

```
"git commit" achieves following:

1) Save the files from staging area to the git repository (or database if you want to call it).

2) Creates additional hash objects to track the commit, mainly:
   a) Commit object: Has details like which author name and email, committer name,
      parent hash (previous commit to current commit) and email and tree object for this commit. 
   b) Tree object: contains the reference of all the files and their types
      which were committed as part of this commit.

##Below is the content of a commit object which shows reference to tree, author and committer
$git cat-file -p <hash of commit object>
tree 05ca2475d3c2f22ff8835bb202c56b174603c5ff
author Your Name <you@example.com> 1609628181 +0000
committer Your Name <you@example.com> 1609628181 +0000

#Tree object content showing the list of blobs and their names added as part of the commit.
$git cat-file -p <hash of tree object for above commit object first line>
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    file1.txt
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    file2.txt
```
</p>
</details>

> Q. Ok, so if file content is saved as blob object, commit is saved as commit object
then why do we need the tree object?
<details><summary>Ans.</summary>
<p>

```
A blob object is built using file content and 
some other "things" hashed together (object type [blob], size and null).
Tree object is a way to connect hash string to its filename, type and permissions.

#You can use below snippet to find each type of object 
#which gets created after a commit.
#
#
#/bin/bash
WORKDIR=$(pwd); 
OBJDIR=$WORKDIR/.git/objects/; 
cd ${OBJDIR};
clear;
echo;echo;
echo "|-> Obj Dir : "${OBJDIR}; 
find . -type f | while read fileName; 
do 
   HASH=`echo ${fileName}|sed "s/\.//g" | sed "s/\///g"` ;
   echo "|  |--> File Name: "${fileName}; 
   echo "|  |   |--> File Hash : "${HASH}; 
   echo "|  |   |--> File Type : "`git cat-file -t ${HASH}`;
   echo "|  |   |--> File Size : "`git cat-file -s ${HASH}` ; 
   echo "|  |   |--> File Data : ";
   git cat-file -p ${HASH}| while read line; 
   do 
      echo "|  |     "${line};
   done; 
   echo "|  | "; 
   echo "|  | ";
done; 
cd ${WORKDIR}

```
</p>
</details>

