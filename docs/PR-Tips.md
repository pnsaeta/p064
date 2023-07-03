{:menu PR}
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
<li><a href="PR-Project.html">Projects</a></li>
<li><a href="PR-Tips.html">Projects Tips</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


# Projects Tips

* toc
{:toc}


## Organizing Data

It used to be that how you organized data was your own business. Modern practice requires you to organize your data files in a logical way and to make data accessible to others upon need or request. You should adopt the mindset that insists upon organization of data files, which requires both sensible naming schemes and documentation of file formats.

Text files have the great virtue of being universally readable. Programs as different as spreadsheets, web pages, statistical packages, and generic programming environments can be taught to load and understand sensibly formatted text data. For small batches of data, this is the most transparent way to go. For larger quantities of data, binary storage is more sensible.

### Text Files: the Great Divide (and a long digression)

Once upon a time there was a fledgling operation seeking to generate a successor to the [CP/M](https://en.wikipedia.org/wiki/CP/M) operating system that they might persuade computer manufacturers to adopt as their "disk operating system." Said operation was developed by a Harvard undergraduate who decided to drop out to pursue the business opportunity of delivering yesterday's technology at an affordable price. Thus was born the Microsoft empire. MS-DOS was hardly an innovation on CP/M, but Gates and Allen were successful in persuading IBM to use the Microsoft operating system to fuel their innovation, the IBM-PC, built to counter a threat generated Heathkit, Commodore, and the duo of Steve Jobs and Steve Wozniak with the Apple II personal computer, followed by the Lisa and the Macintosh. All these efforts aimed to bring computing to the masses with hardware that was both capable and affordable. As your parents about it.

Where UNIX used the linefeed character (\n) to separate lines in a text file, and where Apple used the carriage return (\r) for this purpose, Gates opted for the belt-and-suspenders approach of using both; lines in DOS (and then Windows) would be separated by **a carriage return and a line feed**. I have never understood the rationale. Here's an innovation! "Let's use twice as many characters as necessary." After Jobs was ousted from Apple and founded NeXT, which developed a UNIX-based operating system, he converted from \r to \n, so that when he returned to the helm of Apple and replaced the MacOS with the UNIX-based operating system developed at NeXT, the line separator on Macintosh went from carriage return (\r) to line feed (\n), consistent with other flavors of UNIX.

A table of data typically has rows and columns, each of which needs to be separated (delimited) by a suitable marker in a text file. The standard adopted in the DOS/Windows world was/is **comma-separated-values (CSV)**. In my *excessively* humble opinion, **this choice is absolutely nuts**. Not only do people often use a comma to separate groups of three digits, but many European languages use the comma as the decimal point. To accommodate this unfortunate choice, the Microsoft crowd "solved" the problem by requiring that in situations where a comma might have a different meaning, fields should use double quotation marks to "shield" any embedded commas from the code that seeks to parse a CSV file. What could be simpler? Well, how about using a character that is **never** used in normal text? Indeed, the tabulator (tab) character was invented just for this purpose, so why not use it as a column separator? Why indeed!

When writing and reading text files with pandas or numpy, you can set the separator to use with the `sep` keyword parameter. By default, it is "comma" for CSV, but for the reasons listed above, this choice would appear to privilege the unfortunate choice made by Gates et al.

## Managing Long Runs

If your code produces lots of data over a long run, rather than building up a large list of results, consider writing intermediate results to disk for later retrieval and analysis. How to do this depends a bit on the format of the data you need to store. In all cases, think carefully about the file-naming scheme you will use to help you identify how far the computation has gone, what remains to be done, and how to identify a particular result you may be looking for. I often use a naming scheme that begins with a datecode (or uses the datecode to create a folder for results generated on that date). I'll offer a few examples in the code below.

~~~~ python
from datetime import datetime
from pathlib import Path

def datecode(when=datetime.today()):
    "Return a datecode string of the form YYMMDD"
    return when.strftime('%y%m%d')

def path(fname:str, ext=".txt"):
    """Generate a path to save a file to a datecode folder.
    Pass in the base filename, and optionally, a file extension.
    """
    p = Path(datecode())
    p.mkdir(exist_ok=True)  # make the date directory if it doesn't exist
    p = p / f"{fname}{ext}"
    return p

# The following will open a file named "testing.txt" in a subfolder of the current folder
# with today's datecode and write a public-service announcement therein.
with open(path('testing'), 'w') as f:
    print("This is a test of the emergency broadcast system. This is only a test.", file=f)
~~~~


### Numpy arrays

You can save numpy arrays in binary format, which takes less space on disk than converting to text and which loads a great many times faster.

~~~~ python
A = np.random.random((10, 10))
with open(path("A.npy"), "wb") as f:
    np.save(f, A)
~~~~
Notice that you must first open a file in binary mode to pass as the first argument to the `np.save()` function.

You can ask for information about the file format from the command line with the `file` command. Here's what it says about `A.npy`:

~~~~ shell
> file A.npy
A.npy: NumPy data file, version 1.0, description {'descr': '<f8', 'fortran_order': False, 'shape': (10, 10), }
~~~~

To load such a file back in, call `np.load` as follows

~~~~ python
with open("A.npy", "rb") as f:
    newA = np.load(f)
~~~~

### Pandas DataFrames

A Pandas DataFrame can be saved in a variety of formats. If you intend to look at the data, in a text editor, a spreadsheet, or another computing environment, use `df.to_csv()` to write to a delimited text file (example below). If you intend to load the DataFrame back into Python as a DataFrame, the better approach is to "pickle" the data structure, which saves it in a Python native binary format, using `df.to_pickle("data.pkl)` to store and `pd.read_pickle("data.pkl")` to restore the DataFrame.

~~~~ python
df.to_csv("my_frame.txt", sep="\t") # export in text format, but use tabs to delineate columns, not commas
~~~~


## Parallelizing Code

In some simulations, the next step depends on the previous and there is no way to compute the steps in a different order. In others, you need to run simulations for a variety of different initial conditions or parameters and each is independent of the others. In the latter case, you can use a simple form of parallelism in Python that allows your program to employ more than one CPU (core) at a time.

To illustrate, let us suppose that we have written an `Ising` class that runs a simulation of a 2-dimensional Ising model of given size for a chosen temperature. Each instance of `Ising` is independent of all others and can run independently. We can write a simple function that accepts a list of arguments to specify the size, duration, and temperature of a run of `Ising` and return some summary statistics of the run in the form of a dictionary.

~~~~ python
def run_one(args):
    N, T, rounds, skip = args      # unpack the arguments
    i = Ising(N, 1, 0, T=T)        # run Ising on a NxN grid with J = 1, B = 0, and T=T
    i.update(rounds)               # iterate rounds times
    d = {'T':T} | i.average(skip)  # create a dictionary of average results and the temperature of this simulation
    return d
~~~~

With a routine to accept the parameters of a "run" and return the results, we can now farm out a number of runs to more than one CPU using the Python multiprocessing library as follows.

~~~~ python
import multiprocessing as mp

temps = np.arange(1.0, 2.0, 0.1)
PROCESSES = 6
N = 256
args = [(N, t, 1000, 100) for t in temps] # generate the list of argument sets

with mp.Pool(PROCESSES) as pool:          # create a pool of processes
    res = pool.map(run_one, args)         # use the pool to run the run_one function on each set of args
df = pd.DataFrame(res)                    # when every simulation has been run and assembled in res, 
                                          # generate a DataFrame from the list of dictionaries
~~~~


## Animation

[I have generated a new page with more hints on animations.](SW-Animation.md)

