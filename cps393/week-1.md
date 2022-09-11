---
description: Basics of Bash, Moon Servers, & Vim
---

# Week 1

* ssh \<userid>@moon.cs.ryerson.ca
* Change PW (if logged in): `passwd`
* Logout: `exit`
* Exit Vim: `:wq` (save) / `:q!` (no-save)

Path to _**LABS**_: `cd /usr/courses/cps393/dwoit/labs`

Path to _**NOTES**_: `cd /usr/courses/cps393/dwoit/coursenotes`

* (u.txt = notes for week x)
* copy file into your moon, then edit
  * `cp <filename> <newlocation>`
  * `cp u1.txt ~` : moves u1 to root dir

**Linux** \[**Unix**] is an operating system (OS), much like Win & MacOS. It has many flavours like:

* Ubuntu, Fedora, Debian, ...

OSs based on Linux/Unix: MacOS, ChromeOS, Android, iOS

**Terminology**

**`OS`** - program(s) helping us communicate with computer's resources

* ie. memory, processor, storage

OS is layered:

* `utilities` - commands availble
* `shell` - a command-line interface program. many flavours (bash, zsh, ...)
  * used to communicate with the **kernel**
* `kernel` - heart of OS
  * controls access to hardware
  * maintains file system
  * manages computer's memory
  * allocates resources among various activities (ie. CPU time)

**`VIM`** - terminal-based text editor for Unix

* `vim <filename>`

**Path**

* Absolute Path: _from root dir_
  * eg. `/Users/home/projects/course-notes/index.html`
* Relative Path: _from current dir_
  * eg. `course-notes/index.html` (if cwd == `/Users/home/projects/`)
* Parent Directory: `..`
* Directory Itself: `.`

**File Management**

* 'directory' == 'folder' == 'entry'
* File system is a tree (see `tree` command)
* Topmost directory in tree is `/` or "root"

**Linux Commands**

Commands are stored in `bin/` (binary)

modern day swiss army knife; case sensitive

* `pwd`: _print working directory_
* `cd`: _change directory_
* `ls`: _list_
  * `-a || -A`: include dotfiles (`.` for `-a`, `.. && .` for `-A`)
  * `-l`: include more information (size, modification time, etc.)
  * `-d`: include _only_ directories
  * `-t`: sort by modification time
  * `-r`: reverse order
  * `-R`: _**recursive**_ list, whole subtree
* `mkdir`: _make directory_
* `cp`: _copy_
  * `-R`: _**recursive**_ copy, can possibly overwrite
* `mv`: _move_
  * Can possibly replace existing files
  * `mv lab1.txt lab1` (assume lab1.txt & lab1/ are in same dir)
* `rmdir`: _remove dir_
  * Precondition: the current dir is empty
* `rm`: _remove/delete file(s)_
  * `-r`: _**recursive**_ delete, used for non-empty directories
  * No “Recycle Bin”/Trash
* `cat`: display file content
  * `cat fn1 fn2 fn3` - 3 files displayed consecutively
  * `tac` == `cat`, but reveres file displayed (last line to first line)
* `wc`: gives size (lines, words, chars) of files
* `diff`: shows difference between 2 files (like git vcs)
  * `diff fn1 fn2`

**`#`** = comments

* `ls f1 f2 #f3 f4` === `ls f1 f2`

**Linux Security**

Each file+dir has an **owner**+**group** associated with it:

**`Owner`**

* when you create a file, you become its owner (usually)

**`Group`**

* users can join "groups" of other users with whom they can share files & dirs
* users can join many groups, but have _1 primary group_
* users can _work_ in different groups (change groups with `newgrp newgroup`)
* when a user creates a file, the **file's group** == **group the user was in when the file was created** (typically your **primary group**)

Note: IN CS, ONLY SYSADMINS CAN CREATE GROUPS AND ADD USERS TO GROUPS.

**Permissions**

Linux divides the file permissions into:

