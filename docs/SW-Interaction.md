{:menu SW}

# Interactive Animations in Jupyter

* toc
{:toc}

Jupyter notebooks make it possible to produce interactive simulations/animations that are controlled by interactive widgets, such as sliders and buttons. When appropriately configured, changing the value of a slider or clicking a button triggers Python to run an update function, which can then ask the notebook frontend to redisplay something. The details are a bit tricky, but the result is great and work the effort to debug.

## Requirements

I will assume that the simulation is running in Jupyter Lab and that `ipympl` has been installed, so that matplotlib output is displayed in an interactive widget. That is, you are successfully above to use `%matplotlib widget` in the notebook.
