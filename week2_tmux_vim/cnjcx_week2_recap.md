# CNJCx: Practical Python
## Remote Machine Basics
### Week 2 Reacap

In this session you are going to learn tools that will empower you further at
the command line. These tools will be particularly valuable if/when you work on 
machines that lack a **Graphical User Interface (GUI)**.

In today's session we are going to use a command line text editor called **`vim`**. There are 
many GUI based editors, also. [VS Code](https://code.visualstudio.com/), [Atom](https://atom.io/),
and [Sublime](https://www.sublimetext.com/) are a few we've used in 
the past. However when you are working on a remote machine, a command editor like 
vim, emacs, or nano will be far more convenient. 

**`vim`** is our choice because it has the best learning-curve:power ratio.
 
**Session Leaders**: Tucker Fisher

## Table of Contents
1. [Prerequisites](#prerequisites)
1. [Content Taught Live](#content-taught-live)
1. [Bonus Materials](#bonus-materials)
1. [Preparation for Next Session: Python Part I](#preparation-for-next-session-python-part-i)
1. [FAQ](#faq)

## Prerequisites<a name="prerequisites"></a>
Before you dive in, you need to be able to [open a Bash terminal][howtobashlink]
on your machine. Also, you must have **`vim`** and **`tmux`** installed. Here are 
[instructions for downloading these tools][prepfromlastlink].

**There is one common challenge between `vim` and `tmux`: sometimes commands to
these programs are "silent" to the user. In some cases you will not see what you
have pressed until you have sent the command.**


## Content Taught Live<a name="content-taught-live"></a>
Open your bash terminal and follow the commands. Remember, for all the commands below don't type the leading
`$`. That is there to represent your prompt.

[Live 1: Setup and Refresh](#live-1-setup-and-refresh) || 
[Live 2: Vim](#live-2-vim) || 
[Live 3: "dot" files](#live-3-dot-files) ||
[Live 4: Tmux](#live-4-tmux) || 
[Live 5: SSH](#live-5-ssh) || 
[Live 6: Remote Graphics Forwarding](#live-6-remote-graphics-forwarding)


#### Live 1: Setup and Refresh
First, we will use a few commands we learned last week to setup for today's 
session. We need to make a directory for this week and download a few 
files.

If the symbols and commands below aren't familiar check out the [recap from 
last session][lastweeklink]. 

```bash
$ cd ~
```

We are going to make a new directory with `mkdir -p`. The `-p` flag will allow
`mkdir` to make intermediate directories. If you don't have a `cnjcx` directory,
this command will simultaneously create `~/cnjcx/` and `~/cnjcx/week_2/`. Note:
if the target directory already exists, the -p flag will suppress the error
message `mkdir: <dir>: File exists`.

```bash
$ mkdir -p ~/cnjcx/week_2
```
<a name="returnredirectfootnote"></a>

Make `week_2` your current working directory.

```bash
$ cd ~/cnjcx/week_2
```

Let's download a few files hosted on GitHub. The `curl` command transfers
data from a URL. The `-L` flag (capitalization matters with flags) allows `curl`
to follow HTTP redirects[<sup>1</sup>](#redirectfootnote). The `-o` flag tells `curl` to
rename the file to your specified name. For example without `-o` the first command would make
the file "JJdvq" instead of "basic_vimrc".

```bash
$ curl -L -o basic_vimrc https://git.io/JJdvq
$ curl -L -o basic_tmux.conf https://git.io/JJdei
$ curl -L -o vim_playground.txt https://git.io/JJh7g
```

Practicing a few more skills from last week, copy two of these files to your
home directory. You can do this one at a time, or combine the copy operations
together this way:

```bash
cp ./basic_vimrc ./basic_tmux.conf ../../
```

Above, the `./` stands for "current working directory". You don't need to put this
in, but it was a perfect time to refresh your knowledge from last week. `../../` 
is a reference to `../` move up, `../` move up in the directory tree. Again you could
have just used `~`, but this was a good refresher.


#### Live 2: Vim

Before you enter **`vim`** for the first time, there are a few things to keep 
in mind:
1. Unlike a standard text editor, vim listens for commands when it is first opened.
Different commands are called by pressing keys on your keyboard. Be careful not to press keys unintentionally!
1. Vim commands are case sensitive. If you accidentally press <kbd>Caps Lock</kbd> 
you might send a whole bunch of foreign commands and get lost or stuck.
1. If you ever get trapped or confused during this section and you can't quit, or
anything else _just close your terminal_. You can start it up again. If your
file gets messed up, no worries, just `curl` it again and start fresh! 
1. How to quit vim: 
    1. exit 
        - <kbd>Esc</kbd> then `:q` <kbd>Enter</kbd>
    1. save and exit 
        - <kbd>Esc</kbd> then `:wq` <kbd>Enter</kbd> (this is the most common way to exit vim)
        - <kbd>Esc</kbd> then `ZZ` <kbd>Enter</kbd>
        - <kbd>Esc</kbd> then `:x` <kbd>Enter</kbd>
    1. exit without saving (force exit)
        - <kbd>Esc</kbd> then `:q!` <kbd>Enter</kbd>
        - <kbd>Esc</kbd> then `ZQ` <kbd>Enter</kbd>
    1. emergency exit 
        - <kbd>Ctrl</kbd>-<kbd>C</kbd> then `:q!` <kbd>Enter</kbd>

Ok, open the vim playground and read through it. Just make sure you are home for dinner.

```bash
$ vim vim_playground.txt
```

If you would like to learn more take a look at `vimtutor`, a built-in tutorial program that explains vim basics.

```bash
$ vimtutor
```

#### Live 3: "dot" Files

If a file is prefixed by a `.` it is a **"dot" file**. A directory can also be
prefixed by a `.`, it would be called a **hidden directory**. These files and
directories often contain ancillary content and aren't modified by the user
during day-to-day operations on the command line. Broadly, "dot" files and hidden
directories hold your command line settings. 

Finder, File Explorer, and Ubuntu's Nautilus don't show these files. Terminal
also keeps them hidden. Unless you apply the `-a` flag, these files won't
appear in the `$ ls` output.  

In the remainder of the tutorial you will use "dot" files and hidden directories 
to improve upon the default operations of your command line tools. **`Vim`** will become
more powerful, **`tmux`** will become more convenient, and **`ssh`** options will be automatic. 

The first "dot" file you will add today is `.vimrc`. Right now this file is misnamed `basic_vimrc` so
vim doesn't run it automatically on startup.

Verify that `basic_vimrc` was copied properly. After running the next command
you should see the `basic_vimrc` close to the bottom of the list. The flags `-l`, `-a`,
`-r`, and `-t`, list in a column, show "dot" files, reverse order, and render by time.

```bash
$ ls -lart ~
```

In vim_playground.txt you learned how to change a vim setting: `:set number`.
Settings like this allow you to unlock the power of vim. However, it would be a
drag to manually set each of your favorite settings one at a time.

We need to rename `~/basic_vimrc` to `~/.vimrc` so vim knows to recognize
it. When you run vim it looks for a file located at `~/.vimrc`. The "rc" in
`.vimrc` stands for "run commands", and this is what it does. All the commands
in this file will be executed as vim opens. This file is the perfect place to
put your preferred settings.

**Note if you already have a `.vimrc` you like, please skip the next command
or temporarily move it: `$ mv `.vimrc` `.vimrc.bak`.**

```bash
$ mv -i ~/basic_vimrc ~/.vimrc
```

Open vim_playground.txt again to see the difference! 

```bash
$ vim vim_playground.txt
```

Every command in the `.vimrc` is explained. It is just a text file, so you can easily
take a look.

```bash
$ vim ~/.vimrc
```

#### Live 4: Tmux

Now that you have some comfort with "dot" files you can setup your `.tmux.conf`.
The `.tmux.conf`, like the `.vimrc`, runs commands. Inside `basic_tmux.conf`
are a few handy settings, including enabling your mouse. To verify you have it, 
run the following command.

```bash
$ ls -lart ~
```

`basic_tmux.conf` should be listed somewhere near the bottom of the list. If
not, go back to the beginning of the lesson and verify you ran the `curl`
and `cp` commands properly.

For practice, perform the move command slightly differently from
the `basic_vimrc` move. This time `mv` from within `~`, your home directory.

```bash
$ cd ~
$ mv -i basic_tmux.conf .tmux.conf
```

Now that the "dot" file is in the right place, you can open a new tmux session.
`$ tmux` will open a session with a default name, but a primary function of
**`tmux`** is to stay organized. This is how to open a session with a custom
name, "firstone":

```bash
$ tmux new-session -s firstone
```

When you open **`tmux`** it will look like just like terminal, but will have a
line of text at the bottom. We set the color to purple, from the default green,
in the ~/.tmux.conf. If you prefer green, you now know how to open that file
and edit it: `$ vim ~/.tmux.conf`. The "classic" **`tmux`** colors are there
"commented out" by a `#`. Tmux ignores all lines that begin
with `#` in the .tmux.conf.

Like **`vim`**, **`tmux`** has "hotkeys" as shortcuts for common commands. To
access these "hotkeys" we first need to learn about the **prefix keys** or what
is sometimes referred to as the **leader**. Whenever you want to send a command
to **`tmux`** you first send the **leader** <kbd>Ctrl</kbd><kbd>b</kbd> then
you command. For example to leave **`tmux`** is simple:
<kbd>Ctrl</kbd><kbd>B</kbd> + <kbd>d</kbd> (d stands for detach).  For the rest
of the session we will show the leader as `C-b`. This is how it is most often
documented.

NOTE: the terminals are full shells. We use the leader to separate tmux commands
from regular terminal commands.

`C-b` + `d` -- detaches from the session

Assuming you'd like to attach again you can run the following commands. `$ tmux ls` indicates
which sessions you currently have running. Attaching is done this way:

```bash
$ tmux attach-session -t firstone
```
...or the quicker equivalent.

```bash
$ tmux a -t firstone
```

The `-t` stands for target. It allows you to specify the session you'd like to attach to.

`C-b` + `d` -- to detach again, and open a new session called "secondone".

```bash
$ tmux new-session -s secondone
```

**`Tmux`** can manage multiple sessions, as you have just illustrated by opening
a second session. Run a `$ tmux ls` to see the open sessions if you are curious. Tmux can 
also manage multiple "panes" within a session. The "hotkeys" for making new panes are `"` to form
a horizontal split and "%" to form a vertical split.

`C-b` + `"` will split vertically.

`C-b` + `%` -- split horizontally.

To move between panes you can either use the mouse or use your arrow keys after the leader.

`C-b` + <kbd>&larr;</kbd> -- move left

`C-b` + <kbd>&rarr;</kbd> -- move right

`C-b` + <kbd>&darr;</kbd> -- move down

`C-b` + <kbd>&uarr;</kbd> -- move up

`C-b` + <kbd>;</kbd> -- move to last pane

`C-b` + <kbd>q</kbd> + # -- jump to pane number "#"

Tmux also accepts commands with `:` after the leader. You will see a bar appear at the bottom of your screen (similar to vim).

`C-b :swap-pane -t #` -- swap your current pane with number "#"

`C-b` + <kbd>space</kbd> -- reorganize windows.

Moving between sessions can be much simpler than detaching and reattaching. The `s` command
lets you switch between your open sessions. 

`C-b` + `s` -- choose from session tree. Use arrows to move between and <kbd>Enter</kbd> to
select (or type the number next to the session you want to switch to).

To kill a session is simple. Using the `kill-session` command and the target flag, `-t`, you can point 
to any session and kill it.

```bash
$ tmux kill-session -t secondone
```

#### Live 5: SSH

The command **`ssh`** is the most common way to form a connection with a
server. It stands for "**s**ecure **sh**ell". In order to use **`ssh`**, you
must have a server to connect to. Some universities have shared
computing resources students have access to. In the
examples we are going to use a shared Stanford resource called Farmshare2. If you are connecting 
to a personal server or lab computer you can check out [Setting Up Your Server](#setting-up-your-server) 
in the [Bonus Materials](#bonus-materials). 

Before you connect these are a few tidbits of jargon you might find useful.

- **Server** -- This is your remote machine. You will connect to this machine
  with **`ssh`**.
- **Client** -- This is your personal machine. You connect to the "server" from the "client".
- **Host** -- The "host" is the server. You can call it what you want. Something
  easy to remember.
- **Hostname** -- The "hostname" is specific, and carries real meaning. It is
  where the server can be found.  It could be an IP address on your local
  network (e.g. 171.25.46.172) or a public domain name (e.g. rice.stanford.edu for Farmshare2).
- **User** -- Also specific, the "user" is the identifier you use to login to
  the server. On Farmshare2 "user" is your SUNetID. On your personal server it will
  be the username of the account.
- **X11** -- is a windowing system that runs on your local machine. It receives
  graphical data, that would be GUIs on the server, and renders them on the client. You
  need "X11" to see the figures you make in Python, for example. 

To make a connection via **`ssh`** you run the following command. `ssh
<User>@<hostename>`. _Note: if this is the first time you have ssh'ed to a
particular server, you will be prompted to accept a key._

Here is what a first time login to Farmshare2 looks like (_you can accept the
fingerprint by typing "yes <kbd>Enter</kbd>"_):

```bash
$ ssh lelandjr@rice.stanford.edu
The authenticity of host 'rice.stanford.edu (XXX.XX.XX.XX)' can't be established.
ED25519 key fingerprint is XXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

If you are connecting to a server on your network (with user:rig43, and IP:
555.55.55.555) you will do it this way.

```bash
$ ssh rig43@555.55.55.555
The authenticity of host 'XXX.XX.XX.XX (XXX.XX.XX.XX)' can't be established.
ED25519 key fingerprint is XXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

**RICE SPECIFIC INSTRUCTIONS: When you login to rice you will be assigned a number.
Remember this number. You will need this to login later. The number will be in your
prompt after the word rice &rarr;** `SUNetId@riceXX:~$`.

Typically when an **`ssh`** tunnel is closed, or the connection drops, the processes you started are terminated.
If you are editing a file in vim it will be closed, if you are working in the python REPL your
work will be lost, and the neural network you are training will stall.

However, processes started from within a **`tmux`** window will stay alive after
closing the **`ssh`** tunnel. &larr; **This is the primary role of `tmux` for our purposes.**

Once you are logged into a server, open tmux and start editing a new file with **`vim`**.

```bash
$ tmux new -s stayalive
```

```bash
$ vim bookmark.txt
```

Detach from the session with `C-b` + `d` and close the **`ssh`** tunnel with `$ exit`.

Once you have detached, there are a few thing you can do to improve your **`ssh`** connection.

1. You can save the **host** to make **`ssh`**'ing easier.
2. You can enable window forwarding or "X forwarding" for **`ssh`** connections to this host.


#### Live 6: Remote Graphics Forwarding

In this section you will learn how to setup a host for "X forwarding". To get the most out of it, 
complete [Live 5: SSH](#live-5-ssh) first.

Verify that you have the **`ssh`** hidden directory `.ssh/` with `$ ls ~ | grep .ssh`

If you don't have `.ssh/`

```bash
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
```

If you already have an `.ssh/` directory, or you ran the preceding commands you can
run the following:

```bash
$ cd ~/.ssh
$ vim config
```

Inside the config file place these lines...

    Host <host_nickname> 
        Hostnme <your_host_name>
        User <usr_name_on_server>
        ForwardX11 yes
        ForwardX11Trusted yes

**\<host_nickname\>** -- should be a memorable name you use to refer to this server.

**\<your_host_name\>** -- should be the **hostname** of the server, it will be an
IP address or domain name. If you are connecting to Farmshare2 you should
connect to your assigned node from [Live 5: SSH](#live-5-ssh) (e.g.
riceXX.stanford.edu).

**\<usr_name_on_server\>** -- should be your username on the server (e.g. lelandjr).

All together this would look like this...

    Host ricenode
        Hostname rice09.stanford.edu
        User lelandjr
        ForwardX11 yes
        ForwardX11Trusted yes
    
Now that you have added this server to your `config` file, make sure that the `config` file
has the proper permissions.

```bash
$ chmod 644 ~/.ssh/config
```

Connecting to a **Host** that has been added to your `~/.ssh/config` is easy.

```bash
$ ssh <host_nickname>
```

Once you are connected to your server, check that you are X forwarding with the `$ xeyes` command.
If you don't see anything or `Error: Can't open display:` is returned you should verify that
you have setup your server for X forwarding, and have an X server for your client machine. We cover this in the
[bonus materials](#bonus-materials).

 
## BONUS Materials<a name="bonus-materials"></a>

#### SSH Server Setup

Getting ssh for your Linux server:

```bash
$ apt-get install openssh-server
$ systemctl status ssh
$ sudo systemctl enable ssh
$ sudo systemctl start ssh
```

To forward windows must allow X11Forwarding in your server's `/etc/ssh/sshd_config`

```bash
$ sudo echo "X11Forwarding yes" >> /etc/ssh/sshd_config
```

#### X Forwarding MacOS Client

Getting X11 for MacOS will allow you to forward windows to your laptop from a server.
Running these commands will download the installer for `XQuartz` and open your downloads
folder. Double-click on XQuartzInstaller.dmg to install.

```bash
$ cd ~/Downloads
$ curl -L -o XQuartzInstaller.dmg https://rb.gy/u3syhp
$ open .
```

#### Public-key Authentication

Setting up public-key authentication for a private server.

https://kb.iu.edu/d/aews


## Preparation for Next Session: Python Part I<a name="preparation-for-next-session-python-part-i"></a>

### CNJCx Week 3 Prerequisites
- [ ] Be able to open a terminal running `bash` (or `zsh`) on your machine
- [ ] Have Python 3.8 installed and available as the command `python3` in your terminal

This document walks through our recommended Python installation procedure for Mac and Linux. 

## [Click Here for macOS Instructions :apple:](#macos-instructions)
## [Click Here for Ubuntu (or Windows Subsystem for Linux) Instructions :penguin:](#ubuntu-instructions)
### [Office Hours Zoom Link](#office-hours)


### macOS Instructions<a name="mac-instructions"></a>
We're going to use Homebrew to install `python3` on Mac.

Open a terminal, and run these commands one at a time. Remember you don't need to type the `$`!
Each of these commands might take a few minutes, don't worry if it's taking longer than expected.

#### Step 1: Install Python 3 with Homebrew
The first command installs xcode command line tools, if you don't already have them. If you do have
them, that command will result in an error. That's okay.

The second command installs Homebrew. If you already have Homebrew you can skip this step, but running it anyway won't hurt.

The third command installs the Python 3 binary. If you already have this package installed with Homebrew, you'll get a warning. That's okay.
```bash
$ xcode-select --install
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
$ brew install python3
```

If you get an error that looks like `Error: python@3.8 3.x.x` is already installed, run
```bash
$ brew upgrade python@3.8
```
to fix it.

#### Step 2: Verify that Python 3 was Installed
```bash
$ python3 --version
```

You should see "Python 3.8.5" (the most recent version of Python 3 as of the writing of this guide). If you don't see that version, but see another version of Python 3 instead, that means you have a previous Python 3 installation that is taking precedence on your machine's (`$PATH`). 

#### Step 3: Alias `python3` to the Homebrew binary
**:warning: If you are using Zsh as your shell instead of bash, replace `~/.bash_profile` with `~/.zshrc` instead :warning:**.

[See which shell you're using](#shell-config-files).
```bash
$ echo -e "\n# Adding during CNJCx\nalias python3='$(brew --prefix)/opt/python3/bin/python3'" >> ~/.bash_profile
$ exec $SHELL
```
For the curious, this is appending an alias to the end of your `~/.bash_profile` file, so that `python3` always means "use the Homebrew version".

Now when you run `python3 --version` you should always see "Python 3.8.5" and when you run `which python3` you should see something like `python3: aliased to /usr/local/opt/python3/bin/python3`.

### Ubuntu Instructions<a name="ubuntu-instructions"></a>
On Ubuntu, we're going to install python3.8 from the deadsnakes repository. Run these commands in your terminal.
These steps require root privileges, i.e., they start with `sudo`. When are you are prompted for your password, use the password you made when creating your Ubuntu subsystem.

#### Step 1: Install python3.8
```bash
$ sudo add-apt-repository ppa:deadsnakes/ppa
$ sudo apt-get update 
$ sudo apt-get install python3.8
$ sudo apt-get install python3.8-venv
```

#### Step 2: Verify that Python 3.8 was installed
```bash
$ python3.8 --version
```

#### Step 3: Alias `python3` to the newly-installed binary
**:warning: If you are using Zsh as your shell instead of bash, replace `~/.bashrc` with `~/.zshrc` instead :warning:**.

[See which shell you're using](#shell-config-files).
```bash
$ echo -e "\n# Adding during CNJCx\nalias python3='$(which python3.8)'" >> ~/.bashrc
$ exec $SHELL
```

### Office Hours<a name="office-hours"></a>
If you run into problems installing Python with these instructions, please attend our Week 3 office hours.
You are also welcome to attend if you have lingering issues from content in Weeks 1 and 2!

**Week 3 Office Hours**: Wednesday, August 26, 6:00pm-7:00pm Pacific Time

[Office Hours Zoom Link][officehourslink] (password: 896261)

### Details for Nerds
**Why is this so complicated?** 

_Installing Python would be hard enough if everyone had identical starting points (same operating system, same history of Python installations), but the reality is that people have all sorts of Python installations on their machine. It's easy to forget when, how, and why some of those versions were installed!_

**Don't I already have Python installed?** 

_It's very common for people to already have a version of Python installed. Unfortunately, the default Python installed with macOS is outdated and isn't recommend for use. Even worse, uninstalling it can break programs that use it behind the scenes! For other installations, their suitability for the content in CNJCx depends on how they were installed and the specific Python version_

**Can I use a tool like `pyenv` instead?** 

_Sure! We love `pyenv`, but thought it would be more instructive to use the "default" tools for CNJCx._

**Why alias python3 instead of inserting the Homebrew folder to the start of `$PATH`?**

_Many users don't actually know how their `$PATH` is being constructed, and aliases take precedence over paths anyway. Thus, this is probably the safest 'catch all' solution for now._

### Which shell configuration file should I edit?<a name="shell-config-files"></a>
To figure out what your configuration file is called, run `echo $SHELL`. You should see either `/bin/bash` or `/bin/zsh`. If your shell is `/bin/zsh`, your configuration file is `~/.zshrc`. If your shell is `/bin/bash`, it is either `~/.bash_profile` (if you're on macOS) or `~/.bashrc` (if you're on Ubuntu).

Your Shell | Configuration file
-----------|-------------------
bash (macOS) | ~/.bash_profile
bash (Ubuntu) | ~/.bashrc
zsh | ~/.zshrc

## FAQ<a name="faq"></a>

### Is there a special X11 client I need for my Mac?

Yes, XQuartz. We show you how to download it in the [bonus materials](#bonus-materials)

### How do I move files to or from my server?

With the **`scp`** command:

to server...

```bash
$ scp /local/path/to/file <usr_name>@<host_name>:/path/to/destination
```

from server...

```bash
$ scp <usr_name>@<host_name>:/path/to/file /local/path/to/destination
```

### I'm getting a "bad owner or permissions" on ~/.ssh/config; why?

You probably created `~/.ssh` or `~/.ssh/config` with the wrong permissions.

```bash
$ chmod 700 ~/.ssh
$ chmod 644 ~/.ssh/config
```

--------
[<sup>1</sup>](#returnredirectfootnote)<a name="redirectfootnote"></a> HTTP redirects
are pretty simple. When your web browser reaches a website with a redirect, it sends your browser
to a different URL automatically. URL shorteners use this all the time! In our 
case, the URLs to these files are looooonnnngggg so we are redirecting from short, 
easy to type URLs.

[officehourslink]: https://stanford.zoom.us/j/8505742709?pwd=S2FHWkxySHBON2VtZGZTRTFFMGZNdz09
[howtobashlink]: https://stanford-cnjc.github.io/#/CNJCx#bashInstructions
[prepfromlastlink]: https://github.com/stanford-cnjc/cnjcx-course-materials/blob/master/week1_commandline/cnjcx_week1_recap.md#nextsesh 
[lastweeklink]: https://github.com/stanford-cnjc/cnjcx-course-materials/tree/master/week1_commandline
