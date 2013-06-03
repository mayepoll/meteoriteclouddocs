meteoriteclouddocs
==================
This documentation will give some background information on what Git software is, its purpose, and how to use Git for updating data sets. By the end of this section, you should have a better idea of Git functionality and how to go about depositing and extracting data on Git repositories.
Git Software and Meteorite Cloud
The Meteorite Cloud solution uses Git software on servers that, in some cases, users create to upload data. The software is a means of storing the latest version of that data, as well as any previous versions that the user may want to refer to at a later stage. This documentation will guide users in setting up a data repository and making changes to it.
What is Git?
Git is essentially a software provider, producing open source and free version control software designed for the updating of data. The concept of version control records changes to data or sets of data over time, using any file type. Anything from a simple text file, to more complex types such as spreadsheets can be updated using version control. Version control systems have traditionally been fairly troublesome due to reliability issues, but Git aims to eliminate these problems by using a slightly different approach, which this documentation details later.

Why Use Version Control?

The main advantages of version control are:

• Being able to dig out a version of a file from a previous state, particularly useful for solving discrepancies;
•	The ability to see who last made a change to something that may be causing a problem;
•	The capability to regress the whole of a project back to a previous state.

Information can usually be recovered if something goes wrong or it is lost. 

What Makes Git Functionality Different to Other Providers’?

Basic version control programmes may involve backing up files in another directory. This method is fairly unreliable as it is easy to write the wrong file, copy the wrong files over by accident and it’s easy to forget which directory you’re working in.
In a bid to counteract these potential problems, programmers developed local version control systems containing simple databases that kept all changes to files under version control. A popular tool was a system called RCS that works by storing patch sets (the differences between files) in a unique format on disk. If required it can then recreate an exact replica of the file at any point in time. 
As advancement to this concept, centralised version control systems were developers to collaborate with other editors on other systems. This type of system has a single server containing all versions of files, and allows a number of clients to check out (output) files from that centralised place.
Git software goes one step further and incorporates distributed version control systems, where clients no only check out the latest snapshots (saved versions) of files, they fully mirror the repository. This means that if any server ceases to function, and various systems were collaborating via it, any of the client repositories can be copied back to the server to restore any lost data. Each checkout is effectively a complete back up of all the data. Other plus points are that administrators have tight control over who can do what, and its easier to administrate than local databases for every editor.

How Does Git Software Operate?

Git software is also designed so that several remote repositories can be operated at one time, so you can collaborate with different groups of people in different ways at the same time on the same data/project, and various types of workflow can be set up, for example, hierarchical models.
The key difference to the way in which data is stored using Git to the more historical methods is that Git considers data more like snapshots of a file system, rather than information kept as a set of files that are individually changed over time. This can be illustrated by using the example of taking a photograph of the same scene over different times of the year; one picture might show an autumnal scene with orange and red leaves, while another may show snow on the ground. 
Git will store a reference to these ‘pictures’ and can detect if files have changed or not. If they haven’t, Git won’t store the file, but instead link to the previous identical file it already has stored.
The software is highly flexible, in that if you want to work on a file while away from an internet connection, you can work offline and any changes made can be uploaded and made once you reach a connection.
All data in Git is check summed before it’s stored and is then referred to using the checksum. This means you cannot change a file’s contents without Git recording it.

The Basics of Git in Relation to Repositories

Before creating or importing a repository, it’s important to understand that there are three states that projects can exist in: committed, modified and staged. 

•	Committed means that the data is saved in your local database; 
•	Modified means that you have changed the file but it is not yet committed to your database;
•	Staged means that you have earmarked a modified file in its current version to go into your next commit snapshot.

There are also three main sections of a Git project:

•	The Git directory is where Git stores the metadata and object database of the project. This is what is copied if you were to clone a repository from another computer.
•	The working directory is a single checkout of one version of the project. These files can be extracted from the compressed database in the Git directory and transferred to disk for use or modification.
•	The staging area acts as a workspace that stores information about what will go into your next commit.

In summary, files can be modified in the working directory, then you add snapshots of them in your staging area, then you commit, taking the files in the same state they were in in the staging area, storing the snapshot permanently in your Git directory.
If a particular version of the file is in the Git directory, it’s committed. If it’s modified and added to the staging area, it’s staged, and if it’s been changed since it was checked out but not staged, then it is modified.

How Do You Get a Data Repository?

The repository is where all the data and snapshots are held for a particular project. There are two main ways in which to get a repository. These are:

1.	Taking an existing project or directory and importing it into Git.
2.	The second clones an existing Git repository from another server.

Using An Existing Project
If you want to start recording an existing project in Git, go to the project’s directory and type the following:

    $ git init

This creates a subdirectory named .git containing all necessary repository files in a Git repository skeleton. It is wise to do an initial commit if you want to start tracking an existing project.  To do this, use the following Git add commands that include the files you want to track, then add a commit:

    $ git add *.c
    $ git add README
    $ git comit –m ‘initial project version’

You now have a Git repository containing tracked files and an initial commit.

Cloning an Existing Repository

If you want to contribute to an existing project, you can make a copy of an existing Git repository. You need the following command:

    git clone

This will copy every version of every file for the history of a project.

You clone a repository with git clone [url]. For instance, to clone the Ruby Git library called Grit, use the following command:

    $ git clone git://github.com/schacan/grit.git

