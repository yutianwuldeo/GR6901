# Intro to Unix

An introduction to basic Unix commands and the file system.

*The notes below are adapted from our [textbook](https://earth-env-data-science.github.io/lectures/environment/intro_to_unix.html).*

*The notes below are modified from the excellent [Unix Shell tutorial ](http://swcarpentry.github.io/shell-novice/) that is freely available on the Software Carpentry website. We highly recommend checking out the full version for further reading. The material is being used here under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/).*

---

## Navigating Files and Directories

Several commands are frequently used to create, inspect, rename, and delete files and directories.

To get started, open a terminal using the JupyterLab launcher. You will see
something like this.

~~~
jovyan@jupyter-yutianwuldeo:~$
~~~

The dollar sign is a **prompt**, which shows us that the shell is waiting for input.
`jovyan` is our **username** and `jupyter-yutianwuldeo` is the **hostname**.
Because we are using JupyterHub on the cloud, we all have the same username
("jovyan" = resident of the planet Jupyter). However, we each have a different
hostname (the name of the computer we are using), which corresponds to a
"virtual machine" running in the cloud. From now on, we will just use a `$`
to indicate the prompt.

To find out your username in general, you can use the command

~~~
$ whoami
jovyan
~~~

and to find out your hostname

~~~
$ hostname
jupyter-yutianwuldeo
~~~

Next,
let's find out where we are by running a command called `pwd`
(which stands for "print working directory").
At any moment,
our **current working directory**
is our current default directory,
i.e.,
the directory that the computer assumes we want to run commands in
unless we explicitly specify something else.
Here,
the computer's response is `/home/jovyan`,
which is the **home directory** of the user named `jovyan`.

~~~
$ pwd
~~~


~~~
/home/jovyan
~~~


To understand what a "home directory" is,
let's have a look at how the file system as a whole is organized.  For the
sake of this example, we'll be
illustrating the filesystem on our scientist Nelle's computer.  After this
illustration, you'll be learning commands to explore your own filesystem,
which will be constructed in a similar way, but not be exactly identical.  

On a Unix computer, the filesystem looks like something this:

![The File System](https://fsl.fmrib.ox.ac.uk/fslcourse/unix_intro/tree.gif)

At the top is the **root directory**
that holds everything else.
We refer to it using a slash character `/` on its own;
this is the leading slash in `/home/jovyan`.

Inside that directory are several other directories:
`bin` (which is where some built-in programs are stored),
`lib` (for the software "libraries" used by different programs),
`home` (where users' personal directories are located),
`etc` (system-wide configuration files),
and so on.  

Now let's learn the command that will let us see the contents of our
own filesystem.  We can see what's in our home directory by running `ls`,
which stands for "listing":

~~~
$ ls
~~~


~~~
GR6901  GR6901backup0827  data  examples  github-sandbox  shared
~~~

`ls` prints the names of the files and directories in the current directory in
alphabetical order,
arranged neatly into columns.
We can make its output more comprehensible by using the **flag** `-F`,
which tells `ls` to add a trailing `/` to the names of directories:

~~~
$ ls -F
~~~

~~~
GR6901/  GR6901backup0827/  data/  examples/  github-sandbox/  shared/
~~~

Special directory .. doesn’t usually show up when we run `ls`. If we want to display it, we can give `ls` the `-a` flag:

~~~
$ ls -F -a
~~~

~~~
./             .cache/   .gitconfig           .jupyter/  .ssh/                GR6901/            examples/
../            .config/  .ipynb_checkpoints/  .lesshst   .viminfo             GR6901backup0827/  github-sandbox/
.bash_history  .git/     .ipython/            .local/    .virtual_documents/  data/              shared/
~~~

`-a` stands for “show all”; it forces `ls` to show us file and directory names that begin with `.`, such as `..` (which, if we’re in /home/jovyan, refers to the /home directory) As you can see, it also displays another special directory `.cache/`, which is a user-specific storage space for temporary items in a computer system, and we’ll see some uses for it soon.

`ls` has lots of other options. To find out what they are, we can type:

~~~
$ man ls
~~~

`man` is the Unix "manual" command:
it prints a description of a command and its options,
and (if you're lucky) provides a few examples of how to use it. To navigate through the `man` pages,
you may use the up and down arrow keys to move line-by-line,
or try the "b" and spacebar keys to skip up and down by full page.
Quit the `man` pages by typing "q".

*However, `man` package is not installed on the LEAP Pangeo. But you can always google it!*

Here,
we can see that our home directory contains mostly **sub-directories**.
Any names in your output that don't have trailing slashes,
are plain old **files**.

We can also use `ls` to see the contents of a different directory.  Let's take a
look at our `github-sandbox` directory by running `ls -F github-sandbox`:

~~~
$ ls -F github-sandbox
~~~

~~~
LICENSE  README.md  sample.md  sample.py  sample.txt
~~~

The command to change locations is `cd` followed by a
directory name to change our working directory.
`cd` stands for "change directory",
which is a bit misleading:
the command doesn't change the directory,
it changes the shell's idea of what directory we are in.

Let's say we want to move to the `github-sandbox` directory we saw above.  We can
use the following series of commands to get there:

~~~
$ cd github-sandbox
~~~

We now know how to go down the directory tree, but
how do we go up?  
There is a shortcut in the shell to move up one directory level
that looks like this:

~~~
$ cd ..
~~~

`..` is a special directory name meaning
"the directory containing this one",
or more succinctly,
the **parent** of the current directory.
Sure enough,
if we run `pwd` after running `cd ..`, we're back in `/home/jovyan`:

~~~
$ pwd
~~~

~~~
/home/jovyan
~~~

These then, are the basic commands for navigating the filesystem on your computer:
`pwd`, `ls` and `cd`.  Let's explore some variations on those commands.  What happens
if you type `cd` on its own, without giving
a directory?  

~~~
$ cd
~~~

How can you check what happened?  `pwd` gives us the answer!  

~~~   
$ pwd
~~~

~~~
/home/jovyan
~~~

It turns out that `cd` without an argument will return you to your home directory,
which is great if you've gotten lost in your own filesystem. 

#### Tab Completion

Typing the full path to directories and files can be slow and annoying.
Fortunately, we have "tab completion" to help us. Try typing `cd sh` and then
press the `<tab>`. The system will try to "auto complete" your command.
Pressing tab twice brings up a list of all the files, and so on.
This is called **tab completion**,
and we will see it in many other tools as we go on.

## Working with Files and Directories

We now know how to explore files and directories,
but how do we create them in the first place?
Let's go back to our home directory
and use `ls -F` to see what it contains:

~~~
$ cd
$ pwd
~~~

~~~
/home/jovyan
~~~

Let's create a new directory called `thesis` using the command `mkdir thesis`
(which has no output):

~~~
$ mkdir thesis
~~~

As you might guess from its name,
`mkdir` means "make directory".
Since `thesis` is a relative path
(i.e., doesn't have a leading slash),
the new directory is created in the current working directory:

~~~
$ ls -F
~~~

~~~
GR6901/  GR6901backup0827/  data/  examples/  github-sandbox/  shared/  thesis/
~~~

Since we've just created the `thesis` directory, there's nothing in it yet:

~~~
$ ls -F thesis
~~~

Let's change our working directory to `thesis` using `cd`.
We then create a blank new file called `draft.txt` using the `touch command`:

~~~
$ cd thesis
$ touch draft.txt
~~~

Now we can edit the file in JupyterLab's text editor. 

The most widely used command-line **editors** are `vim`, `emacs`, and `nano`. Since `vim` is available on the LEAP Pangeo, let's talk about `vim`.

We can open an existing file by entering `vim` in the shell followed by the name of the file:

~~~
$ vim draft.txt
~~~

When we first open a document, we always start in normal mode, in which we can easily copy, paste, and delete (as well as other functionality). To enter insert mode to add and remove text, press the letter `i` or the `Insert` key.

Let's type in a few lines of text.

Once we're happy with our text, to exit insert mode, press the `Esc` key. We can save a file that is currently open by entering the `:w` command. We can then quit an open file by entering the `:q` command. If you have made any edits without saving, you will see an error message. If you wish to quit without saving the edits, use `:q!`.

More on `vim` can be found [here](https://cvw.cac.cornell.edu/linux/text-editors/vim) for instance.

`ls` now shows that we have created a file called `draft.txt`:

~~~
$ ls
draft.txt
~~~

Let's tidy up by running `rm draft.txt`:

~~~
$ rm draft.txt
~~~

This command removes files (`rm` is short for "remove").
If we run `ls` again,
its output is empty once more,
which tells us that our file is gone:

~~~
$ ls
~~~

*Your home directory is intended only for notebooks, analysis scripts, and small datasets (< 1 GB). It is not an appropriate place to store large datasets. Unlike the cloud buckets, these directories use an underlying storage with a rigid limit. If a single user fills up the space, the Hub crashes for everyone. [LEAP Pangeo](https://leap-stc.github.io/leap-pangeo/jupyterhub.html#) recommends users use less than 25GB and enforce a hard limit of 50GB.* 

*To check how much space you are using in your home directory open a terminal window on the hub and run:*

~~~
$ du -h --max-depth=1 ~/ | sort -h
~~~

### Good names for files and directories

 Complicated names of files and directories can make your life painful
 when working on the command line. Here we provide a few useful
 tips for the names of your files.

 1. Don't use whitespaces.

    Whitespaces can make a name more meaningful
   but since whitespace is used to break arguments on the command line
   is better to avoid them on name of files and directories.
    You can use `-` or `_` instead of whitespace.

 2. Don't begin the name with `-` (dash).

    Commands treat names starting with `-` as options.

 3. Stick with letters, numbers, `.` (period), `-` (dash) and `_` (underscore).

    Many other characters have special meanings on the command line.
    We will learn about some of these during this lesson.
    There are special characters that can cause your command to not work as
    expected and can even result in data loss.

 If you need to refer to names of files or directories that have whitespace
 or another non-alphanumeric character, you should surround the name in quotes (`""`).

### Deleting Is Forever

The Unix shell doesn't have a trash bin that we can recover deleted
files from (though most graphical interfaces to Unix do).  Instead,
when we delete files, they are unhooked from the file system so that
their storage space on disk can be recycled. Tools for finding and
recovering deleted files do exist, but there's no guarantee they'll
work in any particular situation, since the computer may recycle the
file's disk space right away.

Let's re-create that file and then move up one directory to `/home/jovyan` using `cd ..`:

~~~
$ touch draft.txt
$ cd ..
~~~

If we try to remove the entire `thesis` directory using `rm thesis`,
we get an error message:

~~~
$ rm thesis
~~~

~~~
rm: cannot remove `thesis`: Is a directory
~~~

This happens because `rm` by default only works on files, not directories.

To really get rid of `thesis` we must also delete the file `draft.txt`.
We can do this with the [recursive](https://en.wikipedia.org/wiki/Recursion) option for `rm`:

~~~
$ rm -r thesis
~~~

### With Great Power Comes Great Responsibility

 Removing the files in a directory recursively can be very dangerous
 operation. If we're concerned about what we might be deleting we can
 add the "interactive" flag `-i` to `rm` which will ask us for confirmation
 before each step

~~~
 $ rm -r -i thesis
 rm: descend into directory ‘thesis’? y
 rm: remove regular file ‘thesis/draft.txt’? y
 rm: remove directory ‘thesis’? y
~~~

 This removes everything in the directory, then the directory itself, asking
 at each step for you to confirm the deletion.

Let's create that directory and file one more time.

~~~
$ mkdir thesis
$ touch thesis/draft.txt
$ ls thesis
~~~

~~~
draft.txt
~~~

`draft.txt` isn't a particularly informative name,
so let's change the file's name using `mv`,
which is short for "move":

~~~
$ mv thesis/draft.txt thesis/quotes.txt
~~~

The first parameter tells `mv` what we're "moving",
while the second is where it's to go.
In this case,
we're moving `thesis/draft.txt` to `thesis/quotes.txt`,
which has the same effect as renaming the file.
Sure enough,
`ls` shows us that `thesis` now contains one file called `quotes.txt`:

~~~
$ ls thesis
~~~

~~~
quotes.txt
~~~

One has to be careful when specifying the target file name, since `mv` will
silently overwrite any existing file with the same name, which could
lead to data loss. An additional flag, `mv -i` (or `mv --interactive`),
can be used to make `mv` ask you for confirmation before overwriting.

Just for the sake of consistency,
`mv` also works on directories

Let's move `quotes.txt` into the current working directory.
We use `mv` once again,
but this time we'll just use the name of a directory as the second parameter
to tell `mv` that we want to keep the filename,
but put the file somewhere new.
(This is why the command is called "move".)
In this case,
the directory name we use is the special directory name `.` that we mentioned earlier.

~~~
$ mv thesis/quotes.txt .
~~~

The effect is to move the file from the directory it was in to the current working directory.
`ls` now shows us that `thesis` is empty:

~~~
$ ls thesis
~~~

Further,
`ls` with a filename or directory name as a parameter only lists that file or directory.
We can use this to see that `quotes.txt` is still in our current directory:

~~~
$ ls quotes.txt
~~~

~~~
quotes.txt
~~~

The `cp` command works very much like `mv`,
except it copies a file instead of moving it.
We can check that it did the right thing using `ls`
with two paths as parameters --- like most Unix commands,
`ls` can be given multiple paths at once:

~~~
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
~~~

~~~
quotes.txt   thesis/quotations.txt
~~~

## Connecting to a Linux Server 

We typically use `ssh` to connect to a linux server. However, because this notebook server, LEAP Pangeo, is a linux “virtual machine", we can't `ssh` in! But we can use the terminal via the JupyterLab launcher and `ssh` / `scp` / `ftp` to remote systems (if you have access to them). For example, we can `ssh` to a HPC called Derecho:

~~~
$ ssh yutian@derecho.hpc.ucar.edu
~~~

We can also move a file `test.m` from Derecho to LEAP Pangeo by using `scp`:

~~~
$ scp yutian@derecho.hpc.ucar.edu:/glade/u/home/yutian/scripts/ars22/test.m .
~~~

## Key Points
- `pwd` prints working directory
- `ls` lists the names of the files and directories in the current directory
- `cd dir` changes the current working directory
- `cp old new` copies a file
- `mkdir path` creates a new directory
- `vim file` edits a file
- `mv old new` moves (renames) a file or directory
- `rm path` removes (deletes) a file
- `ssh` enables secure logins to remote computers
- `scp` secure copies between servers
- The shell does not have a trash bin: once something is deleted, it's really gone.

## Learning More

The goal of this lesson was to familiarize you with the basics of working
with files and directories.
There is a **lot more** to the unix shell and filexsystem than what we have  covered here!
To ge deeper with self study, we recommend the excellent
[Software Carpentry Unix Shell Lesson](https://swcarpentry.github.io/shell-novice/),
on which the above material was based.