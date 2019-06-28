---
title: Creating a Repository
teaching: 10
exercises: 0
questions:
- "Where does Git store information?"
objectives:
- "Create a local Git repository."
keypoints:
- "`git init` initializes a repository."
- "Git stores all of its repository data in the `.git` directory."
---

Once Git is configured,
we can start using it.

We will continue with the story Puzz le Master, who is attempting to complete
the largest puzzle ever, with all the planets in our solar system. 

First, let's create a directory in `Desktop` folder for our work and then move into that directory:

~~~
$ cd ~/Desktop
$ mkdir puzzles
$ cd puzzles
~~~
{: .language-bash}

Then we tell Git to make `puzzles` a [repository]({{ page.root }}/reference#repository)—a place where
Git can store versions of our files:

~~~
$ git init
~~~
{: .language-bash}

It is important to note that `git init` will create a repository that
includes subdirectories and their files---there is no need to create
separate repositories nested within the `puzzles` repository, whether
subdirectories are present from the beginning or added later. Also, note
that the creation of the `puzzles` directory and its initialization as a
repository are completely separate processes.

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~
$ ls
~~~
{: .language-bash}

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `puzzles` called `.git`:

~~~
$ ls -a
~~~
{: .language-bash}

~~~
.	..	.git
~~~
{: .output}

Git uses this special sub-directory to store all the information about the project, 
including all files and sub-directories located within the project's directory.
In other words, the `.git` directory, is the filebox that we store our puzzle
snapshots in. If we ever delete the `.git` sub-directory,
we will lose the project's history. 
This is akin to throwing our filebox into a fire. It cannot be recovered.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .language-bash}
~~~
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

If you are using a different version of `git`, the exact
wording of the output might be slightly different.

> ## Places to Create Git Repositories
>
> Along with tracking information about puzzles (the project we have already created), 
> le Master would also like to track information about puzzle playlists.
> So, although music playlists don't directly relate to the puzzle task at hand,
> le Master creates a `playlist` project inside the `puzzles` 
> project with the following sequence of commands:
>
> ~~~
> $ cd ~/Desktop      # return to Desktop directory
> $ cd puzzles        # go into puzzles directory, which is already a Git repository
> $ ls -a             # ensure the .git sub-directory is still present in the puzzles directory
> $ mkdir playlist    # make a sub-directory puzzles/playlist
> $ cd playlist       # go into playlist sub-directory
> $ git init          # make the playlist sub-directory a Git repository
> $ ls -a             # ensure the .git sub-directory is present indicating we have created a new Git repository
> ~~~
> {: .language-bash}
>
> Is the `git init` command, run inside the `playlist` sub-directory, required for 
> tracking files stored in the `playlist` sub-directory?
> 
> > ## Solution
> >
> > No. le Master does not need to make the `playlist` sub-directory a Git repository 
> > because the `puzzles` repository will track all files, sub-directories, and 
> > sub-directory files under the `puzzles` directory.  Thus, in order to track 
> > all information about playlists, le Master only needed to add the `playlist` sub-directory
> > to the `puzzles` directory.
> > 
> > Additionally, Git repositories can interfere with each other if they are "nested":
> > the outer repository will try to version-control
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown
> > above:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .language-bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
> ## Correcting `git init` Mistakes
> Searching the internet for "nested repositories", shows le Master how a 
> nested repository is redundant and may overly complicate things. 
> le Master would like to remove the nested repository. How can le Master undo 
> the last `git init` in the `playlist` sub-directory?
>
> > ## Solution -- USE WITH CAUTION!
> >
> > ### Background
> > Removing files from a git repository needs to be done with caution. To remove files from the working tree and not from your working directory, use
> > ~~~
> > $ rm filename
> > ~~~
> > {: .language-bash}
> > 
> > The file being removed has to be in sync with the branch head with no updates. If there are updates, the file can be removed by force by using the `-f` option. Similarly a directory can be removed from git using `rm -r dirname` or `rm -rf dirname`.
> >
> > ### Solution
> > Git keeps all of its files in the `.git` directory.
> > To recover from this little mistake, le Master can just remove the `.git`
> > folder in the playlist subdirectory by running the following command from inside the `puzzles` directory:
> >
> > ~~~
> > $ rm -rf playlist/.git
> > ~~~
> > {: .language-bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire Git history of a project you might want to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}
