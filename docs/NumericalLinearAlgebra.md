# Numerical Linear Algebra with NumPy

+ [Back to Linear Algebra](LinearAlgebra.md)
+ [Introduction to NumPy](NumPy.md)

* toc
{:toc}


The standard way to access the routines of NumPy in a Python program is with an import statement of the form

    import numpy as np


A basic numerical type in NumPy is the `np.ndarray`, which can represent an array of arbitrary numbers of dimensions. You can create an array from basic Python types such as **lists** and **tuples** using `np.asarray(list_or_tuple)`. For example

    a = np.asarray([[1, 2, 3], [4, 5, 6]])

generates the $$2\times 3$$ array

    array([[1, 2, 3],
           [4, 5, 6]])

Besides listing all elements of a NumPy array, you can use a number of convenience functions to generate them:

+ `np.arange(start, end, dx)` generates a one-dimensional array of values (start, start + dx, start + 2 * dx, ..., start + n * dx) where the final value satisfies start + n * dx < end. For instance, `np.arange(1, 4, 1)` produces  `array([1, 2, 3])`
+ `np.linspace(start, end, n)` generates a one-dimensional array of values that divides [start, end] into $$n-1$$ equal intervals, so that `np.linspace(1, 4, 4)` produces `array([1, 2, 3, 4])`. That is, `linspace` includes the end points, whereas `arange` does not include its end point.
+ `np.zeros((nrows, ncols))` generates a nrows by ncols array of zeros
+ `np.ones((nrows, ncols))` generates a nrows by ncols array of ones
+ [See the NumPy page on Array creation routines](https://numpy.org/doc/stable/reference/routines.array-creation.html) for more information.


## Properties of NumPy arrays

Suppose that you want to multiply each element in a list by 3.2. In standard Python, you could write a list comprehension of the form

    b = [x * 3.2 for x in a]

for a list stored in `a`. If, instead, you use a NumPy array, you can simplify the notation to eliminate explicit loops:

    b = np.asarray(a) * 3.2

This notation also works for multiplying (or performing similar arithmetic operations) on all elements of a NumPy array of arbitrary dimensions.

All of the standard functions have NumPy versions that “broadcast” in this way over the elements of the array that they are passed. So, the following code computes a comb of equally spaced $$x$$ values and computes the corresponding sine values and then uses matplotlib to plot the result:

    import matplotlib.pyplot as plt
    x = np.linspace(0, np.pi, 101)  # create an array of equally spaced x values
    y = np.sin(x)                   # compute the corresponding y values via broadcasting
    fig, ax = plt.subplots()        # start a matplotlib plot
    ax.plot(x, y)                   # by default, matplotlib connects the points
    ax.set_xlabel('$x$')            # dollar signs turn on LaTeX; x is set in italics
    ax.set_ylabel(r'$\sin{x}$')     # a raw string protects the backslash from escaping

![Sine plot](figs/sineplot.png)

You can [read more about NumPy's universal functions](https://numpy.org/doc/stable/reference/ufuncs.html) in the official documentation. They include all the standard trigonometric, exponential, and hyperbolic functions, degree-radian conversions, rounding, etc. Some “unusual” ones you might find handy:

+ `square(x)` computes the square of all elements of `x`
+ `cbrt(x)` computes the cube root of all elements of `x`
+ `arctan2(y, x)` computes the arctangent of (x,y) points, in radians, making sure to get the quadrant correct
+ `degrees(x)` converts values in `x` from radians to degrees; `rad2deg(x)` does the same thing
+ `isnan(x)` returns a boolean array of True values if `x` is not a number and False otherwise
+ `floor(x)` returns the greatest integer less than each value of `x`; see also `round(x)` and `trunc(x)`

### Array axes

Sometimes you want to operate row-wise or column-wise on a two-dimensional array. Consider the following example:

    from numpy.random import default_rng
    rng = default_rng()                     # initialize a random number generator
    m = rng.uniform(-5., 5., size=(2, 3))   # make a row of random numbers in [-5.0, 5.0) with 2 rows and 3 columns
    m

    array([[-1.30298926,  0.29909209, -2.43088339],
           [ 0.49986483,  0.86389192,  3.21737843]])
    
    m.max()
    3.2173784294384173                      # the maximum single value in the array

    m.max(axis=0)                           # find the maximum value in each column
                                            # by "collapsing" over the row axis
    array([0.49986483, 0.86389192, 3.21737843])

    m.max(axis=1)                           # find the maximum value in each row
    array([0.29909209, 3.21737843])

This approach is not limited to two-dimensional arrays:

    m3 = rng.uniform(-10., 10., size=(2,3,4))
    m3
    array([[[ 6.90429787, -2.40068511,  5.68998764,  8.11941128],
            [-8.5648789 , -3.3223694 ,  5.93420326, -6.52864494],
            [-3.95970545, -8.60586592, -9.09347286, -3.33440424]],

           [[ 9.53219154,  4.0103738 ,  7.36151971,  3.82092826],
            [-8.00710273,  9.17986084,  0.05692238,  7.33611053],
            [ 7.51311752, -3.20018323,  8.04918146,  1.9521936 ]]])
    
    m3.max()
    9.532191544702176

    m3.max(axis=0)                          # "collapse" over rows, yielding an array
                                            # with 3 rows and 4 columns
    array([[ 9.53219154,  4.0103738 ,  7.36151971,  8.11941128],
           [-8.00710273,  9.17986084,  5.93420326,  7.33611053],
           [ 7.51311752, -3.20018323,  8.04918146,  1.9521936 ]])
    
    m3.max(axis=1)
    array([[ 6.90429787, -2.40068511,  5.93420326,  8.11941128],
           [ 9.53219154,  9.17986084,  8.04918146,  7.33611053]])
    
    m3.max(axis=2)
    array([[ 8.11941128,  5.93420326, -3.33440424],
           [ 9.53219154,  9.17986084,  8.04918146]])
    
    m3.max(axis=(0,1))                      # "collapse" over the first two indices, yielding
                                            # a 4-element array
    array([9.53219154, 9.17986084, 8.04918146, 8.11941128])
    
    m3.max(axis=(0,2))
    array([9.53219154, 9.17986084, 8.04918146])

In summary, functions such as `sum`, `max`, `min`, etc. operate by default on all elements of multidimensional arrays, but can also be specialized to work along various directions.

## 