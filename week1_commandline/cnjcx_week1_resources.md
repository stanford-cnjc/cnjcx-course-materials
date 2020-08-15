# CNJCx: Practical Python
## Command Line Basics (Week 1)
### Reference Material

**Session Leaders**: Josh Melander, Eshed Margalit, and Tucker Fisher

## Table of Contents
1. [Table of Commands](#commands)
1. [Resources and Tips](#rnt)
1. [FAQ](#faq)


## Table of Commands<a name="commands"></a>
The following table documents all of the commands that were introduced in week 1, including commonly used flags and options. Please refer back to this table at any time!
| Command | Description | Common uses and flags|
| --- | --- | --- |
| `pwd` | [p]rints [w]orking [d]irectory: prints the absolute path of your current working directory to the standard output, i.e., your terminal | N/A |
| `ls` | "list"s the contents of your current working directory, including files and directories |`ls -l` lists the contents with one entry per line, and `ls -rt` lists the contents in order of the last [t]ime they were modified, but [r]everses the list so that the last-modified entry is at the bottom (useful in directories with many entries). `ls -lrt` is an example of combining flags. Lists one entry per line, sorted in reverse chronological order |
| `ls [directory]` | "list"s the contents of the specified directory instead of the current working directory | Same as `ls`|
| `cd [directory]` | [c]hange [d]irectory. Changes the current working directory to the directory provided: replace `[directory]` with the relative or absolute path to the desired directory | `cd ~` returns you to your home directory |
| `mkdir [new_directory]` | create a new directory. replace `[new_directory]` with the relative or absolute path to the directory to be created | `mkdir -p` creates parent directories if needed, e.g., if you want to `mkdir cnjcx/week1` but `cnjcx/` doesn't exist yet, the `-p` flag allows `mkdir` to create it along the way |
| `touch [filename]` | creates a file with the specified filename, or, if the file already exists, updates the record of when it was last modified | N/A |
| `clear` | clears the output currently visible in the terminal window | N/A |
| `cat [filename]` | print the contents of a file to the standard output, i.e., the terminal | `cat -n` will print line numbers next to each line of the printed file |
| `echo [message]` | Print the specified message to the standard output, i.e., the terminal.| `echo "Hello World" >> myfile.txt` would append "Hello World" to the file `myfile.txt` | 
| `[stream] > [file]` | Overwrite the contents of `[file]` with the output of `[stream]`. You can think of this as redirecting the output of `stream` away from the standard output (the terminal) and into the specified file | `>\|` can be used instead of `>` to force an overwrite if an error is raised about the file already existing.|
| `[stream] >> [file]` | Appends the output of `[stream]` to the bottom of `[file]` without overwriting previous content. |N/A |
| `df` | Display storage devices on the filesystem and their free space | `df -h` will print storage usage in [h]uman-readable format |
| `mv [source] [destination]` | Moves the file or directory specified by `[source]` to a new `[destination]`. If `[destination]` already exists, it will be overwritten!| `mv -i [source] [destination]` will warn you before overwriting |
| `cp [source] [destination]` | Copies the file specified by `[source]` to a new `[destination]`. If `[destination]` already exists, it will be overwritten!| `cp -i [source] [destination]` will warn you before overwriting |
| `cp -r [source_directory] [destination]` | Copies the directory specified by `[source_directory]` to `[destination]` | N/A |
| `find [directory] -name '[search pattern]'` | Finds files in `[directory]` whose name contains `[search pattern]`| `[search pattern]` may include wildcards (`*`) which match any set of characters at that location in the pattern |
| `grep -R [search pattern] [directory]` | Finds lines in any file in `[directory]` that match the `[search pattern]` | `grep` also accepts wildcards (`*`)|
| `curl -o [new_filename] [URL]` | Downloads the contents at the specified `[URL]` and renames them to `[new_filename]` | `curl -L [...]` may be needed to follow redirects (e.g., for shortened URLs) |


## Resources and Tips<a name="rnt"></a>

### Resources
Places you can go to for some extra help:

- [Software Carpentry's "The Unix Shell" Course][scbashscriptinglink]: a detailed and thorough introduction to the shell.
- [Bash Scripting Tutorial][rtbashscriptinglink] from Ryan's tutorials.
- [`tldr` Website][tldrlink]: a web interface for the `tldr` program to show common uses for shell programs
- [ExplainShell][eslink]: enter any shell command and get a detailed breakdown of what each part does

### Tips
1. You can press the <kbd>Tab</kbd> key on your keybaord while typing the path to a
file or directory to "tab-complete". This is a great way to prevent typos and save time.
1. Press the up-arrow key on your keyboard to see the last command you entered. Continue
pressing "up" to scroll through past commands.
1. View a list of recently-run commands by using the `history` command.
1. Look into the commands `pushd`, `popd`, and `dirs` to efficiently swap working directories around 

-------------

[scbashscriptinglink]: https://swcarpentry.github.io/shell-novice/ 
[rtbashscriptinglink]: https://ryanstutorials.net/bash-scripting-tutorial/bash-script.php
[tldrlink]: https://tldr.sh/
[eslink]: https://explainshell.com/
