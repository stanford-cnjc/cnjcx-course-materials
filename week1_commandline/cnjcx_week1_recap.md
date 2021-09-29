# CNJCx: Practical Python

## Command Line Basics (Week 1)

### Week 1 Recap

**Session Leaders**: Josh Melander, Eshed Margalit, and Tucker Fisher 

Session Recording at [**CNJCx webpage**](https://stanford-cnjc.github.io/#/CNJCx) under the Week 1 session materials.

## Table of Contents

1. [Prerequisites](#bash-setup)
1. [Content Taught Live](#livecontent)
1. [Bonus Material](#bonus)
1. [Preparation for Next Session](#nextsesh)
1. [FAQ](#faq)

## Prerequisites<a name="bash-setup"></a>

Before following-along with the commands in this session, you need to be able to
open a Bash terminal on your machine.

Prior to the first session, you should be able to open a terminal with the
instructions below. Feel free to type `echo $SHELL` at the command prompt and
hit enter to see the shell you’re using. It should say either `/bin/bash` (if
you’re using Bash) or `/bin/zsh` (if you’re using Zsh). Both will work for
CNJCx: Practical Python.

### For MacOS users

1. We recommend you [download iTerm2][iterm2link] prior to the first session,
   it’s a superior alternative to the built-in Terminal app on MacOS.
2. To open a terminal, open Spotlight Search (with ⌘ + Space or by clicking the
   magnifying glass icon in your top bar) and search "iTerm" (or "Terminal" if
   you’d prefer to use the default application)

### [For Ubuntu users][ubuntutermlink]

1. Ctrl + Alt + t
2. Alternatively, search “terminal” in the Dash

### For Windows users

We recommend enabling the Windows Subsystem for Linux (WSL). This is a little
more complicated than the previous instructions, so please reach out to us if
you get stuck!

1. Right Click the Start Menu
2. Click “Settings”
3. Search “Turn Windows features on and off”
4. Click the checkbox for “Windows Subsytem for Linux”
5. [Download “Ubuntu 18.04” from the Windows Store][wsldownloadlink]
6. Click the Ubuntu Icon to launch a Bash terminal
7. The first time you log in, you may be prompted for a username and password.
   These will be your credentials for the Ubuntu subsystem on your machine,
   i.e., [username] will determine the path to your home directory
   (/home/[username]) and the password you’ll use to perform actions as root
   (more about that in Week 1).

## Content Taught Live<a name="livecontent"></a>

Open a bash terminal and follow the commands (do not type the leading `$`) to go
through the session at your own pace!

#### Section 1: Navigating the Home Directory

First, we'll use `pwd` to see what the current working directory is. If you're
on macOS, you may see something like `/Users/eshed`. If you're on Ubuntu, you
may see something like `/home/eshed`.

```bash
$ pwd
```

Now let's list the contents of the current working directory. If you're using
the Windows Subsystem for Linux, you may not see anything while running this
command. That's okay, it just means there are no files or directories here yet.
If you're on macOS, you may see files and directories like `Desktop` and
`Downloads`. These are the same exact directories you can access with Finder!

```bash
$ ls
```

`..` is the relative path for the directory immediately above the current
working directory, sometimes called the "parent" directory. Let's change
directory to the parent directory and run `ls` again.

```bash
$ cd ..
$ ls
```

You should see your home directory listed here.

Let's "reset" by returning to our home directory. `~` is a shortcut to the
absolute path of your home directory.

```bash
$ cd ~
$ pwd
```

#### Section 2: Creating Files and Directories

Create a new directory called "cnjcx" in the current working directory, then use
`ls` to show the newly-created directory.

```bash
$ mkdir cnjcx
$ ls -lrt
```

Change working directory to "cnjcx" by providing the relative path, then run
`pwd` to see where in the filesystem you are.

```bash
$ cd cnjcx
$ pwd
```

Use `touch` to create an empty file in the current directory named "notes.txt".
Then use `ls` to see the newly created file.

```bash
$ touch notes.txt
$ ls
```

Let's reset: return to your home directory (`~`) and `clear` the console output.

```bash
$ cd ~
$ clear
```

#### Section 3: Using Streams to Modify File Contents

First, let's print a message to the terminal using the `echo` command.

```bash
$ echo "Hello World"
```

`echo` prints by default to the standard output (the terminal), but the output
can be redirected to a file using the `>` and `>>` operators.

The `>>` operator appends text to the bottom of a file. We'll use it to write
"Hello World" to the bottom of our `cnjcx/notes.txt`. Use `cat` to print the
contents of the file to confirm that "Hello World" was successfully added to the
bottom of the file.

```bash
$ echo "Hello World" >> cnjcx/notes.txt
$ cat cnjcx/notes.txt
```

The `>` operator doesn't append messages, but overwrites the contents of the
file (or creates a file if one doesn't exist already). To practice, let's first
overwrite the contents of the notes file with the string "Absolute Path to ~: ",
then append the output of `pwd` to the bottom of the file. Use `cat` to verify
that the file contains what you expect. Finally, let's `cd` into the "cnjcx"
directory and append a bunch of dashes ("------") to the bottom of the file.

**If you run into problems because the file already exists**: try using `>|`
instead of `>` to force the overwrite.

```bash
$ echo "Absolute Path to ~: " > cnjcx/notes.txt
$ pwd >> cnjcx/notes.txt
$ cd cnjcx
$ echo "---------" >> notes.txt
$ cat notes.txt
```

Notice that in this previous block, relative paths changed halfway through. When
we were in the home directory, we specified notes with `cnjcx/notes.txt`. When
we were in the `cnjcx` directory, we specified notes with `notes.txt`.

#### Section 4: Finding and appending storage info

This section is mostly practice of the commands we used in the previous block,
but with a new command, `df`, that prints a summary of the [d]isk [f]ilesystem.

Append the string "Storage Info: " to the bottom of notes.txt, then append the
output of `df -h` to the bottom of the file.

```bash
$ df -h
$ echo "Storage Info: " >> notes.txt
$ df -h >> notes.txt
$ cat notes.txt
```

#### Section 5: Copying and moving files

Let's reset to our home directories.

```bash
$ cd ~
$ clear
```

Enter the cnjcx directory and list its contents.

```bash
$ cd cnjcx
$ pwd
$ ls
```

Let's use `mkdir` to create a new directory called "week_1". Use `ls` to see the
newly-created directory. Finally use `mv` to move notes.txt into the
newly-created `week_1` directory. To verify that the move worked, `ls` the
contents of the current working directory and `ls week_1` to list the contents
of `week_1`

```bash
$ mkdir week_1
$ ls
$ mv notes.txt week_1/
$ ls
$ ls week_1
```

Use `cp -r` to create a duplicate of the entire `week_1` directory named
`week_2`.The `-r` flag is always needed when copying directories. Overwrite the
contents of `week_2/notes.txt` with the string "Week 2 notes below: " using the
`echo` command. Finally, use `cat` to print the contents of `week_2/notes.txt`
using its *absolute* path.

```bash
$ cp -r week_1/ week_2/
$ echo "Week 2 notes below: " > week_2/notes.txt
$ ls
$ cat ~/cnjcx/week_2/notes.txt

```

#### Section 6: How to find and search files

First, let's reset again.

```bash
$ cd ~
$ clear
```

Use `find` to search for files named "notes.txt" in the `cnjcx/` directory.
Then, try using the search pattern "\*.txt" to find all files with the .txt
extension.

```console
$ find cnjcx/ -name 'notes.txt'
$ find cnjcx/ -name '*.txt'
```

Use `grep -R` to search each file in `cnjcx/` for the pattern "Storage Info".
Repeat the command with `--context=1` to print a line above and below each match
to provide "context".

```console
$ grep -R "Storage Info" cnjcx
$ grep -R --context=1 "Storage Info" cnjcx # give 1 line above and below
```

### Bonus Materials<a name="bonus"></a>

We ran out of time and weren't able to go over shell scripting and configuration
files. They are written out here so you can go through it on your own!

#### Section 7: Scripting

The ability to write scripts is extremely powerful, as you can automate tasks
that would be difficult or cumbersome to do by hand. We'll walk you through
downloading a shell script written by Eshed, then we'll go line by line and
explain what's happening.

**What will this script do?** The script creates 4 new directories: "week_3",
"week_4", "week_5", "week_6". In each of those directories, a notes.txt file
will be made with the contents "Notes for week X below: ", where X will be
replaced with the appropriate number.

First, we need to download the file using `curl`. The `-L` flag in the command
is needed to follow HTTP redirects -- don't worry about that. The `-o` flag
indicates the filename that the downloaded contents should be saved to. Run the
`curl` command then `ls` to see the newly-created file.

```bash
$ cd ~/cnjcx
$ curl -L -o create_week_notes.sh https://git.io/JJQJa
$ ls
```

This file is not "executable", meaning that the shell can't run the script as a
program yet (which is a good security precaution for things downloaded off the
internet!). We'll use the `chmod` command to change the permissions of the file
and make it executable. Now you can run the script with
`./create_week_notes.sh`! The leading "./" is non-negotiable -- if you don't
include it you won't be able to execute the file.

```bash
$ chmod u+x create_week_notes.sh # give the logged-in [u]ser permission to e[x]ecute the file
$ ./create_week_notes.sh
```

Let's see if it worked!

```bash
$ ls
$ cat week_3/notes.txt
```

Alright, let's go line-by-line through this file and understand how it works.
Use `cat -n` to print the file with line numbers next to each line. This
explanation assumes some familiarity with control flow (like for loops). If you
don't have that background, no problem! The important point is that you
understand that this script allows us to flexibly create many new directories
and files in a fraction of a second.

```bash
$ cat -n create_week_notes.sh
```

**Line-by-line explanation of script**

1. `#!/bin/bash`: the first line of a shell script always points to the program
   that should be used to run this script. In this case, it's `/bin/bash` (what
   you would see if you typed `echo $SHELL` from a Bash terminal. This also
   ensures that if you're on a different shell, bash will still be used to run
   the script.
2. Blank (for readability)
3. Lines starting with "#" are comments and are ignored by `/bin/bash`
4. `for week_number in $(seq 3 6); do` This line starts a for loop and defines
   what the value of "week_number" will be in each iteration of the loop. In
   this case, `$(seq 3 6)` \$() means "evaluate the expression inside the
   parentheses", and `seq 3 6` returns the numbers 3, 4, 5, 6, each on a new
   line
5. Comment
6. Print the string in double-quotes to the standard output (stdout). Note that
   the value of `week_number`, which will change on each iteration of the loop,
   is embedded in the string and wrapped in \${}. This tells bash that the value
   is a variable and not a literal string.
7. Blank (for readability)
8. Comment
9. Store the string created by adding `${week_number}` to `"week_"` in a new
   variable called `week_directory`
10. Blank
11. Comment
12. Create a new directory, whose name is whatever `$week_directory` evaluates
    to on this iteration of the loop
13. Insert the string in double-quotes (again, with a variable embedded) into
    the specified file (which is also variable based on the value of
    `week_directory` in this iteration of the loop)
14. `done` closes the loop

#### Section 8: Modifying your shell configuration file

Customizing your shell is one of the most satisfying parts of building an
efficient and personalized workflow. Configuration settings are read from
specific files in your home directory each time you log in or create a new
shell. To figure out what your configuration file is called, run `echo $SHELL`.
You should see either `/bin/bash` or `/bin/zsh`. If your shell is `/bin/zsh`,
your configuration file is called `.zshrc`. If your shell is `/bin/bash`, check
this table -- the answer depends on your operating system.

| Your Operating System | Configuration file |
| --------------------- | ------------------ |
| macOS                 | .bash_profile      |
| Ubuntu                | .bashrc            |

In these instructions we'll assume your configuration file is `.bashrc`. Replace
with `.zshrc` or `.bash_profile` if you have a different configuration file.

```bash
$ echo $SHELL
$ cd ~
$ ls -a
```

For safety, copy your configuration file to a backup file. The `.bak` file
extension doesn't change the file in any way, it's just a convention for naming
backup files. Next, append a new `alias` to your configuration script. Aliases
are shortcuts that allow you to define custom commands. In this example, we'll
create a command `lrt` which will translate to `ls -lrt` behind the scenes.

```bash
$ cp .bashrc .bashrc.bak
$ echo "alias lrt='ls -lrt'" >> .bashrc
```

Restart your terminal by running `exec $SHELL` or closing the terminal window
and opening a new one. Try out the new command!

```bash
$ exec $SHELL
$ lrt
```

Optionally, revert your changes by moving the backup configuration file to
overwrite the modified configuration file we made. Restart your terminal to have
the changes take effect.

```bash
$ mv .bashrc.bak .bashrc
$ exec $SHELL
$ lrt
```

## Preparation for Next Session<a name="nextsesh"></a>

In next week's session we will share some of the tools that we believe can make
you a more powerful python developer. <a name="returnfootnote1"></a> You will
learn how to effectively multitask within the terminal, find a text editor that
suits your needs (with special attention to our favorite), and if there is time,
we will show you how to connect to a remote machine[<sup>1</sup>](#footnote1)!

**In order to get the most out of our next session there are two things you can
take care of before we meet:** (1) get a few pieces of software, and (2)
download a couple files we wrote for you.

### 1. Software

1. Open terminal
1. Check if you have **`tmux`**:

   ```bash
   $ which tmux # note: the which command locates a program
   ```

   - if you see `tmux not found` or nothing, keep that in mind. We will show you
     how to download tmux in step 5 once we have checked one more thing.
   - if you see a path, then you already have it! You may see
     `/usr/local/bin/tmux` or `/usr/bin/tmux`.

1. Check if you have **`vim`**:

   ```bash
   $ which vim # same story here check for program location
   ```

   - if you see `vim not found` or nothing, keep that in mind. We will show you
     how to download it in step 6.
   - if you see a path, then you already have it! You may see
     `/user/local/bin/vim` or `/usr/bin/vim`.

1. Introducing you to your package manager:

   Package managers help a developer download command line programs that did not
   come pre-installed on their machine. Getting and managing packages will be
   _critical for python devlopment_.

   **For MacOS**

   Homebrew is the best way (we know of) to get and manage packages on a Mac. If
   you would like to learn more you can read about it directly from
   [Homebrew][hblink]. Once you have Homebrew you will have access to the
   **`brew`** command (used in step 5 and 6).

   **Before we meet next week** you should download Homebrew. Downloading
   Homebrew is simple. Run the following in your terminal. _Remember: If you are
   copy-pasting, the leading `$` is there to orient you, don't type that :)_

   ```bash
   $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
   ```


    **For Unix and Windows Subsystem for Linux**

    You already have a great package manager onboard called **`apt-get`**. **`apt-get`** is
    the classic package manager for derivatives of Debian, like Ubuntu.

    Double check you have **`apt-get`** with `$ which apt-get`. If you don't have
    it, please email us.

5. Download **`tmux`** (if you don't already have it)

   **For MacOS**

   _note: the brew command comes from step 4_

   ```bash
   $ brew install tmux
   ```

   **For Unix and Windows Subsystem for Linux**

   ```bash
   $ sudo apt-get install tmux
   ```

6. Download **`vim`** (if you don't already have it)

   Next, lets get vim if you need it.

   **For MacOS**

   _note: the brew command comes from step 4_

   ```bash
   $ brew install vim
   ```

   **For Unix and Windows Subsystem for Linux**

   ```bash
   $ sudo apt-get install vim
   ```
7. Download **`git`** (if you don't already have it)

   Finally, lets get git!
   
   **For MacOS**
   
   _note: the brew command comes from step 4_
   
   ```bash
   $ brew install git
   ```
   
   **For Unix and Windows Subsystem for Linux**
   
   ```bash
   $ sudo apt-get install git-all
   ```

### 2. Files from Josh-Eshed-Tucker (JET)

**`tmux`** and **`vim`** sometimes get a bad rap. We think this partly due to
the unfriendly default settings. The files you download below will give us a
chance to start out on the right foot.

The **`curl`** command you learned about in [Bonus Material](#bonus) is perfect
for our purposes here.

```bash
$ cd ~/cncjx
$ curl -L -o basic_vimrc https://git.io/JJdvq
$ curl -L -o basic_tmux.conf https://git.io/JJdei
```

No need to do anything with these files yet. We will work with them next week.

## FAQ<a name="faq"></a>

Here are answers to some common questions we got in the Week 1 session:

### Does the order of flags passed to a command matter?

No, `ls -lrt`, `ls -tlr`, and `ls -l -r -t` are all equivalent!

### I'm a Windows Subsytem for Linux (WSL) user, and I don't see anything in my home directory. Is that okay?

Yes, you probably just don't have any non-hidden files in your home directory
yet. Try `ls -a` (`-a` will show hidden files as well) and you should see
output.

### When do I need to use `echo`?

Many commands output text to the standard output (the terminal window) by
default. For example, `pwd` print the absolute path of the current working
directory to the terminal. If you want to print a message yourself, however, you
can use `echo "my message"` to print the message, or
`echo "my message" > my_file.txt` to redirect the printing of the message to a
file instead of the terminal window.

---

[<sup>1</sup>](#returnfootnote1)<a name="footnote1"></a> Remote machines,
machines that you _connect to_ rather than _sit at_, are becoming more common as
demands for computing and storage resources grow. These machines are often
dedicated "compute machines" specialized for the heavy computational loads that
arise when performing advanced analysis or working with large datasets. While
these machines are much more powerful than a laptop, they often lack graphical
user interfaces (GUIs). Without a GUI, users must interact over the command line
to take advantage of the remote compute power. One example is the [Sherlock
cluster][sherlocklink] which allows users to run computationally expensive
processes, including training deep neural networks.


[sherlocklink]: https://www.sherlock.stanford.edu/docs/overview/introduction/
[cnjcxlink]: https://stanford-cnjc.github.io/#/CNJCx
[hblink]: https://brew.sh/
[iterm2link]: https://www.iterm2.com/downloads.html
[ubuntutermlink]: https://www.wikihow.com/Open-a-Terminal-Window-in-Ubuntu
[wsldownloadlink]:
  https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6?activetab=pivot%3aoverviewtab
