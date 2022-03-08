# CNJCx: Practical Python
## Git, GitHub, Clean Code, and Open Science
### Reference Material

**Session Leaders**: Russ Poldrack, Tucker Fisher, and Eshed Margalit

## Table of Contents
1. [Table of Git Commands](#tcm)
1. [Interacting with a Remote (e.g. Github)](#remote)
1. [Resources and Tips](#rnt)

This table covers the commands we discussed in week_4, including useful flags and options. 

Don't understand our conventions? Occasionally we refer to a `[placeholder]` (e.g. `git branch [branchname]` you would... `git branch thenameyouwant` or `echo $[variable]` you would... `echo $THEVARIABLEYOUWANT`.

## Table of Git Commands<a name="tcm"/>
| Command | Description | Common&nbsp;uses&nbsp;and&nbsp;flags |
| :-: | --- | --- |
| <code>git &#8209;&#8209;help</code> | basic help from git. A nice way to remind yourself what command to use. | <code>git [command]&nbsp;&#8209;&#8209;help</code> will open the git manual (detailed help) for that particular command. For example: <code>git&nbsp;init&nbsp;&#8209;&#8209;help</code> will tell you all about `git init`. Press <kbd>q</kbd> to leave the manual page. We used `--help` to make this table. |
| `git init` | Initialize an empty repository in the current directory. | You can also provide git init with a path, like <code>git&nbsp;init&nbsp;/path/to/dir</code> |
| <code>git&nbsp;status</code> | Information about the current position in your version graph. | `git status` tells you your current branch, and lists your non-staged, non-committed and untracked files. |
| `git add` | Stages a file for <code>git&nbsp;commit</code>. Once a file is `add`ed it will always be **tracked**. **`git`** knows to pay attention to **tracked** files and will alert you in the <code>git&nbsp;status</code> message when it changes. | <code>git&nbsp;add&nbsp;&#8209;u</code> will add all tracked files. Super handy if you have a commit that will span a few files. <code>git&nbsp;add&nbsp;[file]</code> will add that file. | 
| <code>git commit</code> | Save your staged changes to the version control history. | <code>git&nbsp;commit&nbsp;&#8209;m&nbsp;"your&nbsp;commit&nbsp;message&nbsp;in&nbsp;quotes"</code> the `-m` flag allows you to specify a commit message. Without `-m` you will be dropped into **`nano`** or **`vim`** to write a message. Save yourself some time and use `-m` |
| <code>git&nbsp;log</code> | Lists the commits under your current position in the version control history. | <code>git&nbsp;log&nbsp;&#8209;&#8209;decorate</code> to see your branches.<br/><code>git&nbsp;log&nbsp;&#8209;&#8209;graph</code> to see the branch history of your version control history. <br/><code>git&nbsp;log&nbsp;&#8209;&#8209;oneline</code> to see just the unique commit hash and message for each commit.<br/> <code>git&nbsp;log&nbsp;&#8209;&#8209;all</code> to see all of your version history (not just what is back-in-time). |
| <code>git&nbsp;checkout</code> | Moves you (and your files) to a specified position in the version control history. | <code>git&nbsp;checkout&nbsp;[location]</code>: `[location]` can be a _commit hash_, a branch, or a reference to your current position (`HEAD~` takes you one step back in history, `HEAD~2` would take you two steps back).<br/> <code>git&nbsp;checkout&nbsp;&#8209;&#8209;&nbsp;[file]</code>: This is a bit more nuanced, you are "checking out" your current position for that file. Since you don't have that file's changes committed this amounts to dropping changes to the specified file. Be careful, you will loose those changes. (<code>git&nbsp;stash</code> is what you want to save changes out of sight w/o committing).</br> <code>git&nbsp;checkout&nbsp;&#8209;b&nbsp;[branchname]</code>: make a branch and place your `HEAD` there.|
| `git branch` | List and manipulate branches. | `git branch [branchname]`: will make a new branch called "branchname".<br/> `git branch` lists branches. |
| <code>git&nbsp;merge</code> | Incorporate changes from another branch or commit. You will be prompted to make a merge message. | <code>git&nbsp;merge&nbsp;[branch&nbsp;or&nbsp;commit_hash]</code>. Also note, if you have multiple remotes, you will have to specify <code>git&nbsp;pull&nbsp;&#8209;&#8209;rebase&nbsp;[remote]</code> |

## Interacting with a Remote (e.g. Github)<a name="remote"></a>

| Command | Description | Common&nbsp;uses&nbsp;and&nbsp;flags |
| :-: | --- | --- |
| <code>git&nbsp;clone</code> | Clone a remote repository onto your machine. | <code>git&nbsp;clone&nbsp;[repo_url]
| <code>git&nbsp;pull&nbsp;&#8209;&#8209;rebase</code>  | After you have committed your local changes you can retrieve and incorporate changes from the remote. | <code>git&nbsp;pull</code> will initiate a merge,  its probably best to always <code>&#8209;&#8209;rebase</code>. If you happen to have multiple remotes for a project, you will have to specify <code>git&nbsp;pull&nbsp;&#8209;&#8209;rebase&nbsp;[remote]</code> |
| `git push` | Incorporate your changes with the remote | As before, if you have multiple remotes you must specify <code>git&nbsp;push&nbsp;[remote]</code>. |

 ## Bonus Bash
| Command | Description | Common&nbsp;uses&nbsp;and&nbsp;flags |
| :-: | --- | --- |
| <code>echo&nbsp;$[variable]</code> | Often we wold like to know the value of a variable. Bash variables are accessed using the `$`. We use `echo` to place any variable into the standard output, making it readable (to us). |  `echo $HOME` places your "home" path to the standard output. |
| <code>cd $\_</code> | The <code>\_</code> variable is constantly maintained by your shell as the "last input". | <code>mkdir&nbsp;&#8209;p&nbsp;/path/to/new_dir&nbsp;&&&nbsp;cd&nbsp;$\_</code> will drop you directly into the directory you just created with `mkdir -p`. |

## Resources and Tips<a name="rnt"></a>

Learn some more advanced **`git`** usage at [learngitbranching.js.org](https://learngitbranching.js.org/).

Make prettier `README.md` with some [markdown tips from Github](https://guides.github.com/features/mastering-markdown/).
