# Using Jupyter Notebooks

* toc
{:toc}

Jupyter notebooks use a browser to provide an interactive computation and
authoring environment that allows one freely to combine text (including LaTeX
equations), graphics, computation, and the results of computations in a single
window. Jupyter Notebook is the more established code base; Jupyter Lab is newer, has a number of nice features, but is buggier than the Notebook interface; use it at your own risk!


Notebook cells can include text written in **Markdown** (such as this cell),
**Code** (the cell below this one) or **Raw** mode. Markdown cells can include
formatting information and math expressions written in LaTeX (more about that in
a bit). Raw cells just hold the text and don’t interpret symbols that would
change the font or show equations if they were processed as Markdown. Code cells
get submitted to the Jupyter kernel (and passed to the Python interpreter). 
This cell is in Raw mode so I can illustrate the basics of Markdown.

~~~~ markdown
    Italics: *this will be in italics*

    Boldface: **whereas this statement is in boldface.**

    Code: `def fred(x, y)`

    - a bullet
    - in a list

    1. Or a numbered
    2. list

    To write math, surround with dollar signs:
    $E = m c^2$ or $x = \frac{-b \pm \sqrt{b^2 - 4 a c}}{2a}$

    To center an equation on its own line, use
    \begin{equation}
    \sin^2 \theta + \cos^2 \theta = 1
    \end{equation}

    Notice that mathematical functions should be preceded with a backslash
    and that you get Greek letters by preceding their name in English with a backslash. 

    For more information about Markdown, check out the **Markdown Reference**
    item in the Jupyter **Help** menu.
~~~~

And this is how that same text appears when used in a Markdown cell


Italics: *this will be in italics*

Boldface: **whereas this statement is in boldface.**

Code: `def fred(x, y)`

- a bullet
- in a list

1. Or a numbered
2. list

To write math, surround with dollar signs: $$E = m c^2$$ or $$x = \frac{-b \pm \sqrt{b^2 - 4 a c}}{2a}$$


To center an equation on its own line, use
\begin{equation}
  \sin^2 \theta + \cos^2 \theta = 1
\end{equation}

Notice that mathematical functions should be preceded with a backslash and that
you get Greek letters by preceding their name in English with a backslash. 

For more information about Markdown, check out the **Markdown Reference** item
in the Jupyter **Help** menu. 

## Code

