Learning Git
================
Ada Hagan
January 9, 2019

## General Notes to Self:

  - Slow down
  - Always have learners tell you the commands you should use (or what
    the next step might be) – use the etherpad to help gauge how
    comfortable the students are with a command
  - Always write/draw commands if I don’t type them
  - Ensure at least two examples for each concept – maybe less for
    add/commit to create more time for Github
  - Create/find at least one exercise for each concept
  - Work to tie the lesson in with previously learned concepts, e.g.,
    UNIX & R
  - Have the learners confirm that they’re in the right working
    directory after every exercise\!\!
  - iterate that when they do come up with a question, they should ask
  - try to hide responses on the etherpad until everyone has answered

## Setup

  - Start with a fresh planets repo
  - Spend first 5 minutes allowing learners to pull up/create github
    accounts & open their command line.
  - Link to SWC Git notes: <https://swcarpentry.github.io/git-novice/>
  - Put the following list of commands in the etherpad – learners add a
    “+” when they’re tired of hearing them 50% means I quit making
    them tell me
      - nano <filename>
      - saving & closing nano
      - cd <directory>
      - ls
      - cat <filename>
      - mkdir <directory>
      - touch <filenames>
      - git add
      - git commit -m “message”
      - git status

## Outline

  - What is Git?
  - How to make your filebox (setup & init)
  - How to add snapshots to your filebox (add, commit)
  - How to track changes between versions (diff, log)
  - How to restore a previous version (checkout)
  - How to choose what to track & what not to track (.gitignore)
  - How to share your filebox with others (github, pull, push)
  - How to collaborate with others (clone)
  - How to resolve collaborative conflicts (merge, branch)

## What is Git?

**It’s very important that the learners fully understand this
concept\!\! If they don’t, the rest doesn’t matter.**

Imagine that you have a very large (\>2k piece) puzzle that you want to
put together, but you don’t have a picture, so you have no idea what
this puzzle is supposed to look like when it’s done. So you clear off
the dining room table and get to work. Because you know that this is
going to take you weeks or months to finish, you decide to take
polaroids to track your progress. One day, some poor unknowing soul
decides to “help” you with the puzzle (maybe your cat, toddler, or drunk
self…). The next morning you walk in and the puzzle is a wreck\!\! What
do you do?

Go back to the polaroids\!\!

This process of taking “snapshots” of your work and storing them ***is
git***\!\!

The way git works is that each time you stop working, you take a
snapshot, label it, and put it in your filebox for later. Because you
can’t keep multiple puzzles in varying stages of completion in your
closet, each photo contains the *differences* between versions, not the
actual old versions. This means that git can take you from the original
to version 4, back to 2, etc.

Connect the puzzle concept to git language: e.g, staging == taking a
snapshot; committing == putting the snapshot in the filebox/repository

What we’re going to spend the rest of our time this morning/afternoon
doing, is learning how to use git: how to create a filebox, take and add
snapshots, compare the differences between snapshots & choosing what you
want to make snapshots of versus not. We’ll also extend this puzzle
analogy to talk about how you can share your project progress with
others and even collaborate together.

On a command line, Git commands are written as `git verb options`, where
we tell the computer that we want to use the `git` program, and perform
the `verb` action, which might be modified using `options`.

## How to make your filebox (setup & init)

When we use Git on a new computer for the first time, we need to
configure a few things: + our name and email address, + what our
preferred text editor is, + and that we want to use these settings
globally (i.e. for every project).

    $ git config --global user.name "Vlad Dracula"
    $ git config --global user.email "vlad@tran.sylvan.ia"

**-Line Endings**

You can change the way Git recognizes and encodes line endings using the
`core.autocrlf` command to `git config`. The following settings are
recommended:

  - On macOS and Linux:
    
    `$ git config --global core.autocrlf input`

  - And on Windows:
    
    `$ git config --global core.autocrlf true`

**- Text editor**

nano `$ git config --global core.editor "nano -w"`

**- Getting help & changing options**

Remember that if you mess up any of the `git config` options, you can
change them by entering the same command with corrected/different
options

Always remember that if you forget a `git` command, you can access the
list of commands by using `-h` and access the Git manual by using
`--help`:

    $ git config -h
    $ git config --help

**- Initializing a directory (creating the filebox)**

1.  Create the `planets` directory on your desktop.

2.  `cd` to the planets directory

3.  Initialize the repository: `git init`

