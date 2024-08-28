# Installing and Running Python

---

## Overview

This section provides an overview of different ways to run Python code, and quickstart guides for:

1.  Choosing a Python platform
2.  Installing and managing Python with Conda

## Choosing a Python Platform

There is no single official platform for the Python language. Here we provide a brief rundown of 3 popular platforms:

1. The terminal,
2. Jupyter notebooks, and
3. IDEs (integrated development environments).

Here we hope to provide you with enough information to understand the differences and similarities between each platform, so that you can make the best choice for your work environment and learn along effectively, regardless of your Python platform preference.

In general, it is always best to test your programs in the same environment in which they will be run. The biggest factors to consider when choosing your platform are:

- What are you already comfortable with?
- What are the people around you using (peers, coworkers, instructors, etc.)?

### Terminal

For learners who are familiar with basic [Linux commands](https://cheatography.com/davechild/cheat-sheets/linux-command-line/) and text editors (such as Vim or Nano), running Python in the terminal is the quickest route straight to learning Python syntax without the covering the bells and whistles of a new platform. If you are running Python on a supercomputer, through an HTTP request or SSH tunneling, you might want to consider learning in the terminal.

[How to Run Python in the Terminal](terminal.md)

### Jupyter Notebooks

We highly encourage the use of Jupyter notebooks: a free, open-source, interactive tool running inside a web browser that allows you to run Python code in "cells." This means that your workflow can alternate between code, output, and even Markdown-formatted explanatory sections that create an easy-to-follow analysis or "computational narrative" from start to finish. Jupyter notebooks are a great option for presentations or learning tools. For these reasons, Jupyter is very popular among scientists. Most lessons in this book will be taught via Jupyter notebooks.

[How to Run Python in a Jupyter Session](jupyter.md)

MORE ON LEAP-Pangeo JupyterHub at the end!!! 

### Other IDEs

If you code in other languages, you might already have a favorite IDE that will work just as well in Python. [Spyder](https://www.spyder-ide.org) is a Python specific IDE that comes with the [Anaconda download](https://www.anaconda.com/products/distribution). It is perhaps the most familiar IDE if you are coming from languages such as [Matlab](https://www.mathworks.com/products/matlab.html) that have a language specific platform and display a list of variables. [PyCharm](https://www.jetbrains.com/pycharm/) and [Visual Studio Code](https://code.visualstudio.com) are also popular IDEs. Many IDEs offer support for terminal execution, scripts, and Jupyter display. To learn about your specific IDE, visit its official documentation.

_We recommend eventually learning how to develop and run Python code in each of these platforms._

## Installing and managing Python with Conda

Conda is an open-source, cross-platform, language-agnostic package manager and environment management system that allows you to quickly install, run, and update packages within your work environment(s). Conda is a vital component of the Python ecosystem. Understanding it is important, regardless of the platform you chose to run your Python code.

It is strongly recommended to read official
[Getting Started with Conda](https://conda.io/docs/user-guide/getting-started.html#)
guide.

To create a conda environment, you execute the following command:

    $ conda create --name my_environment python=3.9 numpy

This will create a special environment in ``$MINICONDA_HOME/envs/my_environment``
with only Python and numpy to begin with. Here, we've also told conda to install
Python version 3.9; you can specify exact versions or minima, and conda will
take care of figuring out all the compatibilities between versions for you. To use
this environment, simply "activate" it by executing:

    $ conda activate my_environment

Regardless of your shell, you should now see the string ``(my_environment)``
prepended to your prompt. Now, if you execute any Python-related tool from the
command line, it will first search in ``$MINICONDA_HOME/envs/my_environment/bin``
to find them.

You can deactivate your environment by typing:

    $ conda deactivate

To see all the environments on your system:

    $ conda info --envs

If you want to permanently remove an environment and delete all the data
associated with it:

    $ conda env remove --name my_environment --all

For extensive documentation on using environments, please see
[the conda documentation](https://conda.io/docs/using/envs.html). The most
important feature to review here is the ability to *share and export* your
environment; this is the basis for reproducibility in the scientific Python stack.
At any time from the shell, you can execute

    $ conda list

to get a complete summary of all the packages installed in your environment, the
channel they were installed from, and their full version info. Using this info,
you can create an **environment file** in
[YAML syntax](http://docs.ansible.com/ansible/latest/YAMLSyntax.html)
which documents the exact
contents of your environment. With that file, a new environment with the exact
configuration can be installed by executing

    $ conda env create -f my_environment.yml

Below we will see an example of an environment file.

## Installing More Packages

Once you have a basic Python environment, you can easily add or remove packages
using conda.
Conda was created to help manage the complex dependencies and
pre-compiled binary libraries that are necessary in scientific python.

If you set up your python environment using the Anaconda Python Distribution or
with miniconda, you should already have the **conda** command available on
the command line.
With it, you can easily install packages from an official, curated set of packages which are
built and tested for a number of different system configurations on Linux,
Windows, and macOS

    $ conda install <package-name>

Additionally, there is a
community-maintained collection of packages/recipes called
[conda forge](https://conda-forge.github.io/>)
which is accessible through conda as a special "channel"

    $ conda install -c conda-forge <package-name>

While conda allows you to install almost any science-related package, there may
be other general-use python packages you wish to you that are not available in
via conda. For these, you can use an alternative installation method.

Outside of the scientific python community,
the most common way to install packages is to search for them on the official
[PyPI](https://pypi.python.org/pypi) index. Once you've found the package you
want to install (you may have also just found it on github or elsewhere), you
use the **pip** command from a the command line:

    $ pip install <package-name>

This will fetch the source code, build it, and install it to wherever your
``$PYTHONPATH`` is set. This works in the vast majority of cases, particularly
when the code you're installing doesn't have any compiled dependencies.

If you can't find a package on either PyPI or conda-forge, you can always install it
directly from the source code. If the package is on github, ``pip`` already has
an alias to do this for you:

    $ pip install git+https://github.com/<user>/<package-name>.git

## WU! MORE on Jupyter Notebooks

1. With your Conda environment activated and Jupyter session launched (see above), create a directory to store our work. Let's call it `pythia-foundations`.

   You can do this in the GUI left sidebar by clicking the new-folder icon. If you prefer to use the command line, you can access a terminal by clicking the icon under the "Other" heading in the Launcher.

2. Create a new `mysci.ipynb` file within the `pythia-foundations` folder:

   Do this in the GUI on the left sidebar by clicking the "+" icon.

   This will open a new launcher window where you can select a Python kernel under the "Notebooks" heading for your project. _You should see "Python 3" as in the screenshot above._ Depending on the details of your system, you might see some additional buttons with different kernels.

   Selecting a kernel will open a Jupyter notebook instance and add an untitled file to the left sidebar navigator, which you can then rename to `mysci.ipynb`.

   Select "Python 3" to use the Python version you just installed in the `pythia_foundations_env` conda environment.

3. Change the first notebook cell to include the classic first command: printing, "Hello, world!".

   ```python
   print("Hello, world!")
   ```

4. Run your cell with {kbd}`Shift`\+{kbd}`Enter` and see that the results are printed below the cell.

5. Saving your notebook and exiting

   When you are done with your work, it is time to save and exit.

   To save your file, you can click the disc icon in the upper left Jupyter toolbar or use keyboard shortcuts.

   Jupyter allows you to close the browser tab without shutting down the server. When you're done working on your notebook, _it's important to **click the "Shutdown" button** on the dashboard_ to free up memory, especially on a shared system.

   Then you can quit Jupyter by:

   - clicking the "Quit" button on the top right, or
   - typing `exit` into the terminal

Alternatively you can simultaneously shutdown and exit the Jupyter session by typing
{kbd}`Ctrl`\+{kbd}`C` in the terminal and confirming that you do want to
"shutdown this notebook server."