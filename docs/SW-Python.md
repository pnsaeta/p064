{:menu SW}


# Python

This course assumes a basic familiarity with Python (and a deep and abiding love for Google and Stack Overflow, although ChatGPT and other sources of artificial misinformation may worm their way into your toolbox). As a lightning refresher, recall that you can define functions using the following syntax:

~~~~ python
def myfunc(x, *args, **kwargs):
    """
    This function has no real purpose in life other than to illustrate fixed
    and variable arguments. The first argument, x, is required; if you don't pass
    some argument, Python will throw an error. On the other hand, if you only supply
    a single argument, args will be an empty tuple and kwargs will be an empty 
    dictionary. There is no error, and no optional arguments are present.
    """
    pass # a real function should do something!
~~~~

+ If we call `myfunc` with `myfunc(1,2,3)`, then `x` will be 1, `args` will be `(2,3)`, and kwargs will be empty.
+ If we call `myfunc(1, 2, 3, a=4, b=5)`, then `x` will be 1, `args` will be `(2,3)`, and `kwargs` will be `{'a': 4, 'b': 5}`.

Inside `myfunc`, you can treat `args` as an ordinary tuple and `kwargs` as an ordinary dictionary that maps keyword (arguments) to their values.

## Classes

Classes in Python may have both **data** and **function** members (function methods are also known as **methods**). The purpose of classes is to associate the two, so you don't have to pass a laundry list of parameters to every function that involves the object. Rather, the member function gets passed a reference to the object itself, from which it can access whichever data members or functions it needs. Classes have a number of standard functions that they may override to do common tasks. I'll illustrate with an example

~~~~ python
class FourierExpansion:
    """
    Represent the Fourier expansion of a given function using specified boundary conditions
    and a given (finite) number of terms.
    """

    def __init__(self, f, leftBC, rightBC, n_max=20): # this is the constructor
        """
        The constructor get called when we try to instantiate an object of 
        the class FourierExpansion with a call such as fe = FourierExpansion(f, …)

        The first argument is conventionally called "self" and refers to the object
        itself. The constructor may take any number of additional arguments, or none
        at all. In this case, there are three required arguments, and one that is 
        optional, but has a default of 20.

        A common thing to do is to store the arguments as data members of the object, 
        as illustrated below.
        """
        self.function = f      # Store the given function (which is assumed to take a single argument)
        self.a = leftBC[0]     # Each BC is a tuple (x, T/F), where x is the position of the boundary
                               # and the second argument describes the condition at x; if it is True,
                               # then the basis function must vanish at this boundary; if it is False,
                               # then the derivative of the basis function must vanish at this boundary.
                               # We store the positions here and in the next statement.
        self.b = rightBC[0]
        self.L = self.b - self.a
        bcs = leftBC[1], rightBC[1] # bcs describes whether the function of its derivative vanishes

        self.basis = np.sin if bcs[0] else np.cos # we will use either sines or cosines as basis functions
                                # for the expansion, depending on whether the function vanishes at a (sines)
                                # or its derivative vanishes at a (cosines)
        # additional code

    def __str__(self):
        return f"Fourier expansion of {self.function} over the range [{self.a}, {self.b}]"
    
    def __call__(self, x):
        """
        This function gets called when you write FE(x), where FE is an object of class
        FourierExpansion and x is some argument. That is, it allows you to treat the
        object as a function, which is sometimes convenient.
        """
        return x * 3 # not particularly useful, but you get the idea
    

~~~~

To assist Python debuggers/linters, it is considered good practice to define in the constructor **all** data members that will ever be present in the object, even if that means initializing them to `None` or `[]`. It is also good practice to keep functions brief. If you need to do a lot of work in the constructor, consider having it define all necessary data members and then call one or more auxilliary functions to perform the necessary computation to fully initialize the object.

### Important default methods

A number of standard methods are automatically defined (or available) for classes.
See [the Python documentation](https://docs.python.org/3/reference/datamodel.html#special-method-names) for a complete list of the special method names. I'll cover just a few here.

+ `__init__(self[, ...] )` the constructor, which is called to instatiate objects of the class type
+ `__str__(self)`: a function to generate a string representation of the object
+ `__call__(self[, args...])`: make an object serve as a function; given a list of arguments between parentheses, return some function of the arguments
+ `__getitem__(self, key)` implements `self[key]`
+ `__setitem__(self, key, value)` sets the data member `key` of the object with the value `value`, as in `self[key] = value`
+ `__dict__(self)` returns a dictionary of the data fields and public methods of the object

### Comparing objects and dictionaries

Let's contrast some basic operations on dictionaries and objects. Suppose we have a dictionary `dic` and an object of some class or other `obj`

<table class="nicetable">
    <tr><th>task</th><th>dictionary</th><th>object</th></tr>
    <tr><td>is field <code>f</code> in it? </td><td> <code>'f' in dic</code> </td><td> <code>hasattr(obj, 'f')</code></td></tr>
    <tr>
      <td>access field <code>f</code></td>
      <td><code>dic['f']</code> <em>or</em> <code>dic.get('f', [optional default value])</code></td>
      <td><code>obj.f</code> <em>or</em> <code>getattr(obj, 'f')</code></td>
    </tr>
    <tr>
      <td>set field <code>f</code> with value <code>v</code></td>
      <td><code>dic['f'] = v</code></td>
      <td><code>obj.f = v</code> <em>or</em> <code>setattr(obj, 'f', v)</code></td>
    </tr>
</table>

What happens if you reference a key in a dictionary that doesn't have that key? You get an error. You could either include that call in a `try ... except` block to catch an exception, you could first test whether it has the key with `if 'key' in dic`, or you could just use `dic.get('key')`. If the key isn't present in the dictionary, the value `None` is returned. However, you can also supply a default value as an optional second argument to the `get` call, which will be returned if the key is not present in the dictionary.

Similarly, you will get an exception if you try to access a member of an object that doesn't exist, whether you use the `obj.f` syntax or the `getattr(obj, 'f')` version. However, you can use `hasattr(obj, 'f')` to determine whether the object has that field/key.