4.  No readout did it work? Check `ls`

5.  Also nothing, try `ls -a`

6.  The `.git` file ***is the filebox*** **DO NOT TOUCH**

7.  `git status` – what does this mean?

-----

**Exercise:**

Create a filebox for the project that you started in your Unix Shell
lesson (`data-shell/`).

-----

## How to add snapshots to your filebox (add, commit)

1.  Navigate back to `planets/`

2.  Create the file `mars.txt`

3.  Populate with a single line.

4.  Save & Exit

5.  `ls` and `cat`

6.  `git status` – now what is it telling me?

7.  `git add mars.txt` – take the snapshot

8.  `git status`

9.  `git commit -m "start notes on Mars"` – label & put photo in filebox
    (this action uses the text.editor you indicated earlier to create
    these commit messages)

10. Break down the output – hexcode/barcode

11. `git status`

-----

**Think/pair/share:**

Which command(s) below would save the changes of `myfile.txt` to my
local Git repository?

1.  `$ git commit -m "my recent changes"`

2.  `$ git init myfile.txt` `$ git commit -m "my recent changes"`

3.  `$ git add myfile.txt` `$ git commit -m "my recent changes"`

4.  `$ git commit -m myfile.txt "my recent changes"`

-----

**Exercise:**

Create a text file and write everything you remember so far about git.

Take a snapshot and put it in your filebox.

-----

## How to track changes between versions (diff, log)

1.  We can view all of our previous commits using the command `git log`.
    What info has this given me?

2.  Let’s add another line to `mars.txt` (Make learners walk you through
    it\!).

3.  Before adding, let’s compare the changes we made to the old version
    `git diff`. What is this telling me?
    
      - The output is cryptic because it is actually a series of
        commands for tools like editors telling them how to reconstruct
        one file given the other. If we break it down into pieces:
    
    <!-- end list -->
    
    1.  The first line tells us that Git is comparing the old and new
        versions of the file.
    2.  The second line tells exactly which versions of the file Git is
        comparing; `df0654a` and `315bf3a` are unique computer-generated
        labels for those versions.
    3.  The third and fourth lines once again show the name of the file
        being changed.
    4.  The remaining lines are the most interesting, they show us the
        actual differences and the lines on which they occur. In
        particular, the `+` marker in the first column shows where we
        added a line.

4.  Let’s `add` it to the staging area.

5.  What happens if we use `git diff` now? Try `git diff --staged`

6.  Now let’s `commit`

7.  Now what does `git log` give me?

8.  That’s a lot of info to view in a single terminal, try `git log
    --oneline`.

9.  Open the `git log` help manual, how do I do that? Here you can see
    that there are a lot of options for searching through all of the
    commits that might occur during a project, including keywords, date
    ranges, and author.

10. Use the break to add a `.dat` file to the repo to help demonstrate
    the `.gitignore` file in the next section.

-----

**Think/pair/share:**

Consider this command: `git diff [ID] mars.txt`, where \[ID\] is
replaced with the unique identifier for your most recent commit. What do
you predict this command will do if you execute it? What happens when
you do execute it? Why?

-----

**Exercise:**

Update your Git notes text file. Commit the updated file and view the
changes using `git diff`, `git diff --staged` and `git log` at the
appropriate steps. Which do you prefer? Why?

## How to restore a previous version (checkout)

**Summarize:**

At this point we’ve learned:

  - How to create the file box (`git init`)
  - How to stage files/take a snapshot (`git add`)
  - How to put the snapshots in a box/commit files (`git commit`)
  - How to view differences between files that have (`git diff
    --staged`) and have not (`git diff`) been staged
  - How to view all of our previous commits (`git log`)

Now let’s learn how to restore previous versions of a file using the
command `git checkout`.

There are two different ways to reference previous file versions in git:
the barcode that I’ve been pointing out to you and “HEAD”. The barcode
is specific to each commit, while head is a generic term that allows you
to work with recent commits w/o digging out the barcode.

The most recent commit is termed the “HEAD”, and each previous commit is
head tilda some number, e.g., HEAD\~1, HEAD\~2, HEAD\~3, etc.

Use `git diff HEAD~2 mars.txt` to demonstrate.

That method can be a bit abstract (& kinda stressful) so another option
is to use the barcode.

Let’s put this to work, we’re going to make changes to mars.txt & create
a new file, which we’ll commit and then make more changes to commit,
that way we have options to use `git checkout` with:

