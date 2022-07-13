{:menu SW}
{::comment}menu-start{:/comment}

<div class="dropdown">
<label id="hamburger-menu"><img id="hamburger" src="figs/hamburger.png"></label>
<div class="dropdown-content">
<ul>
<li><a href="SW-Installation.html">Installing necessary software</a></li>
<li><a href="SW-Jupyter.html">Jupyter notebooks</a></li>
<li><a href="SW-NumPy.html">NumPy</a></li>
<li><a href="SW-Matplotlib.html">Matplotlib</a></li>
<li><a href="SW-MPLFormatting.html">Formatting Plots</a></li>
<li><a href="SW-pandas.html">Pandas</a></li>
</ul>
</div>
</div>

{::comment}menu-end{:/comment}


[Back to Installation](SW-Installation.md)

# Using Google Colab

Google Colab is a hosted version of JupyterLab that makes available the standard
libraries we need: NumPy, SciPy, Matplotlib, pandas, etc. If these are all you
need, you’re all set. However, if you would like to load your own Python code to
use in a notebook, you need to take some additional steps.

## Loading Python code from Google Drive

The easiest way to go is to copy the Python file(s) to a folder on your Google
Drive. To illustrate, I have made a folder `python` in my home directory on
Google Drive. Into that folder I have deposited a module called `fit`. Here's
how I can make the Python files in that module accessible to Colab.

First, I’ll show the layout of the files in the python folder:

~~~~
cd '/content/gdrive/My Drive/python'
ls

fit/

ls fit/

gaussian.py  main.py       sinusoid.py
__init__.py  line.py       __pycache__/
~~~~

Now, here’s what I would put in a colab notebook to allow me to access the Fit
class and its subclasses, which are declared in the `fit/__init__.py` file.

~~~~ python
from google.colab import drive
drive.mount('/content/gdrive') # this step will ask you to authenticate;
(you log in and enter the token Google generates)

import sys
sys.path.insert(0, '/content/gdrive/My Drive/python') # add the python directory
# to the path searched by Python when looking for file/modules.

import fit

help(fit.Fit) # get help on a class defined in the fit module

Help on class Fit in module fit.main:

class Fit(builtins.object)
 |  Object to perform a fit and compute residuals and chisq.
 |  
 |  If the fit is successful, the field Fit.valid is set to True.
 |  
 |  Methods defined here:
 |  
 |  __call__(self, t:numpy.ndarray)
 |      Evaluate the fitting function using current parameter values.
 |  
 |  __init__(self, function, x:numpy.ndarray, y:numpy.ndarray, p0:numpy.ndarray, **kwargs)
 |      kwargs may include hold="1011", where each 0 corresponds
 |      to a parameter allowed to vary and 1 to a value held fixed.
 |      If the function passed has a .tex attribute, it is assumed
 |      to be a string that can be passed to tex to describe the
 |      function in the fit annotation. Subclasses may define a
 |      string variable tex_f for this purpose.

~~~~
