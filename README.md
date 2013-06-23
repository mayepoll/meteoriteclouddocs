meteoriteclouddocs
==================
This documentation will give some background information on what Git software is, its purpose, and how to use Git for updating data sets. By the end of this section, the user should have a better idea of Git functionality and how to go about depositing and extracting data in Git repositories.

Git Software and Meteorite Cloud

The Meteorite Cloud solution uses Git software on servers that, in some cases, users create to upload data. The software is a means of storing the latest version of that data, as well as any previous versions that the user may want to refer to at a later stage. This documentation will act as a guide in setting up a data repository and making changes to it.
What is Git?

Git is essentially a software provider, producing open source and free version control software designed for the updating of data. The concept of version control records changes to data or sets of data over time, using any file type. Anything from a simple text file, to more complex types such as spreadsheets can be updated using version control. Version control systems have traditionally been fairly troublesome due to reliability issues, but Git aims to eradicate these problems by using a slightly different approach, which this documentation will detail.

Why Use Version Control?

The main advantages of version control are:

•   Being able to dig out a version of a file from a previous state, particularly useful for solving discrepancies;
•	The ability to see who last made a change to something that may be causing trouble;
•	The capability to regress the whole of a project back to a previous state.

Information can usually be recovered if something goes wrong or is lost.

What Makes Git Functionality Different to Other Providers’?

Simple version control systems may involve backing up files in another directory. This method is fairly unreliable as it is easy to write the wrong file, copy the incorrect files over by accident, or forget which directory saved or copied files are in.
In a bid to counteract these potential problems, programmers developed local version control systems containing simple databases that kept all changes to files under version control. A popular tool was a system called RCS that works by storing patch sets (the differences between files) in a special format on disk. If required it can then recreate an exact replica of the file from any point in time. 
As an advancement to this concept, centralised version control systems were developed to collaborate with other editors on other systems. This type of system has one server housing all versions of files, and permits a number of clients to output files from that single area.
Git software goes one step further and incorporates distributed version control systems, where clients output the latest snapshots (saved references) of files, while completely echoing the repository. This means that if any server ceases to function, and various systems were working in partnership via it, any of the client repositories can be replicated back to the server to restore any lost data. Every checkout is, in effect, an entire back up of all data. Other plus points are that administrators have tight control over who can do what, and it is easier to administer than local databases for every editor.

How Does Git Software Operate?

Git software is also designed so that assorted remote repositories can be controlled at one time, so teaming up with different individuals in diverse ways concurrently on the same data/project can occur. A mixture of workflows can be created, including hierarchy based access or privileges.
The key difference to the way in which data is stored using Git to the more historical methods is that Git considers data like snapshots of a file system, rather than information kept as a set of files that are individually changed over time. This can be illustrated by using the example of taking a photograph of the same scene over different times of the year; one picture might show an autumnal scene with orange and red leaves, while another may show snow on the ground. 
Git will save a link to these ‘pictures’ and can detect if files have changed or not. If they have not, Git will not save the file, but instead link to the preceding matching file it has stored.
The software is highly flexible, in that a file can be worked on while away from an internet connection, so any changes made can be uploaded and committed once a connection is reached.
All data in Git is check summed before it is stored and is then referred to using the checksum. This means you cannot change a file’s contents without Git recording it.

The Basics of Git in Relation to Repositories

Before creating or importing a repository, it is useful to understand that there are three states that projects can exist in: committed, modified and staged. 

•	At the committed stage, data is saved locally; 
•	At the modified stage, the file has been altered but it is not yet committed to the database;
•	When changes are staged, an adapted file is earmarked in its present version to transfer into a commit snapshot.

There are also three main sections of a Git project:

•	The Git directory is where the metadata and database of the project is kept. If a repository is cloned from another computer, it is stored here.
•	The working directory is a checkout of a certain version of the project. These files can be extracted from the compressed database in the Git directory and put on to disk if needs.
•	The staging area acts as a workspace that stores information about what will transfer into the proceeding commit.