1.  Modify `mars.txt` and create `venus.txt`.

2.  Add & Commit both files (demonstrates how to stage & commit multiple
    files at a time, use `-a` to create a longer commit message)

3.  Modify `venus.txt`, `cat`

4.  Let’s revert to the previous version of `venus.txt` how can we do
    that using “HEAD”? `git checkout HEAD venus.txt`

5.  Check reversion `cat`

6.  Modify `venus.txt` again, stage & commit.

7.  Revert to the previous versions of both mars & venus.txt `git
    checkout ____` – should result in detached head

8.  Fix with `git checkout master`

9.  Try it again `git checkout ____ mars.txt venus.txt`

-----

**Think/pair/share:** Jennifer has made changes to the Python script
that she has been working on for weeks, and the modifications she made
this morning “broke” the script and it no longer runs. She has spent \~
1hr trying to fix it, with no luck…

Luckily, she has been keeping track of her project’s versions using
Git\! Which commands below will let her recover the last committed
version of her Python script called `data_cruncher.py`?

1.  `$ git checkout HEAD`

2.  `$ git checkout HEAD data_cruncher.py`

3.  `$ git checkout HEAD~1 data_cruncher.py`

4.  `$ git checkout <unique ID of last commit> data_cruncher.py`

5.  `Both 2 and 4`

-----

**Exercise**

Restore the previous version of Git notes.

-----

## How to choose what to track & what not to track (.gitignore)

**- Adding to the puzzle analogy**

So going back to our puzzle analogy, are there important piece to your
project that you don’t want to take snapshots of? Maybe because they
don’t change or if they do, then the changes aren’t helpful to track?
Consider the box you store pieces in? Or the pieces that are still
unmatched at the end of a puzzle session? Or the puzzle playlist that
you always use. Or the table you work on?

Because you’re physically holding the camera, you get to choose what
makes sense to track & what doesn’t. But git doesn’t know that on it’s
own. You have to specifically tell git what you DO NOT want snapshots
of.

Sometimes you’re going to have important files that you don’t want to
track changes on, either they’re too big, they don’t change (e.g., data
files) or their changes aren’t recorded by git (e.g., word files).

You can communicate this to Git by creating a text file called
`.gitignore` that tells git what NOT to track. To illustrate this, we’re
going to create a new directory within `planets/` called `moons/` that
contains data files.

1.  Create `moons/`

2.  Populate with `.dat` files and one `.txt` file

3.  Create `.gitignore` text file, add all `.dat` files. – ideally this
    is in your home directory for the project

4.  View `git status`

5.  Stage and view `git status` – discuss why the `.dat` created earlier
    is still staged, unstage it

6.  Commit changes

7.  Add `moons/` to `.gitignore`

8.  View `git status`

9.  Stage, view `git status`, and commit

-----

**Think/pair/share:** Given a directory structure that looks like:

    results/data
    results/plots

How would you ignore only `results/plots` and not `results/data`?

-----

1.  You can view ignored files with `git status --ignored`

2.  Override `.gitignore` using `git add -f ____`

-----

**Think/pair/share:**

You wrote a script that creates many intermediate log-files of the form
`log_01`, `log_02`, `log_03`, etc. You want to keep them but you do not
want to track them through git.

1.  Write one `.gitignore` entry that excludes files of the form
    `log_01`, `log_02`, etc.

2.  Test your “ignore pattern” by creating some dummy files of the form
    `log_01`, etc.

3.  You find that the file `log_01` is very important after all, add it
    to the tracked files without changing the `.gitignore` again.

4.  Discuss with your neighbor what other types of files could reside in
    your directory that you do not want to track and thus would exclude
    via `.gitignore`.

-----

**Exercise:**

Create a `.gitignore` file for the `data-shell/` directory. Tell it to
ignore `.pdb`, `.xml`, and `.dat` files. `Add` and `commit` the contents
of `data-shell/`. What files/directories don’t get committed? Why not?

## How to share your filebox with others (github, pull, push)

**Extending the puzzle analogy:** What if you’re really proud of this
puzzle, or you want a backup of your filebox (since it’s only as safe as
your house is…)? Well, you could scan those polaroids into your computer
then upload them to a website (e.g., mypuzzles.com), where each puzzle
has it’s own webpage that contains the scanned versions of your
snapshots that anybody can view\! This “website” is github.

