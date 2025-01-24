{:menu DE}
{::comment}menu-start{:/comment}

- The site mirrors the structure on GitHub.io; markdown files in the `docs` folder are rendered into HTML and placed locally [on the local host](http://localhost/p064/).
- The fish function `kram.fish` handles automatic rerendering and refreshing the page in Safari:

~~~~ shell
function kram
    find ~/GitHub -name '*.md' | entr /Users/saeta/bin/kd /_
end
~~~~

It watches existing markdown files in the tree rooted at `/Users/saeta/GitHub/` using `entr`, a utility installed with Homebrew, and runs the Python program `kd` when a file has changed. If you add a markdown file to the `docs` directory, you need to restart `kram`. Details on the `kd` program appear below.

## Structure of a markdown file

A new markdown file should start with a line such as:

{:menu FO}

where **FO** indicates the submenu to be included at the top of the page. These are defined in **assets/menus** and have a structure illustrated in the following listing

~~~~ markdown
+	LA-LinearAlgebra.md	Linear Algebra
+	LA-SquareMatrices.md	Square Matrices
+	LA-GaussJordan.md	Gauss-Jordan Elimination
+	LA-HilbertSpace.md	Hilbert Space
+	LA-Diagonalization.md	Diagonalization
+	LA-Eigenvectors.md	Eigenvalues and Eigenvectors of Square Matrices
+	LA-NumericalLinearAlgebra.md	Numerical Linear Algebra with NumPy
+	LA-Krylov.md	Krylov Sets
-	LA-RotationMatrices.md	Rotation Matrices
+	LA-NumericalLinearAlgebra.md	Numerical Linear Algebra with NumPy
~~~~

Items to be included start with a + <tab> filename.md <tab> Title to appear in menu

Code for the submenu will be inserted by `kd` in a comment immediately after the `{:menu xx}` command.

    

# Projects

* toc
{:toc}

## Purpose


Kramdown idiosyncracies of concern.
+ In LaTeX blocks, \\[, \\], and \\\ need an extra preceding
backslash.
+ \\\ at the end of a line ends a paragraph, even in math mode;
to avoid this problem, add a space after \\\ 
+ Single $$ need to be converted to $$, unless they appear in a code
block, defined as lines that start with at least four spaces.

On processing a source .md file, if any of these issues need to be
corrected, the source file is suitably updated before conversion.

PNS addition:
{:menu name} will get converted into html to render the
named menu. Entries are found in assets/menus/name.txt