Therefore, files can be modified in the working directory, snapshots of the files then go into the staging area to be staged, then once a commit is made, the snapshot is saved forever in the Git directory. If a file has been changed since it was checked out but not staged, then it is modified.

How To Get a Data Repository

The repository is where all the data and snapshots are held for a particular project. There are two main ways in which to obtain a repository. These are:

1.	Taking an existing project or directory and importing it into Git.
2.	Cloning an existing Git repository from another server.

How To Use An Existing Project

To start recording an existing project in Git, click on the project’s directory and input the following:

$ git init

This creates a subdirectory with the suffix of .git containing all needed files in a Git repository skeleton. It is wise to do an initial commit in order to start tracking an existing project. To do this, use the following Git add commands that include the files to track, then add a commit:

$ git add *.c
$ git add README
$ git comit –m ‘initial project version’

What is now available is a Git repository consisting of tracked files and a preliminary commit.

How To Clone An Existing Repository

To add to an active project, it is necessary to make a copy of that Git repository. Perform the following command:

git clone

This will copy every version of every file for the lifespan of a project.

To clone a repository, use a URL and the git clone function. For instance, to clone the Ruby Git library called Grit, use the following command:

$ git clone git://github.com/schacan/grit.git

This will generate a directory called grit, produce a .git directory within it, clone all the data for that repository, and result in a usable copy of the latest version.

To copy the repository into a directory with a different name, refer to that on the next command line like this:

$ git clone git://git hub.com/schacan/grit.git mygrit

How To Commit Changes to the Repository

Every file in the working directory can be either tracked or untracked. Tracked files are those contained in the last snapshot, in the form of unmodified, modified or staged. Untracked files are those not in the last snapshot or in the staging area. All files will be tracked and unmodified when a project is initially cloned because no changes have yet been made.
Each time an alteration is made to a file, the next step is to stage this modified file then commit the staged changes. The process then starts again.

How to Check File Statuses

Using the git status command, immediately after cloning a file, it is possible to check which files are in which state. Performing the following command will result in this:

$ git status
# On branch master
nothing to commit (working directory clean)

The above depicts that no tracked files are modified. Furthermore, if there were any untracked files, they would also be referred to here.
If a new file is added to a project that did not exist previously, and then git status is run, the untracked file will appear as so:

$ vim README 
$ git status 
# On branch master 
# Untracked files: 
#   (use "git add <file>..." to include in what will be committed) 
# 
#   README nothing added to commit but untracked files present (use "git add" to track)

As the file is under the heading of “untracked files”, Git has recognised that this is a file that has not been committed in the last snapshot.

How To Track New Files

To start tracking a new file, input the command git add. For example:

$ git add README

By following this with the status command, the file is now tracked and staged (see the “changes to be committed heading”). If the file was committed now, the version of the file at the time git add was run will be in the chronological snapshot.
When git add (files) was processed earlier to begin tracking files in the directory, the git add command took a path name for a file or directory. If it is a directory, the command will include all of the directory’s files.


How to Stage Modified Files

If a previously tracked file is altered, for example, a file called benchmarks.rb and the status command is then typed, the result will look similar to the following:

$ git status 
# On branch master 
# Changes to be committed: 
#   (use "git reset HEAD <file>..." to unstage) 
# 
#   new file:   README 
# 
# Changes not staged for commit: 
#   (use "git add <file>..." to update what will be committed) 
# 
#   modified:   benchmarks.rb 
#

The file appears under a section called “changes not staged for commit”, so it is tracked and has been modified in the working directory, but as yet is not staged. To stage the file, use the git add command. Here is the outcome for running git add, to stage the file, then running git status again:

$ git add benchmarks.rb 
$ git status 
# On branch master 
# Changes to be committed: 
#   (use "git reset HEAD <file>..." to unstage) 
# 
#   new file:   README 
#   modified:   benchmarks.rb 
#

The two files are staged and will be in the snapshot on the next commit. Last minute changes can be made to the file if desired, before the commit. Re-open it, make the update, then perform git status once more. The following will occur:

