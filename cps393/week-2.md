---
description: globbing, grep, and intro to bash scripting
---

# Week 2

**Glob Constructs, Meta-Chars, & Special-Chars**

`globbing` : used for matching or expanding specific types of patterns

* mostly used to match filenames or searching for content in a file.
* uses _wildcard characters_ (`?`, `*` , `[]`, `^`, `!`, `$`, `{}`, `|`,) to create the pattern:
* **`?`** - matches single character (1-1)
  * ex. match any 4-char .txt file : `ls ????.txt`
  * ex. match any file w/ 4-char name & 2-char ext : `ls ????.??`
  * ex. `ls week?.txt` can match week1.txt, ... weekN.txt
* **`*`** - matches N-characters (1-N)
  * ex. match any file w/ .tsx ext : `ls *.tsx`
  * ex. match any file that starts w/ "a" : `ls a*.*`
* **`[]`** - matches any character from range
  * range of:
    * all **uppercase** alphabets : `[:upper:] or [A-Z]`
    * all **lowercase** alphabets : `[:lower:] or [a-z]`
    * all **numeric** alphabets : `[:digit:] or [0-9]`
    * all **alphabets** : `[:alpha:] or [a-zA-z]`
    * all the above: `[:alnum:] or [a-zA-Z0-9]`
  * ex. match any file that starts w p/q/r/s : `ls [p-s]*`
  * ex. match any file that starts w 1/2/3/4/5 : `ls [1-5]*`
  * ex. `ls prog[1-58].c` => possible: prog1.c, prog34.c
  * ex. `ls *[-]*` => possible: prisma-api.md, redux-tk.md
* **`!`** - exclude
  * `[!ABC]` : matches any single char `except A, B or C`
  * `[!a-z0-4]` : matches any single char `except a,...z, 0, ...4`
* Character Classes
  * \[:alnum:] \[:alpha:] \[:blank:] \[:cntrl:] \[:digit:] \[:graph:] \[:lower:] \[:print:] \[:punct:] \[:space:] \[:upper:] \[:xdigit:]
  * ex. match any file that starts w/ a A-Z : `ls [[:upper:]]*`
  * ex. combine multiple classes: `ls lab[[:digit:][:lower:]].*` (0-9 & a-z)
* Specials Characters:
  * `~` : your home directory name (/home/dwoit in my case)
  * `~usr` : the home dir of user with userid "usr"
  * `~-` : your previous working dir (note in bash cd - same as cd \~-)
  * `~+` : your current working dir
  * `\` : ignore glob construct following (like "" or '')
    * ex. `echo /[abc]*` outputs: `[abc]*`
  * `\` : at end of line, means command continues on next line
* Patterns & RegEx
  * `*(exp)` : 0 >= occurrences of exp
  * `+(exp)` : 1 >= occurrences of exp
  * `?(exp)` : 0 / 1 occurrences of exp
  * `!(exp)` : anything that _does not_ match exp
  * `@(exp1|exp2|...)` : anything that matches exp1 or exp2 or ...

**Bash Scripting**

Running **`.sh`** Scripts

```bash
$ sh myscript
```

Alternatively, in your `myscript.sh` file, do the following

```bash
#!/bin/sh
chmod u+x myscript    # sets 'executable' flag on the file
```

and run it with...

```bash
$ ./myscript
```

**Arguments**

Arguments can be passed into a script as you would w/ any bash command.

```bash
$ ./myscript foo bar baz    # params spaced after filename
```

* `$#` : number of args (3)
* `$n`: param name (`n` is the number)
  * eg. `$1 = "foo"`
* `$*`: One string with all parameter names
  * `"foo bar baz"`
* `$@`: Comma seperated strings for each parameter name
  * `"foo", "bar", "baz"`
* `shift`: Shifts Positional Parameters by 1



**Grep**

> _Global Regular Expression Print_
>
> syntax : `grep string filename(s)`
>
> * `string` : string to search for
> * `filename(s)` : files to search string in
>   * w/o file, grep will read from stdin until EOF
>
> Displays the lines of the file containing the string

```bash
# search for string in 1 file
$ grep "editor" vimTutorial.txt

    In this lab you will learn to use the vim editor by actually
    This exits the editor, DISCARDING any changes you have made.
    # and so on....

# search for string in 2 files
$ grep "scanf" waterTemp.c switch.c

# filename:        line contents
waterTemp.c:     scanf("%lf", &tmp);
switch.c:        scanf("%c", &letter);
```

Options

* `-i` : ignore case
* `-v` : print liens **not matching** search string
* `-x` : search string must match entire line

Metacharacters

* `.` : like `?` in glob (subs in any char)
* `*` : 0 or more reps of previous char (not like `*` in glob)
* `^` : patten must be at the start of the line (ie. `"^Raiders"`)
* `$` : pattern must be at the end of a line (ie. `"Chargers$"`)
* `\{m\}` : exactly **m** reps of previous char (ie. `"x\{3\}"`)
* `\{m,\}` : atleast **m** reps of previous char
* `\{m,n\}` : between **m** to **n** reps of previous char (inclusive)
* `\<` : line has word that starts w/ character (ie. `"\<x"`)
* `\>` : line has word that ends w/ character (ie. `"x\>"`)

```bash
# examples

grep '^Assignment' fname # lines starting with Assignment
grep -v '^Assignment' fname # lines not starting with Assignment
grep 'Assignment$' fname # lines ending with Assignment
grep 'd.g' fname # lines containing dag, dbg, dcg, d0g, d1g, etc
grep 'su*m' fname # lines containing sm, sum, suum, suuum, etc
grep 'suu*m' fname # lines containing sum, suum, suuum, etc
grep '\<so\>' fname # the word so (vs. social, absolute)
grep '[A-Za-z][A-Za-z]*' fname # lines containing ANY non-empty alpha string
grep '^[A-Za-z][A-Za-z]*$' fname # lines containing ONLY alpha characters
grep 'xyz\.w\{2,3\}X' # lines containing xyz.wwX or xyz.wwwX
grep 'A(bc)\{2,3\}D' # lines containing AbcbcD or AbcbcbcD
grep -x "abc" # lines that contain exactly and only abc
```