Github is a website that can house each of your fileboxes and allow
other researchers to check out your code as well as acting as a cloud
version of your repository. Why does this matter?

There’s a push for open science, where instead of only telling
scientists what your interpretation of your data is, you also make the
data avilable for them to check your work. When using programs such as R
or python to do your calculations (insted of within excel), you can also
make your code available for other researchers.

**-Starting a remote repository**

1.  Login to GitHub

2.  Click on the `+` icon in the top right corner to create a new repo –
    call it `planets/`

3.  Options:
    
      - README - summary of repo for others to read
      - .gitignore - no, b/c the repo already exists on your desktop
      - license - legal protection of author/creatorship see a later
        section for discussion

4.  Click `create repository`

5.  Follow instructions to push an existing repo from the command line:
    (walk through these commands)

<!-- end list -->

    git remote add origin [URL] #check after this step w. git remote -v
    git push -u origin master #uploads repo to github & sets option so that you only have to use pull/push from now on

-----

**Think/pair/share:**

In this lesson, we introduced the “git push” command. How is “git push”
different from “git commit”?

**Think/pair/share:**

It happens quite often in practice that you made a typo in the remote
URL. This exercise is about how to fix this kind of issue. First start
by adding a remote with an invalid URL:

    git remote add broken https://github.com/this/url/is/invalid

Do you get an error when adding the remote? Can you think of a command
that would make it obvious that your remote URL was not valid? Can you
figure out how to fix the URL (tip: use `git remote -h`)? Don’t forget
to clean up and remove this remote once you are done with this exercise.

*Solution: We don’t see any error message when we add the remote (adding
the remote tells git about it, but doesn’t try to use it yet). As soon
as we try to use git push we’ll see an error message. The command* `git
remote set-url` *allows us to change the remote’s URL to fix it.*

|                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------- |
| **Exercise:**                                                                                                   |
| Set up and push your `data-shell/` repository to your github account. Explore the online track changes options. |

## How to collaborate with others (clone)

**Extending the puzzle analogy again:** What if you have a best friend
across the country and you’re both going to work on the puzzle together.
So your friend buys a copy of the same puzzle to set up in their dining
room. How do you work together on it and share the progress? Through
your puzzles.com\!

First, your friend uses one of your snapshots (maybe the border pieces)
to start putting her puzzle togther, then you work on the top left
corner while they work on the bottom right corner. Then she sends
snapshots and **IF** you agree, you can merge her results into your own
puzzle.

On git, this process of collaboration uses github. By making a clone of
your project repository and then working on it and making their own
commits, they create a “branch” of the project. When they make commits,
you have the option to accept or reject their changes. If you reject, it
stays separate. If you accept, then you can “MERGE” their changes with
your master branch.

`git clone` copies a remote repository to create a local repository with
a remote called `origin` automatically set up.

**- Collaborating with a Partner**

1.  Find a partner

2.  Add your partner as a “Collaborator” on the Settings tab by adding
    their GitHub user name

3.  Partner accepts on their GitHub Notifications page