$ vim benchmarks.rb 
$ git status 
# On branch master 
# Changes to be committed: 
#   (use "git reset HEAD <file>..." to unstage) 
# 
#   new file:   README 
#   modified:   benchmarks.rb 
# 
# Changes not staged for commit: 
#   (use "git add <file>..." to update what will be committed) 
# 
#   modified:   benchmarks.rb 
#


As Git stages a file identically to when the git add command was performed, this file is now in both staged and unstaged states. The version of the benchmarks.rb file saved will be the one when git add was last used, not the one in the working directory when git commit was performed, should commit be used again straight away. By applying git add again after modifying a file, the lastest file version of the file will be staged:

$ git add benchmarks.rb 
$ git status 
# On branch master 
# Changes to be committed: 
#   (use "git reset HEAD <file>..." to unstage) 
# 
#   new file:   README 
#   modified:   benchmarks.rb 
#

How to View Staged and Unstaged Changes

Use the git diff command to give a clearer depiction of what has been changed but not yet saved and what is staged but not yet committed, instead of using git status. Git diff will show precisely what has been inserted and taken out.
If the README file is edited and staged once more and the benchmarks.rb file is edited without staging, apply the status command and you will see something resembling the following:
$ git status 
# On branch master 
# Changes to be committed: 
#   (use "git reset HEAD <file>..." to unstage) 
# 
#   new file:   README 
# 
# Changes not staged for commit: 
#   (use "git add <file>..." to update what will be committed) 
# 
#   modified:   benchmarks.rb 
#

Type git diff to check what has been changed but not staged:

$ git diff 
diff --git a/benchmarks.rb b/benchmarks.rb 
index 3cb747f..da65585 100644
 --- a/benchmarks.rb
 +++ b/benchmarks.rb 
@@ -36,6 +36,10 @@ def main            	
    @commit.parents[0].parents[0].parents[0]          
	end  

+        run_code(x, 'commits 1') do 
+          git.commits.size 
+        end 

+          run_code(x, 'commits 2') do
            log = git.commits('master', 15)
            log.size

That command will evaluate what is in the working directory against what is in the staging area.

To see what is staged ready to go into the next commit, use git diff –-cached. This command contrasts the staged changes with what is in the last commit:

$ git diff --cached 
diff --git a/README b/README 
new file mode 100644 
index 0000000..03902a1 
--- /dev/null 
+++ b/README2 
@@ -0,0 +1,5 @@ 
+grit 
+ by Tom Preston-Werner, Chris Wanstrath 
+ http://github.com/mojombo/grit 
+ 
+Grit is a Ruby library for extracting information from a Git repository

How to Commit Changes

Once prepared to commit staged changes, the easiest way is by using the command:

$ git commit

This will introduce the choice of editor, which is determined by the shell’s $EDITOR environment variable (for instance, emacs or vim) although this can be set to a required variable using:

git config—global core.editor 

The editor will show:

# Please enter the commit message for your changes. Lines starting 
# with '#' will be ignored, and an empty message aborts the commit. 
# On branch master # Changes to be committed: 
#   (use "git reset HEAD <file>..." to unstage) 
# 
#       new file:   README 
#       modified:   benchmarks.rb 
~ 
~ 
~ 
".git/COMMIT_EDITMSG" 10L, 283C

The commit message includes the latest output of the git status shown as a comment below an empty line. It is possible to omit these comments and include a commit message, or leave them there as assistance in remembering what is being committed. 
To view an even more detailed reminder of the modifications, use the –v selection with git commit. This also puts the variation on the project in the editor specific changes are visible. When the editor is closed, Git produces the commit with that commit message (eliminating diff and comments).
Another method is to type a commit message adjacent to the commit command by including it following a –m flag:

$ git commit -m "Story 182: Fix benchmarks for speed" 
[master]: created 463dc4f: "Fix benchmarks for speed"  
2 files changed, 3 insertions(+), 0 deletions(-)  
create mode 100644 README 

The first commit is accomplished. The commit has constructed some information its output; that it is committed to the master branch, the SHA-1 checksum it possesses (463dc4f) is displayed, the number of altered files is revealed, and statistics on edited data in the particular commit are available.
