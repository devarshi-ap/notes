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
#! /bin/sh
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