The first step in a new notebook is a line containing a magic command that
allows graphs to appear in output cells of the notebook. Magic lines start with
a % (and you can’t put a comment after them the way you can in Python. To
execute the commands in a cell, make sure the cell is selected and press
**shift-enter** or **shift-return**. Or, if you are a mouse person, click the
triangle symbol at the top of the page. 


~~~~ python
# the following line is for jupyter notebook
%matplotlib notebook
# if you use jupyter lab, replace "notebook" with "widget"
import numpy as np               # np is the standard abbreviation for numpy
import matplotlib.pyplot as plt  # plt is the standard abbreviation for pyplot
~~~~

## A simple plot

To illustrate how you can make a plot and have it show up in the notebook, let’s
try a very simple example. 

~~~~ python
fig, ax = plt.subplots()
ax.plot([1, 2, 3], [4, 2, 3], 'r*', label="stars")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.legend();
~~~~

<p class="center" markdown="0">
  <img src="figs/intro-1.png" style="width: 400px;">
</p>


Some explanations:

- `plt.subplots` returns both a figure object and an axes object
- `ax.plot` takes two lists, one for the x values, and the other for the y
  values. They must have the same length! The optional argument `'r*'` says to use
  red star symbols, and the label allows the legend to associate a label with
  the symbol in the legend. 
- `ax.set_xlabel` and `ax.set_ylabel` take a string. The string can contain
  LaTeX commands (see below).
- `ax.legend();` says to show a legend of the traces on the plot, letting
  matplotlib decide the best location for it. The semicolon suppresses the
  output of this command. (You can remove it and run the command again to see
  what gets returned.) 

## Plotting a function

To plot a function in matplotlib you need to first compute $$x$$ values and $$y$$ values. Let’s see how to plot the function
\begin{equation}
    y(x) = \frac{1}{\sqrt{(1-x^2)^2 + 4 \zeta^2 x^2}}
\end{equation}
where $$\zeta$$ is called the *damping parameter* and *x* represents the ratio of
the frequency of an oscillator to its *natural frequency*, as you learned in E79.

Can you imagine what the curve looks like for $$x \ge 0$$? See if you can guess
the shape of the curve for a value of $$\zeta \ll 1$$ and also for $$\zeta >
1$$. Then proceed.

We need to pick a suitable range of the independent variable `x`. I’m going to
start at zero and go to $$x = 4$$ for starters. Let’s use 201 points over that
interval. Fortunately, numpy has a very convenient function we can use:


~~~~ python
x = np.linspace(0, 4, 201) # make an array of 201 equally spaced
                           # values between 0 and 4, inclusive
x                          # show the values we just computed
~~~~


*Can you explain why we used 201 points, not 200?*

Now we need to calculate the corresponding values of $$y$$. But those values
depend on the value of $$\zeta$$, which we haven’t yet specified. Let’s write a
little function to take two inputs, the `x` array of values and single value of
$$\zeta$$ and produce the corresponding values of `y`.


~~~~ python
def myfunc(x: np.ndarray, zeta:float):
    """Calculate the y values given by the equation defined above in the section
    called Plotting a function
    """
    return 1.0 / np.sqrt((1 - x*x)**2 + 4 * zeta**2 * x*x)
~~~~

Some explanations:
- `myfunc` takes two arguments, and their types are indicated after the
  colons. Where possible, specifying the type expected for the argument makes
  your functions easier to interpret. 
- the type `np.ndarray` is the kind of array that gets returned from
  `np.linspace`; it is a very commonly used type in numpy. 
- A docstring helps explain the purpose of the function.
- the square root function is defined differently in numpy than in the Python
  `math` module. The numpy version notices when an argument is not a single
  number but a np.ndarray of values and automatically calculates for each value
  in the array. 

Read that last bullet point again. Numpy calls this feature *broadcasting*; it
is **really** nice. It means we don’t need to write loops to compute array
values; numpy will take care of that for us. 

Let’s try a curve with a small value of damping parameter $$\zeta$$.

~~~~ python
    y = myfunc(x, 0.1)
    fig, ax = plt.subplots()
    ax.plot(x, y, label="0.1")
    ax.set_xlabel("$x$")
    ax.set_ylabel("$y$");
~~~~

<p class='center' markdown='0'>
  <img src='figs/intro-2.png' style='width: 500px;'>
</p>



Okay, that looks like a peak near $$x = 1$$ (which means that the frequency is
near the *natural frequency*). Now let’s add a curve on the same axes but with
$$\zeta = 0.5$$ this time. 

### Adding a second curve

~~~~ python
y2 = myfunc(x, 0.5)
ax.plot(x, y2, label="0.5")
ax.legend();
~~~~

<p class='center' markdown='0'>
  <img src='figs/intro-3.png' style='width: 500px;'>
</p>

<p class='mycap'>Stronger damping attenuates the resonance peak.</p>



Well, that’s interesting. Increasing the damping parameter really pushed the
peak down. I wonder if we could make a plot that showed curves for several
values of damping parameter. Let’s try. 


~~~~ python
fig, ax = plt.subplots()
ax.set_xlabel("$$x$$")
ax.set_ylabel("$$y$$")
for zeta in (0.05,0.1, 0.2, 0.5, 1, 2):
    y = myfunc(x, zeta)
    ax.plot(x, y, label=r"$\zeta = %g$" % zeta)
ax.legend();
~~~~

<p class='center'><img src="figs/intro-4.png" style="width: 500px;"></p>
<p class="mycap">Now our resonance cup runneth over!</p>



Can you summarize the behavior you observe?

### Logarithmic axes

It turns out that this plot will look better if we use logarithmic axes. Let’s see what that looks like. For grins, I’m going to compute a more suitable set of $$x$$ values first.


~~~~ python
logx = np.power(10, np.linspace(-1, 1, 201))
fig, ax = plt.subplots()
ax.set_xlabel("$$x$$")
ax.set_ylabel("$$y$$")
for zeta in (0.05, 0.1, 0.2, 0.5, 1, 2):
    y = myfunc(logx, zeta)
    ax.loglog(logx, y, label=r"$\zeta = %g$" % zeta)
ax.legend();
~~~~

<p class="center"><img src="figs/intro-5.png" style="width: 500px;"></p>
<p class="mycap">Now our resonance cup runneth over in style!</p>



How would you summarize the behavior you observe in this plot?

## Quiz

Let’s see if you can now apply what we’ve explored so far.

1. Make an array called `hermione` that has 51 equally spaced points between 0 and 1, inclusive.
2. Make a plot of the square of the values in `hermione`. Use blue dots to plot
   the points by passing **'bo'** to the `plot` function. 

## Pandas

Pandas is a module that provides features somewhat akin to a spreadsheet or
database and meshes very naturally with both numpy and matplotlib. Before we can
explore it, we need to import this module. 


~~~~ python
import pandas as pd # pd is the standard abbreviation for pandas
~~~~

I’m going to recompute the values plotted in the previous figure and store them
in a pandas DataFrame for easy display. 


~~~~ python
# First make a dictionary of vectors
values = {z:myfunc(logx, z) for z in (0.05, 0.1, 0.2, 0.5, 1, 2)}
# Now create a pandas DataFrame to store them
df = pd.DataFrame(values, index=logx)
df
~~~~

<p class="center"><img src="figs/intro-pandas.png"></p>
<p class="mycap">Displaying a pandas DataFrame.</p>




You can access individual columns using their name:


~~~~ python
df[0.2]
df.plot(logx=True, logy=True, xlabel="$$x$$", ylabel="$$y$$");
~~~~

<p class="center"><img src="figs/intro-6.png"></p>
<p class="mycap">With the curves in a pandas DataFrame, the plot command takes a single line.</p>



Notice how the value of $$\zeta$$ doesn’t affect the frequencies either
significantly below the natural frequency ($$x = 1$$) nor significantly above it,
where all the curves fall off in the same way with increasing frequency. Also
note how the plotting operation could be achieved with a single call, with the
various properties adjusted with keyword arguments. 

### Practice with pandas and matplotlib

I have placed some experimental data with uncertainties at
https://www.physics.hmc.edu/courses/p134/CircularMoore2004.txt. The $$x$$ axis
variable is the position of the detector (in mm); the $$y$$ axis variable is the
observed light intensity (in volts); the $$y$$ uncertainty values are in the same
units. 

Prepare a plot of these data using discrete points for the data, error bars set
according to the uncertainties, and see if you can style your graph *exactly*
like the one shown below. Feel free to consult the matplotlib documentation as
liberally as you like! 


<p class="center"><img src="figs/moore.png"></p>
<p class="mycap">Target practice: Can you make your plot look *exactly* like this one?</p>

**Hints**

+ You can load the data into a convenient data structure defined by pandas with
   some code like 

~~~~ python
import pandas as pd
the_data = pd.read_table('filename_or_URL')
~~~~

You can then see a table of the data by entering `the_data` in a Jupyter
cell. You can access individual columns of the data by name: `the_data['x']` or
`the_data.x`. 

+ The command to plot with error bars is `ax.errorbar(xvals, yvals, yerrors)`
   and you can add lots of keyword arguments to make things look the way you
   wish. To make a pleasant-looking plot, I recommend scaling the errors in
   Moore’s data by a factor of 50 (yeah, he was good!). The data in the
   $$x$$ column is the position of the detector in millimeters, while the data in
   the columns labeled `I` and `I_err` are the intensity and intensity errors,
   with values in volts. 

+ Potentially interesting keywords:
    - `marker`
    - `fmt`
    - `markersize`
    - `capsize`

### Modifying the way a trace is displayed

You can modify the way a trace appears with both positional and keyword
arguments to the call to =plot(xvals, yvals)=. For a few basic colors, you can
use the following shortcuts:

| color code   | meaning | symbol code | meaning       |
|------------+---------+-------------+---------------|
| `'b'`        | blue    | `'o'`         | filled circle |
| `'r'`        | red     | `'.'`         | dot           |
| `'g'`        | green   | `'*'`         | star          |
| `'k'`        | black   | `'-'`         | line          |
| `'y'`        | yellow  | `'v'`         | triangle down |
| `'w'`        | white   | `'^'`         | triangle up   |
| `'m'`        | magenta | `'s'`         | square        |
| `'c'`        | cyan    | `'d'`         | thin diamond  |
|------------+---------+-------------+---------------|

You can also use an RGB or RGBA notation, such as =#0f0800= or =#0f0f0f80=. To
combine such a color specification with a marker designation, use a command such
as the following

~~~~ python
ax.plot([0, 0.25, 0.5, 0.75], [1, 0.75, 0.5, -0.25], 'o', color='#44bb60')
~~~~

See [markers](https://matplotlib.org/api/markers_api.html?highlight=marker#module-matplotlib.markers) for more marker options and [colors](https://matplotlib.org/api/colors_api.html?highlight=color#module-matplotlib.colors) for more options for representing colors.

[Next step: formatting in Matplotlib](MPLFormatting.md)