4.  Partner (collaborator) downloads a copy of the Owner’s repo to their
    desktop \`git clone \[URL\].git \~/Desktop/\[Owner\]-planets

5.  Collaborating partner makes a change in her cloned copy of the repo:

<!-- end list -->

    cd ~/Desktop/vlad-planets
    nano pluto.txt
    cat pluto.txt
    git add pluto.txt
    git commit -m "Add notes about Pluto"

1.  Push change to the Owners GitHub repo: `git push origin master`

2.  Owner partner should refresh their GitHub account – can you find the
    changes?

3.  Owner downloads Collaborator’s changes: `git pull`

**A Basic Collaborative Workflow** In practice, it is good to be sure
that you have an updated version of the repository you are collaborating
on, so you should `git pull` before making your changes. The basic
collaborative workflow would be:

  - update your local repo with `git pull origin master`,
  - make your changes and stage them with `git add`,
  - commit your changes with `git commit -m`, and
  - upload the changes to GitHub with `git push origin master`

It is better to make many commits with smaller changes rather than of
one commit with massive changes: small commits are easier to read and
review

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Think/pair/share:** The Owner pushed commits to the repository without giving any information to the Collaborator. How can the Collaborator find out what has changed with command line? And on GitHub?                                                                                                                                                                                                                                                                                                                                              |
| *Solution: On the command line, the Collaborator can use git fetch origin master to get the remote changes into the local repository, but without merging them. Then by running git diff master origin/master the Collaborator will see the changes output in the terminal.*                                                                                                                                                                                                                                                                           |
| *On GitHub, the Collaborator can go to their own fork of the repository and look right above the light blue latest commit bar for a gray bar saying “This branch is 1 commit behind Our-Repository:master.” On the far right of that gray bar is a Compare icon and link. On the Compare page the Collaborator should change the base fork to their own repository, then click the link in the paragraph above to “compare across forks”, and finally change the head fork to the main repository. This will show all the commits that are different.* |
| **Exercise:** Switch roles and repeat the whole process.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

## How to resolve collaborative conflicts (merge, branch)

As soon as people can work in parallel, they’ll likely step on each
other’s toes. This will even happen with a single person: if we are
working on a piece of software on both our laptop and a server in the
lab, we could make different changes to each copy. Version control helps
us manage these conflicts by giving us tools to resolve overlapping
changes.

To see how we can resolve conflicts, we must first create one. The file
`mars.txt` currently looks like this in both partners’ copies of our
planets repository:

    $ cat mars.txt

Let’s add a line to one partner’s copy only:

    $ nano mars.txt
    $ cat mars.txt

and then push the change to GitHub:

    $ git add mars.txt
    $ git commit -m "Add a line in our home copy"
    $ git push origin master

Now let’s have the other partner make a different change to their copy
without updating from GitHub:

    $ nano mars.txt
    $ cat mars.txt

We can commit the change locally:

    $ git add mars.txt
    $ git commit -m "Add a line in my copy"

but Git won’t let us push it to GitHub:

    $ git push origin master
    
    To https://github.com/vlad/planets.git
     ! [rejected]        master -> master (non-fast-forward)
    error: failed to push some refs to 'https://github.com/vlad/planets.git'
    hint: Updates were rejected because the tip of your current branch is behind
    hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
    hint: before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.

Git rejects the push because it detects that the remote repository has
new updates that have not been incorporated into the local branch. What
we have to do is pull the changes from GitHub, merge them into the copy
we’re currently working in, and then push that. Let’s start by pulling:

The git pull command updates the local repository to include those
changes already included in the remote repository. After the changes
from remote branch have been fetched, Git detects that changes made to
the local copy overlap with those made to the remote repository, and
therefore refuses to merge the two versions to stop us from trampling on
our previous work. The conflict is marked in in the affected file: `cat
mars.txt`

Our change is preceded by `<<<<<<< HEAD`. Git has then inserted
`=======` as a separator between the conflicting changes and marked the
end of the content downloaded from GitHub with `>>>>>>>`. (The string of
letters and digits after that marker identifies the commit we’ve just
downloaded.)

It is now up to us to edit this file to remove these markers and
reconcile the changes. We can do anything we want: keep the change made
in the local repository, keep the change made in the remote repository,
write something new to replace both, or get rid of the change entirely.
Let’s replace both.

To finish merging, we add `mars.txt` to the changes being made by the
merge and then commit.

    git add mars.txt
    git status
    git commit -m "Merge changes from GitHub"

What happens when the collaborator pulls the changes?

It’s already been merged, so it doesn’t have to be done again.

-----

**Think/pair/share**

You sit down at your computer to work on a shared project that is
tracked in a remote Git repository. During your work session, you take
the following actions, but not in this order:

  - *Make changes* by appending the number `100` to a text file
    `numbers.txt`
  - *Update remote* repository to match the local repository
  - *Celebrate* your success
  - *Update local* repository to match the remote repository
  - *Stage changes* to be committed
  - *Commit changes* to the local repository

In what order should you perform these actions to minimize the chances
of conflicts? Put the commands above in order in the action column of
the table below. When you have the order right, see if you can write the
corresponding commands in the command column. A few steps are populated
to get you started. order action . . . . . . . . . . command . . . . . .
. . . .

    1        
    2                                     echo 100 >> numbers.txt
    3        
    4        
    5        
    6       Celebrate!                    AFK

**Exercise:**

Clone the repository created by your instructor. Add a new file to it,
and modify an existing file (your instructor will tell you which one).
When asked by your instructor, pull her changes from the repository to
create a conflict, then resolve it.

## What else do you need to know?

There are a few other sections on Git & GitHub that we aren’t going to
go indepth on, but you might be interested in reading:

  - Open Science
  - Licensing
  - Citations
  - Hosting
  - Using Git from R studio
