# CNJCx: Practical Python
## Python Installations and Virtual Environments
### Week 3 Recap

In this session, we practice using Python, creating virtual environments, and installing packages
into virtual environments.

**Session Leaders**: Eshed Margalit and Julia Wang

Session Recording at [**CNJCx webpage**](https://stanford-cnjc.github.io/#/CNJCx) under the Week 3 session materials.

## Table of Contents
1. [Prerequisites](#prerequisites)
1. [Content Taught Live](#content-taught-live)
1. [Preparation for Next Session: Clean Code](#week4-prep)
1. [FAQ](#faq)

## Prerequisites<a name="prerequisites"></a>
Before you begin these instructions, you must complete the pre-requisite instructions
to install Python 3.8 on your machine!

[Link to Python 3.8 Installation Instructions][week3_prereq_link]


## Content Taught Live<a name="content-taught-live"></a>
Open your bash terminal and follow the commands. Remember, for all the commands below don't type the leading
`$`. That is there to represent your prompt.

### Code-Along Part 1: Playing with Python

In the pre-requisite instructions for this week, we had you add an alias to your shell configuration file,
so that `python3` is expanded to the absolute path to the Python interpreter you want to use. A Python
interpreter is the program that runs Python code. Interpreters can be downloaded and installed from many
sources, which is a common point of confusion!

First, let's check the version of Python we're using. Both of these commands are equivalent. 
```bash
$ python3 --version 
$ python3 -V
```

There are two ways to use the Python interpreter: as an interactive program, or by running scripts.

#### The REPL
When we use Python interactively, we enter the "REPL": the [R]ead [E]valuate [P]rint [L]oop.
You can type Python statements in the REPL prompt and the interpreter will return the output.
When you quit the REPL, all of your variables will be lost -- this is mostly a useful tool
for quickly checking a feature or doing a quick calculation and is not suitable for work that
needs to be saved.

To start the REPL, just start the interpreter:
```bash
$ python3 
```

You should see something like this:
```bash
Python 3.8.5 (default, Jul 21 2020, 10:42:08)
[Clang 11.0.0 (clang-1100.0.33.17)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
The `>>>` is your Python prompt.

Play with the REPL by asking it to evaluate Python statements:
```bash
>>> 2 + 3
5
>>> print("Hello CNJCx!")
Hello CNJCx!
```

#### Writing Python scripts
We can also use Python to run through the commands in a file.

Let's create a file with two lines of Python code, then use `cat` to examine the file's contents:
If the `mkdir` or `echo` commands aren't familiar, make sure to check out our
[Week 1][week1_link] and [Week 2][week2_link] materials.
```bash
$ mkdir -p ~/cnjcx/week_3
$ cd ~/cnjcx/week_3
$ echo "x = 5 / 2" >> hello_cnjcx.py
$ echo "print(x)" >> hello_cnjcx.py
$ cat hello_cncjx.py
```

Then, run the script with:
```bash
$ python3 hello_cnjcx.py 
```

You should see the answer "2.5". Note that if we were using a Python 2 interpreter (bad idea, Python 2 is dead), the answer would be "2" instead of "2.5". [Read more about the differences between Python 2 and Python 3][py2v3_link].

### Code-Along Part 2: Virtual Environments
Virtual environments are special directories on your machine that encapsulate a Python interpeter and associated packages that are used for a specific project or purpose.
- You can have multiple virtual environments on your machine, e.g., one for each project
- When you install a package with `pip` into a virtual environment, it is only accessible when that virtual environment is "active".
- After activating a virtual environment, `$ python` and `$ pip` will almost always use the python interpreter and pip program associated with that virtual environment (via clever manipulation of your `$PATH` variable.)

For more details, walkthrough, and example, see the [Week 3 Slides][week3_slides_link].

#### Creating and activating our virtual environment
Let's make a virtual environment called `~/cnjcx_env`.

The syntax for creating a virtual environment (if you're using Python 3.3 or higher) is:
```bash
$ <path to Python interpreter> -m venv <path to virtual environment>
```

If you followed, the setup instructions for this week, you can run:
```bash
$ python3 -m venv ~/cnjcx_env
```

This says "use `python3` to create a virtual environment at the path `~/cnjcx_env`".
Now we can activate our virtual environment and verify our Python version:
```bash
$ source ~/cnjcx_env/bin/activate 
(cnjcx_env) $ python -V
```
Notice that we no longer need `python3` and are using `python` instead! Activating the
virtual environment tells our shell that `python` means "the interpreter we used to
create the virtual environment". You might also notice your prompt change to include
"(cnjcx_env)" at the front. This is a helpful reminder that you currently have a
virtual environment active.

Next, let's use `pip` to install Numpy, a popular package for working with arrays
and matrices. After installing, we'll list the packages installed in this virtual environment.

```bash
(cnjcx_env)$ pip install numpy 
(cnjcx_env)$ pip list
```

To practice importing numpy, let's use the REPL one more time.
```bash
(cnjcx_env)$ python
Python 3.8.5 (default, Jul 21 2020, 10:42:08)
[Clang 11.0.0 (clang-1100.0.33.17)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np
>>> print(np.random.random())
0.8569153269332772
```

Notice the syntax `import numpy as np`. This means "import the package numpy, but rename it to `np` for convenience".

We can also use `pip` to install a bunch of packages at once into our virtual environment. For CNJCx,
we've provided a list of packages that will be useful later in the course. To install them,
we need to download the file (lines 1 and 2) and install the packages from the file (line 3).

```bash
(cnjcx_env)$ cd ~/cncjx/week_3
(cnjcx_env)$ curl -L -o requirements.txt https://git.io/JUk8S
(cnjcx_env)$ pip install -r requirements.txt
```

The format of `requirements.txt` is such that one package is on each line. When 
we `pip install -r <file>`, pip goes line by line and installs each package in order. To create one
of these files, you can run `pip freeze > requirements.txt` (note that this will overwrite the
requirements file in your directory if you already have one).

### Code-Along Part 3: Starting a Jupyter Notebook
One of the packages you just installed is `jupyter`, a very powerful set of tools
that allows you to write Python code alongside images, text, and more. To start
a Jupyter notebook:

```bash
(cnjcx_env)$ jupyter notebook
```

If you're on Windows Subsystem for Linux (or otherwise have issues), try:
```bash
(cnjcx_env)$ jupyter notebook --no-browser
```

This should generate a bunch of output that looks like:
```
[I 09:34:41.256 NotebookApp] Serving notebooks from local directory: /Users/eshed
[I 09:34:41.256 NotebookApp] Jupyter Notebook 6.1.3 is running at:
[I 09:34:41.256 NotebookApp] http://localhost:8888/?token=eb71e986eb0cf091e0d1399776836df73b253d166a905242
[I 09:34:41.256 NotebookApp]  or http://127.0.0.1:8888/?token=eb71e986eb0cf091e0d1399776836df73b253d166a905242
[I 09:34:41.256 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 09:34:41.262 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///Users/eshed/Library/Jupyter/runtime/nbserver-10550-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=eb71e986eb0cf091e0d1399776836df73b253d166a905242
     or http://127.0.0.1:8888/?token=eb71e986eb0cf091e0d1399776836df73b253d166a905242
```

Copy the link starting with `http://localhost` and paste it into your favorite web browser to reach the notebook landing page.
From there, click New -> Python 3 to create a new Jupyter Notebook. From here, you should be able to follow along with 
a [basic Jupyter notebook tutorial][realpython_jupyter_tutorial].

#### Review the Jupyter notebook from the session
The Jupyter notebook that Julia walked through in the second half of the session is available [here](Week%203%20Part%20II%20Code%20Along.ipynb) !

## Preparation for Next Session: Version Control and Clean Code<a name="week4-prep"></a>

### CNJCx Week 4 Prerequisites
#### Introducing yourself to **`git`**
In Week 4, we're going to cover version control and collaboration tools: `git` and GitHub.
In preparation, we ask that you perform two tasks:

1. If you don't already have one, [make a GitHub account][gh_signup_link].
2. Configure the `git` program on your computer so it knows who you are! If you're on macOS, you'll need to install xcode command line tools if you haven't already.
    1. (for macOS users only) `$ xcode-select --install`
    1. `$ git config --global user.name "John Doe"`
    2. `$ git config --global user.email johndoe@example.com`

Important: note that the name in 2.ii has double quotes around it, but the email address in 2.iii does not!
When setting your email, use the same address you made your GitHub account with -- this will prevent GitHub
from getting confused and thinking there are two versions of you making commits.


## FAQ<a name="faq"></a>

### Should I use `pip` or `conda`?   
`pip` and `conda` are tools that solve somewhat overlapping problems. The shortest description that encompasses their differences is this quote from Jake VanderPlas:

>For the user, the most salient distinction is probably this: pip installs python packages within any environment; conda installs any package within conda environments

In short, you have three options:
1. Use virtual environments and `pip` to manage your packages
2. Use `conda` exclusively
3. Try to use `conda` exclusively, but fall back on `pip` if needed

In our opinion, the necessity of that third option is what makes `conda` a poor solution for beginners. Here's a brief comparison table:
| `conda` | `pip` |
|--------|--------|
| Can install any program or package into a conda environment | Can install only Python packages, either into the default system installation or into a virtual environment |
| About 1500 packages available | About 230,000 packages available |
| Some parts closed-source | Entirely open-source |
| All-in-one tool to manage python installations, packages, environments | Specialized tool to install Python packages |
| Somewhat easier to reproduce entire computational environments than virtualenv + pip | Easy to save package list and reinstall elsewhere|



### How should I use Jupyter notebooks?

Jupyter notebooks provide an interactive and user-friendly interface to running Python code, embedding figures, and adding Markdown to documents.
We think there are two use cases where Jupyter shines:
1. Prototyping code, creating a quick plot, or testing a new feature
2. Integrating code with figures to create a self-contained document explaining a series of analyses

We do, however, encourage newcomers to Python to not become overly reliant on Jupyter notebooks.
Some critics have suggested that they encourage poor programming habits in the long run, and the nonlinear execution of code can be confusing
if the order of execution of cells is not carefully tracked. A good rule of thumb is to use notebooks to develop re-usable functions and classes
that can be turned into proper Python modules down the road.

### Which version of Python do I have?
#### The short answer:
`which python3`

#### The long answer:
Depending on your machine and your history of Python installation, any of the following programs may be accessible from your shell.
- `python`
- `python2`
- `python3`
- `python2.x`
- `python3.x`

If you followed the setup instructions for this week, then `python3` is the interpreter you want, and it points to an installation of Python 3.8. Remember that after you activate a virtual environment, you can just type `python` and it should give you the right interpreter (unless you aliased `python` to something else in your `.bashrc` or `.bash_profile`).

---- 

[week3_prereq_link]: https://github.com/stanford-cnjc/cnjcx-course-materials/blob/master/week2_tmux_vim/cnjcx_week2_recap.md#preparation-for-next-session-python-part-i
[week1_link]: https://github.com/stanford-cnjc/cnjcx-course-materials/tree/master/week1_commandline
[week2_link]: https://github.com/stanford-cnjc/cnjcx-course-materials/tree/master/week2_tmux_vim
[py2v3_link]: https://www.geeksforgeeks.org/important-differences-between-python-2-x-and-python-3-x-with-examples/
[week3_slides_link]: https://docs.google.com/presentation/d/1qVUVSAaDkvHupeIkPhr0Dzp-MwtM1wa5fpYIiSPSVAQ/edit?usp=sharing
[realpython_jupyter_tutorial]: https://realpython.com/jupyter-notebook-introduction/#creating-a-notebook
[gh_signup_link]: https://github.com/join
