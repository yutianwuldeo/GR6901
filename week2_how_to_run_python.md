# Installing and Running Python

An introduction of different ways to run Python code, installing and managing Python with Conda, and running Python with JupyterHub.

*The notes below are adapted from our [textbook](https://earth-env-data-science.github.io/lectures/environment/python_environments.html#) and [Pythia Foundations](https://foundations.projectpythia.org/foundations/getting-started-python.html#).*

---

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

[How to Run Python in the Terminal](https://foundations.projectpythia.org/foundations/terminal.html)

### Jupyter Notebooks

We highly encourage the use of Jupyter notebooks: a free, open-source, interactive tool running inside a web browser that allows you to run Python code in "cells." This means that your workflow can alternate between code, output, and even Markdown-formatted explanatory sections that create an easy-to-follow analysis or "computational narrative" from start to finish. Jupyter notebooks are a great option for presentations or learning tools. For these reasons, Jupyter is very popular among scientists. Most lessons in this book will be taught via Jupyter notebooks.

*More on Running Python on LEAP Pangeo JupyterHub later*

### Other IDEs

If you code in other languages, you might already have a favorite IDE that will work just as well in Python. [Spyder](https://www.spyder-ide.org) is a Python specific IDE that comes with the [Anaconda download](https://www.anaconda.com/products/distribution). It is perhaps the most familiar IDE if you are coming from languages such as [Matlab](https://www.mathworks.com/products/matlab.html) that have a language specific platform and display a list of variables. [PyCharm](https://www.jetbrains.com/pycharm/) and [Visual Studio Code](https://code.visualstudio.com) are also popular IDEs. Many IDEs offer support for terminal execution, scripts, and Jupyter display. To learn about your specific IDE, visit its official documentation.

## Installing and managing Python with Conda

*This is the general guidance for installing and managing Python with Conda. With the LEAP Pangeo JupyterHub, a set of packages has already been installed and is good to use. More on LEAP Pangeo Python Environment later.*

Conda is an open-source, cross-platform, language-agnostic package manager and environment management system that allows you to quickly install, run, and update packages within your work environment(s). Conda is a vital component of the Python ecosystem. Understanding it is important, regardless of the platform you chose to run your Python code.

It is strongly recommended to read official
[Getting Started with Conda](https://conda.io/docs/user-guide/getting-started.html#)
guide.

To create a conda environment, you execute the following command in the terminal:

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

    $ conda env remove --name my_environment 

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

## LEAP Pangeo Python Environment

The environment on our cloud JupyterHub is a highly curated combination of packages
maintained by the [Pangeo Project](http://pangeo.io/).
Then environment lives at <https://github.com/pangeo-data/pangeo-docker-images/>.
In addition to just specifying a combination of packages, this repo automatically
builds [Docker containers](https://docs.docker.com/get-started/).

The latest Pangeo notebook environment lives at <https://github.com/pangeo-data/pangeo-docker-images/blob/master/pangeo-notebook/environment.yml>.
Below are the contents of that file as of 2024-09-06.
Copy and paste the following ``environment.yml`` file somewhere
on your local hard drive:

name: pangeo
channels:
 - conda-forge
 - nodefaults
dependencies:
 - adlfs
 - argopy
 - awscli
 - black
 - boto3
 - bottleneck
 - cartopy
 - cdsapi
 - cfgrib
 - cf_xarray
 - ciso
 - cmocean
 - contextily
 - dask-geopandas
 - dask-ml
 - datashader
 - descartes
 - earthaccess
 - eofs
 - erddapy
 - esmpy
 - fastjmd95
 - flox
 - fsspec
 - gcm_filters
 - gcsfs
 - gh
 - gh-scoped-creds
 - geocube
 - geopandas
 - geopy
 - geoviews-core
 - git-lfs
 - gsw
 - h5netcdf
 - h5py
 - holoviews
 - hvplot
 - intake
 - intake-esm
 - intake-geopandas
 - intake-stac
 - intake-xarray
 - ipdb
 - ipykernel
 - ipyleaflet
 - ipympl
 - ipytree
 - ipywidgets
 - jupyterlab_code_formatter
 - jupyterlab-git
 - jupyterlab-lsp
 - jupyterlab-myst
 - jupyter-panel-proxy
 - jupyter-resource-usage
 - kerchunk
 - line_profiler
 - lonboard
 - lxml
 - lz4
 - matplotlib-base
 - memory_profiler
 - metpy
 - nb_conda_kernels
 - nbstripout
 - nc-time-axis
 - netcdf4
 - numbagg
 - numcodecs
 - numpy
 - numpy_groupies
 - odc-stac
 - pandas
 - panel
 - parcels
 - param
 - planetary-computer
 - pop-tools
 - pyarrow
 - pycamhd
 - pydap
 - pystac
 - pystac-client
 - python-blosc
 - python-gist
 - python-graphviz
 - python-lsp-ruff
 - python-xxhash
 - rasterio
 - rechunker
 - rio-cogeo
 - rioxarray
 - ruff
 - s3fs
 - satpy
 - scikit-image
 - scikit-learn
 - scipy
 - seaborn
 - sparse
 - snakeviz
 - stackstac
 - tiledb-py
 - timezonefinder
 - watermark
 - xarray
 - xarrayutils
 - xarray-datatree
 - xarray_leaflet
 - xarray-spatial
 - xbatcher
 - xclim
 - xesmf
 - xgboost
 - xgcm
 - xhistogram
 - xmip
 - xmitgcm
 - xpublish
 - xrft
 - xskillscore
 - xxhash
 - xvec
 - zarr

Create this environment using conda

    $ conda env create -f environment.yml

Activate this environment

    $ conda activate pangeo

This environment should be sufficient for all of your work in this class.

If you are interested, you can [speed things up with Mamba](https://earth-env-data-science.github.io/lectures/environment/python_environments.html#speeding-things-up-with-mamba).

## Running Python on LEAP Pangeo JupyterHub 

1. When you open your [hub](https://leap.2i2c.cloud/), you can see a “File Browser” on the left sidebar and a Launcher with Notebook, Console, and Other on the right sidebar. 

![Jupyter GUI](images/jupyter_gui.png)

You can create a directory to store our work. Let's call it `work` (or whatever you want to call it). 

You can do this in the GUI left sidebar by clicking the new-folder icon. If you prefer to use the command line, you can access a terminal by clicking the icon under the "Other" heading in the Launcher.

2. Create a new `mysci.ipynb` file within the `work` folder:

Do this in the GUI on the left sidebar by clicking the "+" icon.

This will open a new launcher window where you can select a Python kernel under the "Notebooks" heading for your project. _You should see "Python 3" as in the screenshot above._ Depending on the details of your system, you might see some additional buttons with different kernels.

Selecting a kernel will open a Jupyter notebook instance and add an untitled file to the left sidebar navigator, which you can then rename to `mysci.ipynb`.

3. Change the first notebook cell to include the classic first command: printing, "Hello, world!".

   ```python
   print("Hello, world!")
   ```
   
4. Run your cell with {kbd}`Shift`\+{kbd}`Enter` and see that the results are printed below the cell.

5. Saving your notebook and exiting.

   When you are done with your work, it is time to save and exit.

   To save your file, you can click the "File" in the upper left Jupyter toolbar and "Save" or use keyboard shortcuts.

   Jupyter allows you to close the browser tab without shutting down the server. When you're done working on your notebook, it's important to shutdown the server to free up memory, especially on a shared system. You can do this by clicking "Hub Control Panel" under "File" and then "Stop My Server".

   Then you can quit Jupyter by clicking "Log Out" under "File".

6. Now you can log back onto hub and download the course materials. In the terminal you can do this by -

   $ git clone https://github.com/yutianwuldeo/GR6901.git

## More on Jupyter 

Project Jupyter is a project and community whose goal is to “develop open-source software, open-standards, and services for interactive computing across dozens of programming languages”. Jupyter consists of four main components: Jupyter Notebooks, Jupyter Kernels, Jupyter Lab, and Jupyter Hub. Jupyter can be executed locally and remotely.

### Jupyter Notebooks

The Jupyter Notebook software is an open-source web application that allows you to create and share Jupyter Notebooks (*.ipynb files). Jupyter Notebooks contain executable code, LaTeX equations, visualizations (e.g., plots, pictures), and narrative text. The code does not have to just be Python, other languages such as Julia or R are supported as well.

Jupyter Notebooks are celebrated for their interactive output that allows movement between code, code output, explanations, and more code - similar to how scientists think and solve problems. Jupyter Notebooks can be thought of as a living, runnable publication and make for a great presentation platform.

### Jupyter Kernels

Software engines and their environments (e.g., conda environments) that execute the code contained in Jupyter Notebooks.

### Jupyter Lab

A popular web application on which users can create and write their Jupyter Notebooks, as well as explore data, install software, etc.

### Jupyter Hub

A web-based platform that authenticates users and launches Jupyter Lab applications for users on remote systems.

## Summary 

...

