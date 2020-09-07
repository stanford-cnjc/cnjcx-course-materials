# CNJCx: Practical Python
## Git, GitHub, Clean Code, and Open Science
### Week 4 Recap

**Session Leaders**: Russ Poldrack, Tucker Fisher, and Eshed Margalit

In this session, we introduce the tools `git` and Github, discuss clean code best
practices, and preview selected topics in open science.

## Table of Contents
1. [Prerequisites](#prerequisites)
1. [Content Taught Live](#content-taught-live)
1. [Bonus Content](#bonus-content)
1. [Preparation for Next Session: Clean Code](#week4-prep)
1. [FAQ](#faq)

## Prerequisites<a name="prerequisites"></a>
Before you begin these instructions, you should go through the prerequisite
instructions for each of the previous weeks.

1. [Week 1: Setting up a bash shell on your machine][week1_prereq_link]
2. [Week 2: Installing `tmux` and `vim`][week2_prereq_link]
3. [Week 3: Python 3.8 Installation Instructions][week3_prereq_link]


## Content Taught Live<a name="content-taught-live"></a>
Open your bash terminal to follow along with the commands. Remember, for all the
commands below don't type the leading `$`. That is there to represent your prompt.

### Code-along Part 1: `git` started!

Lets set ourselves up for today's exercise and learn a few tricks along the way.

Like other languages `bash` (and `zsh`) have variables. We get access to these 
variables using the `$`. 

Using our old friend `echo` which Josh introduced us to last week we can see what
lives inside these variables.
```zsh
$ echo $HOME 
```

Now lets head `$HOME`
```zsh
$ cd $HOME
```

Time to make our new folder where we will work with git. I store all of my
repositories together in a directory called `local_repos/`

we will use `mkdir` like we did last week, but I'm going to add the `-p` flag
so that `mkdir` knows that it can go ahead and build the entire path at once.

```zsh
$ mkdir -p $HOME/cnjcx/week_4/local_repos/git_tutorial && cd $_
```

Notice that `$_` takes on the value of the last argument of the last command. So in
this case, `$_` will resolve to the path of the newly-made directory. Let's list (with
the `-a` flag to show hidden directories too)

```zsh
$ ls -a
```

So far, empty directory. Let's create a git repository and see what changes.

```zsh
$ git init
Initialized empty Git repository in ...
```

```zsh
$ ls -a
```

You should now see a `.git` directory in there too! Keep in mind you wouldn't see this
directory if you didn't add the `-a` flag to `ls`, it is hidden by default.

`git status` is an extremely useful command that reports the current state of your
git repository. If we run it now, we'll see that we haven't made any commits yet:
```zsh
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Alright, let's create a file in this repository with `touch`, then use `echo` to push
some text into that file.

```zsh
$ touch README.md
$ echo "## This Directory Holds CNJCx Sandbox Repo" >| README.md
```

The command line connoisseur will see these two steps as awkward neophyte
verbosity. We just wanted to show you how to force through `noclobber`.

When we run a `git status`, we'll see helpful output indicating that a new file was
added.

```zsh
$ git status
On branch master

No commits yet

Untracked files:
    (use "git add <file>..." to include in what will be commited)

        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

### Committing to changes

The output of `git status` suggested we use `git add` to include our newly-created
file in the next commit.

```zsh
$ git add README.md
$ git status

On branch master

No commits yet

Changes to be committed:
    (use "git rm --chached <file>..." to unstage)

        new file:   README.md
```

We've now added `README.md` to the next commit, but haven't locked in those changes.
To do so, we need to run `git commit`. The `-m <message>` allows you to add a commit
message to the commit. We'll see what happens if you neglect to include it a bit later.

```zsh
$ git commit -m "init with readme"
[master (root-commit) #####] init with readme
 1 file changed, 1 insertion(+)
 create mode ##### README.md
```

Great, we've just made our first commit!
Let's continue onward and make more changes to our codebase. The next two lines will
append new output to the bottom of `README.md`, then create a new file called
`untracked.txt` with the contents "random words".

```zsh
$ echo "1. Totes tracks ur work" >> README.md
$ echo "random words" > untracked.txt
```

Running `git status` now will notify us both of the modification and of the new file.

```zsh
$ git status
On branch master
Changes not stgged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md

Untracked files:
    (use "git add <file>..." to include in what will be committed)
        
        untracked.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

To add only files that have been previously committed, we can use a shortcut, the `-u`
flag:

```zsh
$ git add -u
$ git status
On branch master
Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
        modified:   README.md

Untracked files:
    (use "git add <file>..." to include in what will be committed)
        
        untracked.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Let's go ahead and make our second and third commits:

```zsh
$ git commit -m "adds info about init command"
$ echo "2. A commit list can help organize your coding plan" >> README.md
$ git status
$ git add -u
$ git commit -m "adds info about status command"
```

### Log and Explore

One of the strengths of `git` is the easy to navigate revision history. To see a list
of previous commits, you can run the `git log` command:
```zsh
$ git log --decorate --graph
```

The flags `--decorate` and `--graph` will make the output a bit more informative and
easy on the eyes.

You'll notice a few things about this output:
1. Each commit is listed in chronological order. Commits are tagged with a specific
hash, which serves as a unique identifiers (commit messages can be repeated, but hashes
cannot). An example commit hash might look like `bd94866794ee1976bf7b374f5e0fd3523d26cdea`
2. Commits are shown with four additional pieces of information
    1. The name of the commit author
    2. The email address of the commit author
    3. The date and time of the commit
    4. The commit message
3. You may see additional marks next to some commits. In particular, you'll find 
"HEAD" and "master" next to your most recent commit.

HEAD refers to the currently checked-out commit. `master` is the name of a _branch_.
We'll look at branches in more detail in a minute, but for now, keep in mind that
`master` is really just pointing at a specific commit!

Alright, given this log, how do we navigate through it? To roll back to one commit
before our current HEAD, we use `git checkout HEAD~1`. If you look at the contents of
README.md, you'll see it was rolled back in time to before the last addition!

```zsh
$ git checkout HEAD~1
$ cat README.md
$ git log --all
```

After running that list `git log --all`, you should see that HEAD and `master` are now
in different places. To return to the most recent commit, we can just `git checkout` 
the master branch.

```zsh
$ git checkout master
```

### Branching Out

The `git branch` command gives you a list of all existing branches, and puts a star
(\*) next to the currently checked out branch.
```zsh
$ git branch
* master
```

To create (and immediately checkout) a new branch, we use the `git checkout -b` command:
```zsh
$ git checkout -b formalize
$ git branch
* formalize
  master
```

Now that we're on a new branch, let's make more edits to our README.md. We used `vim`
during the session, but you should feel free to use the text editor of your choice!

```zsh
$ vim README.md
## This Directory Holds CNJCx Sandbox Repo
1. Keep track of your changes.
2. A commit list can help organize your coding plan.
```

Now let's `add` and `commit` these changes.

```zsh
$ git add -u
$ git commit -m "more formal language"
$ git log --decorate --graph --all
```

The git log now shows that `formalize` has moved ahead of `master`. Imagine you need to
go back to master for a minute. No problem, just use `git checkout`!

```zsh
$ git checkout master
$ cat README.md
```

What happens if we make edits to the README.md file on the master branch now?

```zsh
$ vim README.md
## This Directory Holds CNJCx Sandbox Repo
1. Keep track of your changes.
2. A commit list can help organize your coding plan.

## Github is great too
1. You can share code with your friends
2. The code is backed up once its on Github
```

```zsh
$ git add -u && git commit -m "adds info about github"
$ git log --all --decorate --graph
```

The git log now shows how `formalize` and `master` have diverged! `git` can easily
keep track of these different parallel universes for our codebase. To merge them
together, we use the `git merge` command. Because we currently have `master` checked 
out, we will merge `formalize` _into_ master. Let's do that and look at how
README.md ended up:

```zsh
$ git merge formalize
$ cat README.md
```

The git log will also now reflect the merge. If you add `--graph`, you'll see the two
paths diverge and merge back together.

```zsh
$ git log --all --graph
```

## Bonus Material<a name="bonus-content"></a>

### Git Github

For this session, we've prepared a repository, uploaded to Github, that you can `clone`
to your machine.

```zsh
$ cd $HOME/cnjcx/week_4/local_repos
$ git clone https://github.com/stanford-cnjc/cnjcx_project.git
$ cd cnjcx_project.git
```

This repository is actually a Python package that we can install with `pip`! If you 
haven't already made a virtual environment to install packages into, go back to the
[code-along for Week 3][week3_codealong].

```zsh
$ source ~/cnjcx_env/bin/activate
(cnjcx_env) $ pip install .
```

### How do hand-written Python packages work?
This repository has a `setup.py` file, which is required for `pip` installation to work.
The setup.py file points to the `convertime/` directory to be installed as a package.
The contents of `convertime/` are then available to be imported in any script!

We encourage you to poke around and see how this directory is structured. We added
some basic modules, an example script, and example binary (in the `bin/` folder) that
gets installed as a command-line program when you `pip install` the package. There's also
an intentional bug in the code, see if you can find it and fix it! The unit tests will
fail if the bug isn't fixed.

Some commands you can try with this package:
1. `$ seconds_until_2021` (to run the installed binary)
2. `$ python scripts/time_until_2021.py --units weeks` (to try the Python script) 
3. `$ python -m unittest discover tests` (to run the unit tests)

---- 

[week1_prereq_link]:  https://stanford-cnjc.github.io/#/CNJCx
[week2_prereq_link]: https://github.com/stanford-cnjc/cnjcx-course-materials/blob/master/week1_commandline/cnjcx_week1_recap.md#nextsesh 
[week3_prereq_link]: https://github.com/stanford-cnjc/cnjcx-course-materials/blob/master/week2_tmux_vim/cnjcx_week2_recap.md#preparation-for-next-session-python-part-i
[week3_codealong]: https://github.com/stanford-cnjc/cnjcx-course-materials/blob/master/week3_python/cnjcx_week3_recap.md#content-taught-live
