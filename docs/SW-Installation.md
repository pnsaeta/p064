{:menu SW}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="main-menu"><img id="master" src="figs/master.webp"></label>
<div class="dropdown-content">
<ul>
<li><a href="SW-Installation.html">Software Installation</a></li>
<li><a href="LA-LinearAlgebra.html">Linear Algebra</a></li>
<li><a href="FO-Intro.html">Fourier Series and Transforms</a></li>
<li><a href="ST-Random.html">Stochastic Processes</a></li>
<li><a href="DE-DE1.html">Differential Equations</a></li>
<li><a href="PD-PD1.html">Partial Differential Equations</a></li>
<li><a href="PR-Project.html">Projects</a></li>
</ul>
</div>
</div>
<div class="dropdown hamburger">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.webp"></label>
<div class="dropdown-content">
<ul>
<li><a href="SW-Installation.html">Installing and Configuring Software</a></li>
<li><a href="SW-Jupyter.html">Using Jupyter Notebooks</a></li>
<li><a href="SW-NumPy.html">Basics of NumPy</a></li>
<li><a href="SW-Matplotlib.html">Introduction to Plotting with Matplotlib</a></li>
<li><a href="SW-MPLFormatting.html">Formatting in Matplotlib</a></li>
<li><a href="SW-pandas.html">Pandas</a></li>
<li><a href="SW-colab.html">Using Google Colab</a></li>
<li><a href="SW-Python.html">Python</a></li>
<li><a href="SW-Animation.html">Animations in Matplotlib</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# Installing and Configuring Software

* toc
{:toc}

The computational portions of the course will use Python 3 and several modules.
If you have Anaconda installed, You may already have everything you need

I prefer not to use Anaconda, but to install the tools I need using Pip, the Python installer program.

