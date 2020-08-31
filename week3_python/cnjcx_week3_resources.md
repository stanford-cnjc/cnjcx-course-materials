# CNJCx: Practical Python
## Python Part I (Week 3)
### Reference Material

**Session Leaders**: Eshed Margalit and Julia Wang

## Table of Contents
1. [Resources and Tips](#rnt)
1. [Understanding your Python Installation](#installations)
1. [Starting Fresh](#starting-fresh)

## Resources and Tips<a name="rnt"></a>

### Tools
- [pyenv](https://github.com/pyenv/pyenv) to manage Python installations, versions, and virtual environments
- [pipx](https://github.com/pipxproject/pipx) allows you to install single python packages into their own virtual environment, isolating them from the system package directory and making them available at the command line (if they can be run that way)
- [PyCharm](https://www.jetbrains.com/pycharm/) is a Python-specific IDE (integrated development environment) that is popular among those looking for a full-featured development ecosystem.
- [Jupyter Notebook and JupyterLab](https://jupyter.org/) are popular tools to combine Python code with figures, markdown, and interactive components.

### Formatting and Linting
- [black](https://black.readthedocs.io/en/stable/) is a Python code formatter that enforces a strict style whether PEP8 guidelines were violated or not
- [YAPF](https://github.com/google/yapf) is "yet another python formatter" that, like `black`, enforces a style guide whether PEP8 guidelines were violated or not. However, YAPF provides more configuration options than `black`
- [autopep8](https://pypi.org/project/autopep8/) is a Python code formatter that formats code minimally so that it conforms to the PEP8 style guide. Unlike the previous two options, `autopep8` does not guarantee that code will be "uniform" since it only does the minimum required.
- [flake8](https://flake8.pycqa.org/en/latest/) is a popular linter that checks for style best practices. Code formatter with `black`, `yapf`, or `autopep8` will usually, but no always, resolve any warnings raised by `flake8`

### Tutorials
- [NeuroHackademy 2020](https://neurohackademy.org/neurohack_year/2020/) was a course taught in July 2020 with excellent tutorials on version control, Python, machine learning, and neuroimaging.
    - In particular, we recommend their [Intro to Python](https://github.com/neurohackademy/nh2020-curriculum/blob/master/mo-python/02-introduction-to-python.ipynb) and their [Numpy Basics](https://github.com/neurohackademy/nh2020-curriculum/blob/master/tu-numpy-yarkoni/01-numpy-basics.ipynb)
    - See all of their content on [their GitHub](https://github.com/neurohackademy/nh2020-curriculum)
- [The CS231n Numpy Tutorial](https://cs231n.github.io/python-numpy-tutorial/)

## Understanding your Python Installation<a name="installations"></a>
Before we dive in, let's clarify what it means to "install Python". The Python interpreter is a program installed
somewhere on your computer. Different methods of installation will put the program in different directories. For
example, on a MacBook with Python 3.8 installed with Homebrew, the interpreter can be found at `/usr/local/Cellar/python@3.8/3.8.5/Frameworks/Python.framework/Versions/3.8/bin/python3`. **However**, Homebrew (and many other tools) employ two tricks to make the interpreter easier to use.

First, they employ "soft links". Think of soft links as portals on your filesystem that allow you to reroute one path on your filesystem to a different path. For example, on that same MacBook, `usr/local/opt/python3/bin/python3` is a soft link to the more complicated path I copied above. You'll also find soft links in `/usr/local`, `/usr/local/bin`, etc. This doesn't mean there are many different Python programs installed, just that Homebrew (the tool we used for installation) created a web of soft links. The important thing to keep in mind is that **all these softlinks** resolve to the exact same place. 

To make matters more complicated, sometimes the softlinks will be named like `python3.8`, `python`, `python@3.8`, and moe.

Now, different installation methods _will_ create different Python interpreters, each with a possible set of softlinks pointing to them. However, those interpreters may have the exact same name as those installed by a different installer. So when you type `$ python3` at the command line, how does your shell know which interpreter to give you? 
To understand the answer to that question, we need to talk a bit about `PATH`. On UNIX machines (macOS and Ubuntu included), `echo $PATH` will print a list of directories on the "path", each separated by a colon (":"). When you type the name of a command, the following happens (in order);

1. If the command is aliased, the command is replaced by the value of the alias.
2. If the command is an absolute path to a program on your filesystem, that program is executed.
3. If the command is not an absolute path to a program, the shell will search each directory in the `PATH`, in order, until a match is found. If no match is found, you'll just get an error.

So in short, unless you create an `alias` for `python3`, the interpreter you get when you type `$ python3` will depend on the order of directories in your `PATH`. This is why many Python installers ask if they can modify your `PATH` variable!
However, because providing the absolute path to a program short-circuits the need to search the `PATH`, the setup instructions for this session had you create an alias for `python3` that resolves to the absolute path to a Python interpreter, e.g., `alias python3='/usr/local/bin/python3.8`.

## Starting Fresh<a name="starting-fresh"></a>
So you want to start over with a fresh Python 3 installation and virtual environments? This guide should work:

#### Step 1: Remove any aliases to `python` or `python3`
1. Check if you have any relevant aliases with `$ alias | grep python`
2. If you have any aliases, you need to figure out where they're defined. A good bet is `~/.bashrc` on Ubuntu and `~/.bash_profile` on macOS. However, if those shell configuration files `source` a different file, the aliases may be defined there too. Try checking `~/.aliases` if you don't find the alias definition in `~/.bashrc` or `~/.bash_profile`
3. Delete the lines of the shell configuration file that set the Python aliases.
4. As a final check, make sure you don't have any aliases defined for `pip` or `pip3`.

#### Step 2: Remove any `PATH` manipulation commands that were added by Python installers.
1. Once again, check your shell configuration file. You may see lines like `export PATH=$HOME/anaconda/bin:$PATH` -- these put certain directories at the front of `PATH` variable to influence the order in which your shell will check for a command.
2. Delete the line modifying your `PATH` variable if and only if you are confident it was added by a Python installer. If you're not sure, don't delete it.

#### Step 3: Install a fresh version of Python
1. Option A: Install the latest Python 3 using Homebrew or APT
    1. Follow [our instructions here][pythoninstalllink]

2. Option B: Install [`pyenv`][pyenvlink], a sophisticated and powerful Python version manager.
    1. `curl https://pyenv.run | bash`
    2. `exec $SHELL`
    3. Read the documentation for basic commands. In short, use `pyenv install 3.8.5` to install Python 3.8.5, then `pyenv global 3.8.5` to make that the default version used.
    4. Optionally, look into [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) for virtual environment management

3. Option C: Install Python with Anaconda (not recommended for CNJCx). You can find the [conda installation instructions][condalink] here.
    

#### Step 4: Create a virtual environment for your project
1. Run `$ python3 -m venv <path to venv>` to create a new virtual environment at `<path to venv>`. As a rule of thumb, use a different virtual environment for each distrinct project you work on.
2. To activate the virtual environment, run `$ source <path to venv>/bin/activate`. To deactivate the virtual environment, just type `$ deactivate`
While the virtual environment is active, any packages installed with pip.


-------------

[pyenvlink]: https://github.com/pyenv/pyenv
[pythoninstalllink]: https://github.com/stanford-cnjc/cnjcx-course-materials/blob/master/week2_tmux_vim/cnjcx_week2_recap.md#preparation-for-next-session-python-part-i
[condalink]: https://docs.anaconda.com/anaconda/install/
