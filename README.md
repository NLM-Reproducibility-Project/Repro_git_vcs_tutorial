Git and Version Control
=======================

[NLM 2018 REPRODUCIBILITY WORKSHOP](https://nlm-repro.github.io/)

[Keith Hughitt](keith.hughitt@nih.gov)
2018-09-24

Outline
-------

- [Overview](#overview)
    - Intro to version control systems (VCS)
    - Why is VCS useful?
- [Git Basics](#git-basics)
    - Installation
    - Six most useful git commands to know
        1. Creating a new repo (git init)
        2. Checking a repo's status (git status)
        3. Saving changes (git commit)
        4. Pushing your changes to a remote repo (git push)
        5. Pulling changes made to a remote repo (git pull)
        6. Downloading a copy of a remote repo (git clone)
- [GitHub Basics](#github-basics)
    - Overview
    - Why use GitHub?
    - Single-user Workflow
    - Multi-user Workflow
    - Setting up the master and forked repos
    - Making changes
    - Accepting changes
    - Other multi-user workflows
- [Beyond just code](#beyond-just-code)
- [Further reading](#further-reading)

Overview
--------

The goal of this tutorial is to familiarize the user with the basics of version control (VCS),
[Git](http://git-scm.com/) and [GitHub](https://github.com/). 

Of course, there are already numerous tutorials which do this and do a much
better job than I could hope to do, e.g.:

- [Git - gittutorial Documentation](http://git-scm.com/docs/gittutorial)
- [Try Git: Code School](http://try.github.io/levels/1/challenges/1)
- [Set Up Git · GitHub Help](https://help.github.com/articles/set-up-git)
- [GitHub For Beginners: Don't Get Scared, Get Started](http://readwrite.com/2013/09/30/understanding-github-a-journey-for-beginners-part-1)

I would encourage people to check these out as well.

Here I am just going to try and cover enough to get people started and 
hopefully interested enough to try it out and learn more.

## Intro to version control systems (VCS)

Version control systems (VCS) are software tools used to track changes to a
collection of files and directories and to aide in collaborative development.
VCS is most widely used in the context of software development for tracking
changes to code, but it can also be used to track changes to other types of
work such as manuscripts, data, etc.

Some popular examples include:

- Concurrent Versions System (CVS)
- Subversion (SVN)
- Git
- Mercurial

Although the big picture is generally the same for each of these, and using
any of them is going to be better than using none, there are some differences
in the philosophy and function of each.

CSV and SVN were developed first, and are *centralized* version control
systems. This means that there is a master codebase, and client hosts which
"checkout" pieces of this code to make changes.

Newer VCS, including the later three listed above, follow a different approach
called *distributed* VCS (dVCS). In this model there is no central repository
-- all clients have an entire copy of the repository.

Both approaches have their advantages and disadvantages. The focus in this
tutorial, however, is on one of the dVCS: git.

## Why is VCS useful?

Some of the main uses for VCS include:

- Tracking changes (imagine not having an undo button in Word...)
- Backing up code or other files (Mirroring on GitHub, etc.)
- Experimentation (branches)
- Collaboration

Git Basics
----------

## Installation

Download and install Git from
[git-scm.com](http://git-scm.com/book/en/Getting-Started-Installing-Git).

## Six most useful git commands to know

This is 99% of what you need to know to use Git:

1. git init
2. git status
3. git commit
4. git push
5. git pull

## 1. Creating a new repo (git init)

To create a new git repository, simply enter the root directory which you want
to make a repo and run `git init`:

```bash
$ mkdir test
$ cd test 
$ git init
Initialized empty Git repository in /home/username/test/.git/
$
```

## 2. Checking a repo's status (git status)

It's always a good idea before making a commit to check the status of a repo
before making any changes using `git status`:

```bash
$ touch newfile
$ echo 'Hello World' > newfile 
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    newfile

nothing added to commit but untracked files present (use "git add" to track)
$ git add .
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   newfile
$
```

## 3. Saving changes (git commit)

Once you have done something interesting, `commit` it!

```bash
$ git commit -m 'Important change #1'
[master (root-commit) 9c5205a] Important change #1
 1 file changed, 1 insertion(+)
 create mode 100644 newfile
$ 

Only the changes that you have stages (using `git add`) will be included in
the commit. To include all changes made to files in the repo, you can use
`git commit -am`.
```

## 4. Pushing your changes to a remote repo (git push)

Once you have committed some changes, you may want to sync them with a remote
repository such as GitHub. This is done using the `git push` command.

```bash
$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 232 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:khughitt/test-repo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
$
```

Note that for this to work, you must first create a remote repo and add a
reference to it. We will come back to this part later...

## 5. Pulling changes made to a remote repo (git pull)

Once you start to collaborate with other people, you will need a way to sync
your repo when other people have made changes to the shared repo.

This is done using the `git pull` command.

```bash
$ git pull
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From github.com:khughitt/test-repo
   9c5205a..1336440  master     -> origin/master
Updating 9c5205a..1336440
Fast-forward
 README.md | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 README.md
$ 
```

## 6. Downloading a copy of a remote repo (git clone)

Finally, you may come across code or other files hosted in an online repo (usually on Github) that
you wish to download and possibly make changes to. The command to do so is `git clone`:

```bash
git clone https://github.com/khughitt/labnote                                    
Cloning into 'labnote'...
remote: Counting objects: 763, done.
remote: Total 763 (delta 0), reused 0 (delta 0), pack-reused 763
Receiving objects: 100% (763/763), 1.90 MiB | 3.95 MiB/s, done.
Resolving deltas: 100% (382/382), done.
```

The above command downloads the [khughitt/labnote](https://github.com/khughitt/labnote) repository
from Github over https, and stores it on your local machine. By default, it will be saved in your
current working directory in a directory with the same name as the repo (here, `labnote`).

GitHub Basics
-------------

## Overview

[GitHub](https://github.com) is a free online mirroring service for git 
repositories. It hosts mostly open source code, although you can also pay to 
have "private" repositories.

## Why use GitHub?

- Backup your code
- Share your code
- Collaboration
- Online code viewing/editing
- Browsable [commit history](https://github.com/pydata/pandas/commits/master)
- Integrates with [other services](http://developer.github.com/v3/repos/hooks/)
- Renders [Markdown](http://daringfireball.net/projects/markdown/)
- Host websites (e.g. [NLM 2018 REPRODUCIBILITY WORKSHOP](https://nlm-repro.github.io/))
- Host [HTML5 presentations](http://karthik.github.io/git_intro/#/slide-title)
- Host R packages ([devtools::install_github](https://www.rdocumentation.org/packages/devtools/versions/1.13.6/topics/install_github))
- Host Python packages ([pip](https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support))
- Repo [statistics](https://github.com/pydata/pandas/graphs/contributors)

Single-user Workflow
--------------------

For small projects or scripts that you would like to track and/or share on
GitHub, the process is very simple:

1. [Create a repo](https://github.com/new) on GitHub
2. Follow steps to clone repo and [add repo as an upstream
   remote](http://gitready.com/intermediate/2009/02/12/easily-fetching-upstream-changes.html)
3. Hackity-hack (keep it [atomic](http://www.freshconsulting.com/atomic-commits/))
4. `git commit`
5. `git push`
6. Repeat steps 3-5.

It is also not a bad idea to add a
[README.md](https://help.github.com/articles/about-readmes/) to
the repo with some notes to yourself or others (same as README.txt.)

Multi-user Workflow
-------------------

The process for collaborating with other users on a project using Git and
GitHub is similar to the single-user workflow described above, with a couple
additional steps along the way.

## Setting up the master and forked repos

1. [Create a repo](https://github.com/new) on GitHub (do this once)
2. [Fork](https://help.github.com/articles/fork-a-repo) the master
   repo (each user does this)
3. Follow steps to clone the forked repo and [add repo as an upstream
   remote](http://gitready.com/intermediate/2009/02/12/easily-fetching-upstream-changes.html)
   (each user does this)

## Making changes

Next, once a repo has been created and each user has their own fork of that
repo, the process each user follows to make changes is the same:

1. If master repo has changed, used `git pull` to merge changes into fork.
2. Make changes
3. `git commit`
4. `git push`
5. Submit a [pull request](https://help.github.com/articles/using-pull-requests)

## Accepting changes

Once a pull request (PR) has been submitted, it will [appear on the master
repo](https://github.com/pydata/pandas/pulls). The PR will list all of the
commits made, files changes, and any information the user submitting the PR
provided about the PR.

If this all looks good, then any user who has privileges to the master repo can
"accept" the PR, and the changes will
([usually](https://help.github.com/articles/merging-a-pull-request)) be 
automatically merged into the master repo.

## Other multi-user workflows

There are [other workflows](https://www.atlassian.com/git/workflows) that can
be used for collaboration on GitHub -- the above just illustrates one of these
which I am partial to.

For larger efforts, you can also [create teams on
GitHub](https://help.github.com/articles/how-do-i-set-up-a-team) so that an
entire team owns or manages a repo instead of a single user.

Beyond just code...
-------------------

One of the nice things about Git and GitHub is that you are not limited to
using it for just code. Some other useful things it can be used for include:

- Documents
    - [Notes](https://github.com/khughitt/network-biology-study-group)
    - [Knitr output](https://github.com/khughitt/network-layouts)
    - [Science manuscripts](https://github.com/sunpy/sunpy-0.4-paper)
- Websites
    - [NLM 2018 REPRODUCIBILITY WORKSHOP](https://nlm-repro.github.io/)
    - [Slidify](http://khughitt.github.io/slidify-byob-intro/)
- Images
- Etc.

Further reading
---------------

If you want to learn more, there are a lot of other great tutorials on Git and Github as they
pertain to science. Here are just a few examples to help get you started:

- [A Quick Introduction to Version Control with Git and Github (PLOS Bio)](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004668)
- [Ten Simple Rules for Taking Advantage of Git and Github (PLOS Comp Bio)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4945047/)
- [Making Reproducible Research Enjoyable](https://yihui.name/en/2012/06/enjoyable-reproducible-research/)
- [Electronic lab notebook - The stupidest thing...](http://kbroman.wordpress.com/2013/08/20/electronic-lab-notebook/)
- [Git can facilitate greater reproducibility and increased transparency in science](https://scfbm.biomedcentral.com/articles/10.1186/1751-0473-8-7)
- [GitHub for Academics: the open-source way to host, create and curate knowledge](http://blogs.lse.ac.uk/impactofsocialsciences/2013/06/04/github-for-academics/)
- [Version control for scientific research](http://blogs.biomedcentral.com/bmcblog/2013/02/28/version-control-for-scientific-research/)
- [A quick introduction to Git and GitHub (Data Carpentry for Biologists)](http://datacarpentry.org/semester-biology/START-for-self-guided-students/)

References
----------

- https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
- https://help.github.com/articles/github-flavored-markdown

_Note: This tutorial was adapted from [an earlier version](https://github.com/umd-byob/presentations/tree/master/2014/0128-into_to_git) 
originally presented at a UMD bioinformatics club meeting in January, 2014._

