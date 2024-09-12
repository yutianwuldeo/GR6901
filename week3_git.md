# Intro to Git for Version Control

*The notes below are adapted from our [textbook](https://earth-env-data-science.github.io/lectures/environment/intro_to_git.html#) and [Pythia Foundations](https://foundations.projectpythia.org/foundations/getting-started-github.html).*

---

## Overview:

[Version control](https://en.wikipedia.org/wiki/Version_control) is a powerful way to organize, back up, and share with collaborators your research computing code.
A Verson control system keeps track of a set of files and saves snapshots (i.e. _versions_, _commits_) of the files at any point in time.
Using version control allows you to confidently make changes to your code (any any other files), with the ability to roll back to any previous state. This help avoid filling our directories up with files that look like this:

    my_code.py
    my_code_version2.py
    my_code_version2B-RPA-edit.py
    my_code_FINAL_VERSION.py
    my_code_THIS_IS_ACTUALLY_THE FINAL VERSION.py

Version control also allows you to share code with collaborators, make simultaneous edits, and merge your changes in a systematic, controlled way.

Version control has been used for a long time in software development.
More recently, it has become an essential part of modern data and computational science.
Our strong recommendation is that _all of your research code be stored in a version control system_.

The tool we will be using for version control is called [Git](https://git-scm.com).
Git is incredibly powerful--it also has a somewhat steep learning curve.
Fortunately, in this class, we will only be using a small subset of what git can do, avoiding the more complex aspects.

For a full-length tutorial, we recommend the article [Version Control with Git](http://swcarpentry.github.io/git-novice/) on Software Carpentry website.
Here we simply enumerate the most common git commands.

## GitHub

### GitHub

[GitHub](https://github.com) is a web-based platform for the dissemination of free and open-source software.

GitHub provides the following:

1. _Version control_ for free and open-source software and other digital assets
1. Project _discussion forums_
1. _DevOps_ to facilitate building and testing software
1. _Bug_ reporting, patching, and tracking
1. _Documentation_ hosting
1. An environment that fosters _collaboration_

Although GitHub can host any digital asset, the most common use case for GitHub is for individuals or organizations to house _repositories_ of _free_ and _open-source software_.

You can set up a free user account on GitHub.

### GitHub Repositories

GitHub gives the following explanation of a [repository](https://docs.github.com/en/get-started/quickstart/hello-world):

> A repository is usually used to organize a single project. Repositories can contain folders and files, images, videos, spreadsheets, and data sets -- anything your project needs. Often, repositories include a `README` file, a file with information about your project. GitHub makes it easy to add one at the same time you create your new repository. It also offers other common options such as a license file.

In short, it is a _collection of files_. Each GitHub repository has an _owner_, which could be an individual or an organization. Repositories can also be set to _public_ or _private_, determining who can see and interact with it. While a repository can simply store files, GitHub is designed with **collaboration** in mind. Three key collaborative tools in GitHub are:

1. **Issues**: report a bug, plan improvements, or provide feedback to others working on the repository.
1. **Discussions**: post ideas or other conversations that are not as specific or actionable as an **Issue**.
1. **Pull requests**: We will go into the specifics later, but a **Pull request** allows a user to _propose a change_ to any of the files within a repository.

All of the Python packages covered (e.g. [Numpy](https://github.com/numpy/numpy) and [Xarray](https://github.com/pydata/xarray)) have associated GitHub repositories, as well as [Python itself](https://github.com/python/cpython).

As you can see by the recent timestamps, these repositories are actively changing; this reflects the adaptability of the [open-source software](https://opensource.org/osd) ecosystem surrounding Python.

Finally, we introduce an important concept that is vital to your
understanding when working with GitHub. It is the source of GitHub's power, as well
as much of its complexity. GitHub repositories
are _distributed_; in the general case, there is more than one
repository for any project. In fact, repositories can come and go
at any time, created and deleted as need dictates. Creating new
repositories from existing ones, synchronizing them, and managing them
are the topics of later sections. For now, it is only important to
understand that for a GitHub-managed project, there is typically one
"official" repository, often called the "upstream" repository, and it lives on GitHub.com. There may be any
number of copies of the "official" repository, known as _forks_ (or _origins_,
if it is owned by you),
that also reside on GitHub.com. Repos that are hosted on GitHub.com
are referred to as _remotes_. In addition to the remotes, there may
be one or more copies of the remotes on your desktop or laptop
computer that are referred to as _locals_. A conceptual diagram of
the various repos is shown in the image below.

![GitHub repositories](images/github-repos.png)




## GitHub Workflows

GitHub, together with Git, are powerful tools for managing and
collaborating on all kinds of digital assets, such as software,
documentation, and even manuscripts for research papers. Like other
complex software environments, often these tools can be employed
in many different ways to accomplish the same goal. In order to
effectively and consistently use Git and GitHub, over the years a
variety of best practices have evolved for supporting different
modes of collaboration. Collectively these different models, or
recipes, are referred to as _workflows_.

A typical sequence of workflow steps consists of the following:

1. A contributor clones a personal remote repository, creating a local copy
1. The contributor creates a new branch in their local repository
1. The contributor makes changes to the branch and commits them to
   their local repository
1. The contributor _pushes_ the branch to a remote repository
1. The contributor submits a PR via GitHub

The sequence of steps
outlined above provides a general framework for submitting a PR.
But the precise set of steps is highly dependent on the choice of
workflow for a given project. In this chapter we describe Pull
Requests for two commonly used workflows: The **Git Feature Branch
Workflow** and the **Forking Workflow**. The former is simpler and often
used by teams when everyone on the team is an authorized contributor
to the destination repository. I.e. all of the contributors have
write access to the remote repository hosted by GitHub. The latter
is typically what is needed to contribute to external projects for
which the contributor is not authorized (i.e. does not have write
access) to make changes to the destination repository. We briefly
describe both workflows below, and include the steps necessary to
make a PR on each.

## Git Feature Branch Workflow

The **Git Feature Branch Workflow** is one of the simplest and oldest
collaborative workflows that is used for small team projects. The
key idea behind this workflow, which is also common to the **Forking
Workflow**, is that all development (all changes) should take place
on a dedicated Git _feature_ branch, not the _main_ (historically
referred to as _master_) branch. The motivation behind this is that
one or more developers can iterate over a feature branch without
disturbing the contents of the main branch. Consider using the **Git
Feature Branch Workflow** for GitHub’s most widely used purpose,
software development. Software modifications are liable to introduce
bugs. Isolating them to a dedicated branch until they can be fixed
ensures that a known, or official, version of the software is always
available and in working order.

```{note}
Avoiding making edits directly on the `main` branch is considered best practice for most workflows and projects!
```

Working with the Git Feature Branch Workflow

This model assumes a single, remote GitHub repository with a branch
named `main`, that contains the official version of all of the digital
assets, along with a history of all of the changes made. When a
contributor wishes to make changes to the remote repository, they
clone the repo and create a descriptively named feature branch,
such as `my-new-feature` or perhaps `issue-nnn`, where `nnn` is the
number of an issue opened on the repository that this new feature
branch will address. Changes by the contributor are then made to
the feature branch in a local copy of the repository. When ready,
the new branch is pushed to the remote repository.

At this point,
the new branch can be viewed, discussed, and even changed by
contributors with write access to the remote repository. When the
author of the feature branch thinks the changes are ready to be
merged into `main` on the remote repository, they create a PR. The
PR signals the project maintainers that the contributor would like
to merge their feature branch into `main`, and invites review of the
changes made in the branch. GitHub simplifies the process of viewing
the changes by offering a variety of ways to see context differences
(diffs) between `main` and the feature branch. Discussion between
the reviewers and the contributor inside a PR discussion forum
occurs in the same way that discussion over GitHub [Issues](github-issues) takes
place inside a discussion forum associated with a particular issue.
If additional changes are requested by the reviewers, these can be
made by the contributor in their local repository, committed, and
then pushed to the remote using the same processes they used with
the initial push. Once reviewers are satisfied with the changes, a
project maintainer can merge the feature branch with `main`.

First of all, set up your username and email:

~~~
git config --global user.name "Yutian Wu"
git config --global user.email "yutianwu@ldeo.columbia.edu"
~~~

### Cloning the remote repository

If you don’t have a local copy of the remote repository, you’ll want
to create one by [cloning the
remote](github-cloning-forking)
to your local computer. This can be done with the git command line
tools and the general form of the command looks like this:

~~~
git clone repository-url local-directory-name
~~~

Where `repository-url` is the URL for the GitHub repo that you want
to clone, and `local-directory-name` is the directory path on your
local machine into which you want to create the clone. The local
directory need not already exist. The clone command will create the
local directory for you. If you don’t know the URL for your
repository, navigate your web browser to your GitHub repository,
and click on the `Code` button. The URL will be displayed.

For example, let's clone the [Project Pythia sandbox repository](https://github.com/ProjectPythia/github-sandbox):

~~~
git clone https://github.com/ProjectPythia/github-sandbox.git
~~~

Note, we did not specify a `local-directory_name` here, so git will
use the `base name` of the `repository_url`, "github-sandbox" as
the local directory.

### Start with the main branch

Continuing with our example above, make sure you are on the main
branch and that it is up to date with the remote repository main:

~~~
cd github-sandbox
git checkout main
git pull
~~~

You should see output that looks like:

~~~
Already on 'main'
Already up to date.
~~~

Now inspect this repository with 

~~~
git status
~~~
which will always give you information about the current git repo. Try it! You should see something like this:

.... TO ADD ...

### Create a new branch

You may have noticed that the file `sample.txt` in the `github-sandbox` repository contains a typo. Here we're going to fix the error and save it locally.

Before we start editing files, the first thing to do is to _create a new branch_ where we can safely make any changes we want.

```{tip}
While there's nothing stopping us from making changes directly to the `main` branch, it's often best to avoid this! The reason is that it makes collaboration trickier. See the [lesson on Pull Requests](github-pull-request).
```

Let's create and checkout a new branch in one line:

~~~
git checkout -b fix-typo
~~~

Now try your new best friend again:

~~~
git status
~~~

You should see something like this:

~~~
On branch fix-typo
nothing to commit, working tree clean
~~~

This tells us that we have switched over to a new branch called `fix-typo`, but there are not (yet) any changes to the files in the repo.

### Make changes and commit

Now do the following:

- Using your favorite text editor, open the file `github-sandbox/sample.txt`.
- Replace the word `Fxing` with the much more satisfying `Fixing`.
- Save the changes.
- Revisit your new best friend `git status`. It should now show something like this:

~~~
On branch fix-typo
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   sample.txt

no changes added to commit (use "git add" and/or "git commit -a")
~~~

Here `git` is telling us that the file `sample.txt` does _not_ match what's in the repository.

Of course we know what changed in that file because we just finished editing it. But here's a quick and easy way to see the changes:

~~~
git diff
~~~

which should show you something like this:

~~~
diff --git a/sample.txt b/sample.txt
index 4bc074c..edc31c0 100644
--- a/sample.txt
+++ b/sample.txt
@@ -4,6 +4,6 @@ We can use it to demonstrate making pull requests or raising issues in a GitHub

 One good way to contribute to a project is to make additions and/or edits to documentation!

-Fxing something as simple as a typo is a great way to get started as a contributor!
+Fixing something as simple as a typo is a great way to get started as a contributor!

 Or, consider adding some more content to this file.
~~~

We can see here that `git diff` finds the line(s) where our current file differs from what's in the repo, along with a few lines before and after for context.

The next step is to add our changes to the "official" history of our repo. This is a two-step process (staging and committing).

#### Staging

Before we make a commit, we must first stage our changes. Think of staging simply as "getting ready to commit". The two-step process can help avoid accidentally committing something that wasn't ready.

To stage our changes, we use `git add` like this:

~~~
git add sample.txt
~~~

and now our new best friend tells us

~~~
On branch fix-typo
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   sample.txt
~~~

Now we see that all-important line `Changes to be committed`, telling us the contents of our staging area.

If you made a mistake (e.g., staged the wrong file), you can always unstage using `git restore` as shown in the `git status` output. Nothing is permanent until we commit!

(And if you accidentally commit the wrong thing? Don't worry, you can always "go back in time" to previous commits -- see below!)

#### Committing

It's time to make a commitment. We can now permanently add our edit to the history of our `fix-typo` branch by doing this:

~~~
git commit -m 'Fix the typo'
~~~

```{note}
Every commit should have a "message" that explains briefly what the commit is for. Here we set the commit message with the `-m` flag and chose some descriptive text. Note, it's critical to have those quotes around `'Fix the typo'`. Otherwise the command shell will misinterpret what you are trying to do.
```

Now when we do `git status` we see

~~~
On branch fix-typo
nothing to commit, working tree clean
~~~

And we're back to a clean state! We have now added a new permanent change to the history of our repo (or more specifically, to this _branch_ of the repo).

#### Going back in time

Each commit is essentially a snapshot in time of the state of the repo. So how can we look back on that history, or revert back to a previous version of a file?

*Viewing the commit history with `git log`*

A simple way to see this history of the current branch is this:

~~~
git log
~~~

You'll see something like this:

~~~
commit 7dca0292467e4bbd73643556f83fd1c52b5c113c (HEAD -> fix-typo)
Author: Brian Rose <brose@albany.edu>
Date:   Mon Jan 17 11:31:49 2022 -0500

    Fix the typo

commit 35fcbd991f911e170df550db58f74a082ba18b50 (origin/main, origin/HEAD, main)
Author: Kevin Tyle <ktyle@albany.edu>
Date:   Thu Jan 13 11:29:40 2022 -0500

    Close docstring quote on sample.py

commit e56ea58071f150ec00904a50341a672456cbcb8f
Author: Kevin Tyle <ktyle@albany.edu>
Date:   Tue Jan 11 14:15:31 2022 -0500

    Create sample.md

commit f98d05e312d19a84b74c45402a2904ab94d86e45
Author: Kevin Tyle <ktyle@albany.edu>
Date:   Tue Jan 11 13:58:09 2022 -0500

    Create sample.py
~~~

which shows the last few commits on this branch, including the commit number, author, timestamp, and commit message. You can page down to see the rest of the history
or just press `Q` to exit `git log`!

```{note}
Every commit has a unique hexadecimal checksum code like `7dca0292467e4bbd73643556f83fd1c52b5c113c`. Your history will look a little different from the above!
```
*Checking out a previous commit*

Let's say you want to retrieve the file `sample.txt` from the previous commit. Two possible reasons why:

1. You just want to take a quick look at something in the previous commit, but then go back to the current version. That's what we'll do here.
2. Maybe you don't like the most recent commit and want to do some new edits _starting from the previous commit_ -- in effect, undoing the most recent commit and going back in time. The simplest way to do this is to _create a new branch_ starting from the previous commit. We'll cover branches more fully in the next lesson.

To retrieve the previous commit, just use `git checkout` and the unique number code which you can just copy and paste from the `git log` output:

~~~
git checkout 35fcbd991f911e170df550db58f74a082ba18b50
~~~

You may see output that looks like this:

~~~
Note: switching to '35fcbd991f911e170df550db58f74a082ba18b50'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 35fcbd9 Close docstring quote on sample.py
~~~

(the details may vary depending on what version of git you are running).

By `detached HEAD`, git is telling us that we are NOT on the most recent commit in this branch.

If you inspect `sample.txt` in your editor, you will see that the typo `Fxing` is back!

As the git message above is reminding us, it's possible to create an entirely new branch with changes that we make from this point in the history using `git switch -c`. But for now, let's just go back to the most recent commit on our `fix-typo` branch:

~~~
git checkout fix-typo
~~~

### Push the feature branch to the remote repository

After running `git commit` your changes have been captured in your
local repository. But most likely only you can see them, and if
your local file system fails your changes may be lost. To make your
changes visible to others, and safely stored on your remote GitHub
repository, you need to push them. However, remember at the beginning
of this section we said that the **Git Feature Branch Workflow** works
when you have write access to the remote repository? Unless you are
a member of Project Pythia you probably don't have write access to
the `github-sandbox` remote repo. So you won't be able to push your
changes to it. That's OK. We can still run the `push` command. It won't
break anything. Here is the `push` command that we expect to fail:

~~~
git push --set-upstream origin fix-typo
~~~

You should get a helpful error message like:

~~~
remote: Permission to ProjectPythia/github-sandbox.git denied to clyne.
fatal: unable to access 'https://github.com/ProjectPythia/github-sandbox.git/': The requested URL returned error: 403
~~~

The use of the ‘--set-upstream’ option is a one-time operation when
you push a new branch. Later, if you want to push subsequent changes
to the remote you can simply do:

~~~
git push
~~~

If you are feeling unsatisfied about not having `git push` succeed, there
is a simple solution: create a GitHub repository owned by you. The
GitHub Quickstart guide provides an excellent [tutorial](https://docs.github.com/en/get-started/quickstart/create-a-repo) on how to
do this.

### Making a Pull Request

Finally, after cloning a remote repository, creating a feature
branch, making your changes, committing them to your local repository,
and pushing your commits back to the remote repository, you are now
ready to issue a PR requesting that the remote repository maintainers
review your changes for potential merger into the main branch on
the remote. This final action must be performed from within your
web browser. After navigating to your repo do the following:

1. Click on “Pull Requests” in the top navigation bar
1. Click on “New Pull Request”
1. Under “Compare changes”, make sure that `base` is set to `main`, and `compare` is set to the name of your feature branch, `my-new-feature`
1. Click on “Create Pull Request”
1. A PR window should open up. Provide a descriptive title, and any helpful comments that you want to communicate with the reviewers
1. Click on “Create Pull Request” in the PR window.

That’s it! You’re done! Sit back and wait for comments from reviewers.
If changes are requested, simply repeat the steps above. Once your
PR is merged you’ll receive notification from GitHub.

## Using Git / GitHub from remote JupyterHub

The recommended way to move code in and out of a remote hub is via git / GitHub.
You should clone your project repo from the terminal and use git pull / git push to update and push changes.
In order to push data to GitHub from the hub, you will need to set up GitHub authentication.
[gh-scoped-creds](https://github.com/yuvipanda/gh-scoped-creds/) should be already setup
on your 2i2c managed JupyterHub, and we shall use that to authenticate to GitHub for
push / pull access.

Open a terminal in JupyterHub, run `gh-scoped-creds` and follow the prompts.

Alternatively, in a notebook, run the following code and follow the prompts:

~~~
import gh_scoped_creds
%ghscopedcreds
~~~

You should now be able to push to GitHub from the hub! These credentials will expire after
8 hours (or whenever your JupyterHub server stops), and you'll have to repeat these steps
to fetch a fresh set of credentials. Once you authenticate, you'll be provided with a link
to a [GitHub App](https://docs.github.com/en/developers/apps/getting-started-with-apps/about-apps)
that you have to [install](https://docs.github.com/en/developers/apps/managing-github-apps/installing-github-apps)
on the repositories you want to be able to push to from this particular JupyterHub. You only
need to do this once per JupyterHub, and can revoke access any time. You can always provide
access to your own personal repositories, but might need approval from admins of GitHub
organizations if you want to push to repos in that organization.

## Summary

- Version control is an important tool for working with code files (or anything that is saved as plain text).
- git is the most common version control software in use today.
- `git init`: initiate a new repo
- `git status`: see what branch we're on and what state our repo is in
- `git log`: see the commit history of our branch
- `git add file`: stage a file for a commit
- `git commit -m 'message/comment'`: create a new commit with the staged files
- `git checkout`: switch between branches (use the `-b` flag to create a new branch and check it out)
- `git diff commit-one commit-two` and `git diff branch-one..branch-two`: compare files between current version and last commit (default), between two commits, or between two branches.
- `git push` and `git pull`: export or input changes between your local branch and a remote repository (e.g. hosted on GitHub)
  