* **READ** - **r**
  * file: can be _read_ / _copied_
  * dir: can look at its contents (list dir\`s files/subdirs ). But can't display contents of a file inside (would need **r** on the file and **x** on dir for that)
* **WRITE** - **w**
  * file: can _modify_ / _delete_
  * dir: _add/delete_ entries to/from dir
    * can modify a file in dir without **w** on dir
* **EXECUTE** - **x**
  * file: can _run_ it, if it's an executable file (ie. /usr/bin/ncal)
  * dir: weaker than **r**; can access an entry of dir, if you know its name but cannot list contents of dir.

**Vim**

\[[Cheat Sheet](https://vim.rtorr.com)]

`vim fn1`

`:w` - save changes

`:wq` - save and exit Vim

`:q!` - don't save changes and quit

`<esc>` - enters normal mode (ie. to exit _insert mode_, )

`x` - deletes char _after_ cursor

`i` - enter **insertion mode**, insert _before_ the cursor

`a` - enter **insertion mode**, and insert (append) _after_ the cursor

**delete operators & motions**

delete operator == **\[d]**

* `dd` - deletes the entire line

motions:

* `w` - until the start of the next word, EXCLUDING its first character.
* `e` - to the end of the current word, INCLUDING the last character.
* `$` - to the end of the line, INCLUDING the last character.

ie. delete operator + motions:

* `dw` - delete the chars of the word from the cursor to the start of the next word.
  * (I like to bag eat watermelon) > cursor on **|b**ag > **dw** > (I like to eat watermelon)
* `d$` - delete to the end of the line

Typing a **number** before a **motion** repeats it that many times:

* `2w` - move the cursor 2 words forward.
* `3e` - move the cursor to the end of the 3rd word forward.
* `0` - move to the start of the line.

Typing a **number** with an **operator** repeats it that many times.

* `d2w` - delete the two

`u` - undo action

`U` - undo all the changes on a line

`Ctrl + r` - undo the Undo's

Copy & Paste Lines:

* `dd` - deletes the line & stores it in a Vim register.
* `p` - paste after cursor from register.

`r<charX>` - replaces the char ahead of cursor with charX

`Ctrl + g` - shows location in file and file status

`(N) + G` - jumps to line N

* `G` - jump to bottom of file
* `gg` - jump to top of file

`/(phrase)` - search for phrase. hit , then:

* `n` - next hit
* `N` - previous hit

`:s/<old>/<new>` - swaps first occurrence of w/ in the current line

* `:s/<old>/<new>/g` - swaps all occurrences in current line
* `:s/<old>/<new>/gc` - swaps all occurrences in file

`:!<bash commands>` - you can temp. write external shell commands from vim

`:w filename` - save changes of current file to _filename_

`:v` - select text ( to unselect)

`y` - yank (copy) selected text

`p` - put (paste) selected text

**Permissions**

`ls - l`: lists w/ permissions

```
- means not set ie. rwx means read, write, exec. capability

ex.    rw-r-xr--
rw-               r-x                  r--
OWNER             GROUP                OTHERS
Read, Write       Read, Exec.          READ
```

`chmod`: used by owner to change permissions

* `chmod (ugoa)(+-=)(rwx) name(s)`
  * **ugoa**: user/group/others/all (all means User & Group & Others)
  * **+-=**: (+ add given perms) | (- remove given perms) | (= change to exactly those given perms)
  * **rwx**: permissions

ex. supose myFile has perms:    -rwxr-xr--

* (- file) (OWNER rwx) (GROUP r-x) (OTHERS r--)
* `chmod g+w myFile` : g+w = group/add/write ==== add write perm to group
  * now, -rwx rwx r--
* `chmod ug-x myFile` : ug-x = user+group/remove/exec. ==== remove execute perm from user + group
  * now, -rw- rw- r--
* `chmod a+r+w+x myFile` : a+r+w+x = all/remove/exec. ==== add read, write, exec. perm to all
  * now, -rwx rwx rwx
* `chmod go=rx myFile` : go=rx = group+others/exactly/rx ==== change group + others perms to exactly rx (or r-x)
  * now, -rwx r-x r-x
* `chmod g=x,o+w myFile` : g=x, o+w = group/exactly/exec, then others/add/write ==== change group perm to exactly x (or --x), then add write perm to others.
  * now, -rwx --x rwx

\-rw- r-x r-x

* HW 1: `chmod go=- myFile`
* HW 2: `chmod a+x,g+r,u-w myFile`
* HW 3: tst1, tst2, tst3, dog, cat

**I/O Streams**

Linux commands do I/O. The shell knows WHERE to read/write to using **`streams`** (tunnels; _output sent down one, input received from another_)

Linux assigns **3 standard streams** to any command:

1. `stdin (0)`: Standard Input - eg. Keyboard input goes through `stdin`
2. `stdout (1)`: Standard Output - eg. Terminal output (printing to screen)
3. `stderr (2)` : Standard Error

When command:

* needs to read input, it reads whatever's in stdin
* produces output, it sends it down stdout
* produces error message, it send it down stderr

Note: many commands ignore `stdin` if you give them a file to operate on (`cat`, `wc`; read directly from lab1 instead of looking in **stdin**)

**I/O Redirection**

Linux includes redirection commands for each stream which can be used to write stdout/stderr to a file (created if DNE)

> Commands with a single bracket _overwrite_ the destination’s existing contents.

**Overwrite**

* **`>`** - standard output; redirect output, overwriting target if exists
* **`<`** - standard input; redirect input
* **`2>`** - standard error; redirects stderr (2) only

> Commands with a double bracket _do not_ overwrite the destination’s existing contents.

**Append**

* **`>>`** - standard output
* **`<<`** - standard input
* **`2>>`** - standard error

```bash
# redirects stdout
# attaches other end of stdout to myFile to see output of ls command
ls > myFile
# ls can be vim/cat/...

# eg. write contents of tst1 to tst.new (== cp tst1 tst.new)
# STDOUT: redirect output (cat tst1) to target (tst.new)
cat tst1 > tst.new

# eg. create a input stream to myFile and write content:
cat > myFile
first line in file
second line in file
^d    # end of file in Linux (^z in Win)
```

**Devices**

`device` : usually a piece of equipment for storing/communicating data

* eg. printer, disk drive, terminal

> Presented as files in Linux

Unix kernal _creates_ file names and _emulates_ file operations, known as ‘Special Files’, typically found in dir `/dev`

* eg. a printer might be file `/dev/lp0`, therefore:
  * `cp myFile /dev/lp0` prints myFile on line printer
  * `echo "hi there" >/dev/pts/4` writes message directly to terminal
* eg. standard streams are files `/dev/<stdin/stdout/stderr>`, therefore:
  * `cp blah /dev/stderr` displays file contents on stderr

> Null device (`/dev/null`) is device file that discards all data written to it but reports that the write operation succeeded
>
> ```bash
> # will stderr if a file DNE
> $ wc file1 file2 file3 2>/dev/null
> 7   8  34 file1
> 28  32 136 file2
> 21  24 102 file3
> 56  64 272 total
> ```