Alternatively, you can let Google take care of hosting the software (which, of
course, requires a live net connection) by using Google Colab, a
Google-inflected version of JupyterLab. If you use this approach, all you need
to do is head to [Google's colab page](https://colab.research.google.com/).
If you need to access your
own Python code, see [the Colab page](SW-colab.md) for more information.

An Anaconda installation should already have Jupyter notebook installed and
available, but you don't need the full anaconda distribution to use Jupyter
notebook and I have had some trouble in the past getting Anaconda to update to a
more recent version of some of the tools. If you already have an Anaconda
installation, it seems reasonable to check it out and make sure that it can run
what we need. Otherwise, I recommend a light-weight approach using Python/Pip,
as described below.

## Anaconda
   If you have Anaconda installed you can launch the Anaconda Navigator from
   which you can launch Jupyter notebook. You can download Anaconda from
   [https://www.anaconda.com/](https://www.anaconda.com/).

## Python/Pip

Many systems have Python installed automatically. At this point, there is no
reason to use Python 2.7.x; it has been deprecated and is no longer supported
(although many projects have stubbornly refused to update to Python
3). Because Python 2 still hangs around, typing `python` at a command prompt
may launch a version 2 interpreter. You can test with

~~~~ python
> python
Python 2.7.17 (default, Dec 23 2019, 21:25:33)
[GCC 4.2.1 Compatible Apple LLVM 11.0.0 (clang-1100.0.33.16)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
~~~~

To be sure that you are running some flavor of Python 3, you can use =python3=:

~~~~ python
> python3
Python 3.10.1 (main, May 24 2022, 11:45:23) [Clang 13.1.6 (clang-1316.0.21.2.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
~~~~

## Installing Python on MacOS

Although there is a Python version already installed in MacOS, it tends to lag
behind and I much prefer to use [Homebrew](https://homebrew.sh) to install an up-to-date version (and
plenty of other free software). You can check if you already have it installed
by opening up a terminal window (the *Terminal.app* program is in
`/Applications/Utilities/Terminal.app`, or you can use an alternative terminal
program, such as [iTerm2](https://iterm2.com)).

~~~~ shell
> which brew
/opt/homebrew/bin/brew
~~~~

Since I already have the `brew` command installed, I see that it is located in
`/opt/homebrew/bin`, which is where most Homebrew commands get linked.

If you do not have Homebrew installed, you can follow the directions at [brew.sh](https://brew.sh)
or paste the following at the terminal.

~~~~ shell
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
~~~~

Once Homebrew is installed, use it to install python:

~~~~ shell
brew install python
~~~~

This should install the most recent stable version of Python 3. It also includes
the Python installer `pip`. (Prior versions of jupyterlab required nodejs, but
the current version (jupyterlab-3.0) does not.) 

~~~~ shell
> brew --version

Homebrew 3.3.9
Homebrew/homebrew-core (git revision 5eeaacb2ec3; last commit 2022-01-04)
Homebrew/homebrew-cask (git revision 16eab891a1; last commit 2022-01-04)
~~~~

## Installing on Windows 10 or 11

Download the Anaconda3 installer and launch it. After it finishes installing, launch the Anaconda Navigator. Then click to launch a Powershell:

![blah](figs/w11powershell.webp)

This opens a terminal window. Enter the command

~~~~ shell
pip install ipympl
~~~~

to install the Python package that allows graphs generated by ~Matplotlib~ to be
displayed inside a jupyter lab window.

## Installing on Ubuntu (Linux)

Make sure that Python 3 is installed:

~~~~ shell
sudo apt update
sudo apt -y upgrade
sudo apt install -y python3-dev python3-pip
sudo apt install -y build-essential libssl-dev libffi-dev
~~~~

## Environment

You can learn a lot about your current environment by issuing the `env` command
at a terminal prompt:

~~~~ shell
> env
PWD=/Users/saeta/Documents/Courses/p64
LOGNAME=saeta
LC_TERMINAL=iTerm2
COLORFGBG=0;15
TERM_PROGRAM=iTerm.app
TERM_PROGRAM_VERSION=3.4.15
LANG=en_US.UTF-8
COLORTERM=truecolor
EDITOR=/Applications/Aquamacs.app/Contents/Resources/bin/aquamacs
ITERM_SESSION_ID=w2t0p0:8CE2A14F-C154-4863-A515-86F06CC7167C
PATH=/Users/saeta/.pyenv/shims:/Users/saeta/bin:/usr/local/bin:/usr/local/sbin:
  /opt/homebrew/bin:/opt/homebrew/sbin:/opt/local/bin:/opt/homebrew/opt/fzf/bin:
  /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin:
  /Library/TeX/texbin:/Applications/Wireshark.app/Contents/MacOS:
  /Users/saeta/Library/Python/3.9/bin:/usr/local/mysql/bin:/Users/saeta/.gem/ruby/2.6.0/bin
OMF_CONFIG=/Users/saeta/.config/omf
PYENV_SHELL=fish
TERM=xterm-256color
TMPDIR=/var/folders/tw/_d06s9vj4wj_83s0m3j99qhc0000gn/T/
SHLVL=1
SHELL=/opt/homebrew/bin/fish
ITERM_PROFILE=Default
SECURITYSESSIONID=186a5
JUPYTER=/opt/homebrew/bin/jupyter
OMF_PATH=/Users/saeta/.local/share/omf
HOME=/Users/saeta
USER=saeta
PYTHONPATH=/Users/saeta/.python
COMMAND_MODE=unix2003
BAT_THEME=zenburn
~~~~

In particular, notice the value of the `PATH` shell variable, which tells you
where the system will look for commands that you name on the command line, and
shows them in the order in which they will be searched. Paths are separated with
colons, so in this example, my shell will first look in `/Users/saeta/bin`, then
in `/usr/local/bin`, etc. If you have installed Anaconda, your `PATH` variable may
start with the path to the `bin` directory inside your Anaconda distribution.

## Using pip to install Python modules

Python has a standard package manager, *pip*, which stands for **Package
Installer for Python**. You can check if `pip` is available by entering the
following command at a terminal prompt:

~~~~ shell
$$ pip --version
pip 22.1.2 from /Users/saeta/.local/lib/python3.10/site-packages/pip (python 3.10)
~~~~

Look carefully at the path to your version of pip. If it has Anaconda in it
somewhere, then it is associated with an existing Anaconda installation (perhaps
a relic from CS 5?) and likely for an older version of Python and Pip. If so,
see if you can upgrade to a current version of Anaconda and its associated
versions of numpy, scipy, matplotlib, and plotly.

If you have a Python 3 installation, and pip is
available, you can install everything you need with the following. If you
prefer, you can first create a virtual environment for this Python installation
so any upgrades or installed libraries don't encounter conflicts:

~~~~ shell
virtualenv jup        # the standard virtualenv package
vf jup                # or, if you use the fish shell, as I do
~~~~

After creating the virtual environment above, then run

~~~~ shell
pip install --upgrade pip  # make sure you have an up-to-date version
pip install numpy scipy matplotlib jupyter
~~~~

These commands install the minimum you need to get going. However, I recommend also installing some more packages:

~~~~ shell
pip install autopep8 ipympl jupyter_contrib_nbextensions plotly
jupyter contrib nbextension install --user
~~~~

## Configuration

Although Jupyter and Matplotlib work “out of the box,” you will probably want to
customize things a bit. Here are some basic ideas.

### Extensions in Jupyter Notebook

First install `jupyter_contrib_nbextensions` from pip:

~~~~ shell
pip install jupyter_contrib_nbextensions
~~~~

Next install the necessary javascript and css files

~~~~ shell
jupyter contrib nbextension install --user
pip install jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user
~~~~

Launch Jupyter notebook from the directory where you would like to load code and save notebooks:

~~~~ shell
> cd ~/Documents/testing
> jupyter notebook
~~~~

A browser window should open and you will see a listing of the files in the current directory. At the bottom of the Edit menu you should see

<p class="center" markdown="0"><img alt="nbextensions config" src="figs/notebookext1.webp"></p>

You should now see a menu item called **Nbextensions**, as illustrated in the figure.
   
<p class="center" markdown="0">
   <img alt="Nbextensions" src="figs/nbextensions.webp">
</p>

Clicking on the **Nbextensions** menu will allow you to load extensions as  desired. I recommend several, including 

+ Autopep8
+ Codefolding
+ Collapsible Headings
+ ExecuteTime

![Extensions](figs/extensions.webp)

### Extensions in Jupyter Lab

We will need a couple of extensions to be installed in JupyterLab. The first step to install those is to enable them by clicking the jigsaw icon as shown in the figure below and then clicking on the **Enable** button.

<p class="center"><img alt="Enable" src="figs/labext1.webp"></p>

Once you have enabled extensions, you can use the search box to install the two extensions shown here

<p class="center"><img alt="?" src="figs/labext2.webp"></p>

Alternatively, you can issue the following statement in the terminal

~~~~ shell
jupyter labextension install @jupyter-widgets/controls @jupyter-widgets/jupyterlab-manager \
   jupyterlab-plotly jupyter-matplotlib
~~~~

### Jupyter Notebook

By default, Jupyter notebook uses a fixed-width column no matter how wide you
make your browser window. Perhaps this is just what you want, but I have
sometimes found it very convenient to allow the column to expand with the
window.

You can override default styling of notebook cells by preparing a `custom.css`
file and placing it in `~/.jupyter/custom/custom.css`. The following example
allows the width of the cell to expand as the window is made wider:

~~~~ css
.container {
  width: 100% !important;
  margin-right: 40px;
  margin-left: 40px;
}
~~~~


### Matplotlib

I dislike matplotlib's defaults. Although it is possible to customize each plot,
it is convenient to put common changes in a preferences file. A copy of the
format file is located in `site-packages/matplotlib/mpl-data/matplotlibrc`. Save
a copy of this file at `~/.config/matplotlib/matplotlibrc` on a Unix/Linux
system or in `$$HOME/.matplotlib/matplotlibrc` on other systems.

This file has all sorts of options, all of them commented out with leading hash
tags. Uncomment the lines you wish to modify and set appropriate values. On my
system, I have set the following lines:

~~~~ shell
saeta@Saeta-MBP19~/.c/matplotlib> grep "^[^ #]" matplotlibrc
backend             : macosx
font.family         : serif # sans-serif
font.size           : 12.0 # 10.0
font.serif          : Utopia, DejaVu Serif, Bitstream Vera Serif, ...

text.usetex         : True ## use latex for all text handling. 

xtick.top           : True ## draw ticks on the top side
xtick.direction     : in   ## direction: in, out, or inout
ytick.right         : True ## draw ticks on the right side
ytick.direction     : in   ## direction: in, out, or inout

savefig.format      : pdf  ## png, ps, pdf, svg
savefig.transparent : True ## setting that controls whether figures are saved with a
                           ## transparent background by default
~~~~

### Using LaTeX in matplotlib labels

If you set `text.usetex: True` in the configuration file, you can take full
advantage of TeX formatting in labels and annotations. However, beware that
certain characters that have special meaning in TeX, such as the underscore, may
cause labels to throw TeX errors unless they are in math mode. If you have
set the default text style to use TeX, you can always pass the optional
keyword argument `usetex=False` in the label to avoid the problem.


### Configuring defaults in a Jupyter notebook

You can change the defaults used to generate graphs in a notebook by writing
values directly to the `matplotlib.rcParams` dictionary.

~~~~ python
import matplotlib as mpl
mpl.rcParams['figure.figsize'] = [12, 8] # You can adjust the plot size
mpl.rcParams['axes.titlesize'] = 18
mpl.rcParams['axes.labelsize'] = 14
mpl.rcParams['xtick.labelsize'] = 14
mpl.rcParams['ytick.labelsize'] = 14
mpl.rcParams['legend.fontsize'] = 'large'
~~~~

If you'd like to see *all* the available parameters and their current values,
launch Python and run

~~~~ python
import matplotlib as mpl
for k, v in mpl.rcParams.items():
    print(f"{k: >32s} = {v}")
~~~~

The output runs to 300+ lines.