This will create a directory called grit, initialises a .git directory inside it, clones all the data for that repository, and checks out a working copy of the latest version.
To copy the repository into a directory called something different, you can specify that on the next command line using:

    $ git clone git://git hub.com/schacan/grit.git mygrit
    Committing Changes to the Repository

Every file in your working directory can either be tracked or untracked. Tracked files are files that were in the last snapshot, which can be unmodified, modified or staged. Untracked files are all other files that are not in your last snapshot or in your staging area. When a project is first cloned, all files will be tracked and unmodified because you checked them out and haven’t yet edited them.
Every time you wish to make an edit, Git sees this a modifying files as you’ve changed them since your last commit. You stage these modified files then commit your staged changes. The cycle then repeats itself.

How to Check the Status of Your Files

Using the git status command, you can check which files are in which state. If you run this command straight after a clone, you should see this:

    $ git status
    # On branch master
    nothing to commit (working directory clean)

This means no tracked files are modified. If there were any untracked files, they would also be listed here.

If you add a new file to your project, for example a README file, and you run git status, you’ll see your untracked file like this:

    $ vim README 
    $ git status 
    # On branch master 
    # Untracked files: 
    #   (use "git add <file>..." to include in what will be committed) 
    # 
    #   README nothing added to commit but untracked files present (use "git add" to track)

The README file is untracked because it’s under the “untracked files” files heading in your status output. This means that Git has seen a file that you did not commit in your previous snapshot, because it’s new.

How To Track New Files

To start tracking a new file, run the command git add. So to start tracking the new README file run:

    $ git add README

If you run the status command now, you can see that your README file is now tracked and staged (see the “changes to be committed heading”). If you commit now, the version of the file at the time you ran git add will be in the historical snapshot.
When you ran git init earlier, you then ran git add (files) to begin tracking files in your directory. The git add command takes a path name for a file or directory. If it’s a directory, the command adds all the files in the directory.

How to Stage Modified Files

If you change a previously tracked file, for example, a file called benchmarks.rb and then run the status command, you will see something like this:

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

The benchmarks.rb file appears under a section called “changes not staged for commit”, meaning a file that has been tracked has been modified in the working directory, but not yet staged. To stage the file, run the git add command. Here is the outcome for running git add, to stage benchmarks.rb, then run git status again:

    $ git add benchmarks.rb 
    $ git status 
    # On branch master 
    # Changes to be committed: 
    #   (use "git reset HEAD <file>..." to unstage) 
    # 
    #   new file:   README 
    #   modified:   benchmarks.rb 
    #

Both files are staged and will now go into your next commit. At this point you can still make a last minute change that you want to make to the file before you commit it. Open it again, make the change, then run git status once more. You will see something like this:

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


Now benchmarks.rb is listed as both staged and unstaged. In this instance, Git stages a file exactly as it is when you ran the git add command. If you were to commit now, the version of benchmarks.rb will be the one when you last ran git add, not the version of the file as it looks in your working directory when you ran git commit. If you modify a file after running git add, you have to run git add to stage the lastest version of the file:

    $ git add benchmarks.rb 
    $ git status 
    # On branch master 
    # Changes to be committed: 
    #   (use "git reset HEAD <file>..." to unstage) 
    # 
    #   new file:   README 
    #   modified:   benchmarks.rb 
    #

How to View Your Staged and Unstaged Changes

By using the git diff command, it will  give you a better idea than using git status for seeing what you have changed but not yet saved and what you have staged but not yet committed. Git diff will show you the exact lines added and removed (or the patch).
If you edit and stage the README file once more and edit benchmarks.rb file without staging it, run the status command and you will see something resembling this:

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

To see what you’ve changed but not staged, type git diff:

    $ git diff 
    diff --git a/benchmarks.rb b/benchmarks.rb 
    index 3cb747f..da65585 100644
     --- a/benchmarks.rb
     +++ b/benchmarks.rb 
    @@ -36,6 +36,10 @@ def main            	@commit.parents[0].parents[0].parents[0]          
    	end  

    +        run_code(x, 'commits 1') do 
    +          git.commits.size 
    +        end 

    +          run_code(x, 'commits 2') do
                log = git.commits('master', 15)
                log.size

That command will compare what’s in your working directory with what’s in your staging area.

To see what you’ve staged that will go in your next commit, use git diff –-cached. This command compares the staged changes to your last commit:

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

How to Commit Your Changes

Once you are ready to commit your staged changes, the easiest way to commit these changes is by using the command:

    $ git commit

Doing this launches your editor of choice. This is set by your shell’s $EDITOR environment variable (normally vim or emacs) although this can be configured to your desired variable using:

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



As you can see, the default commit message includes the latest output of the git status commented out and one empty line above it. You can remove these comments and type a commit message, or leave them there to assist you in remembering what you’re committing. 
If you need an even more detailed reminder of your modifications, pass the –v option to git commit. Doing this also puts the differences of your project in the editor so you can see exactly what you’ve changed. When you come out of the editor, Git creates your commit with that commit message (with the comments and differences removed).
Another option is to type your commit message in line with the commit command by specifying it after a –m flag, like this:

    $ git commit -m "Story 182: Fix benchmarks for speed" 
    [master]: created 463dc4f: "Fix benchmarks for speed"  
    2 files changed, 3 insertions(+), 0 deletions(-)  
    create mode 100644 README 

Now you have completed your first commit. As you can see, the commit has given you some output about itself; which branch it has committed to (master), what SHA-1 checksum the commit has (463dc4f), how many files have been changed and statistics about data edited in the commit.








