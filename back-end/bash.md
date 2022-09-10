# Bash

## Core Commands

| Key/Command     | Description                                                               |
| --------------- | ------------------------------------------------------------------------- |
| cd \[folder]    | Change directory e.g. `cd Documents`                                      |
| cd              | Home directory                                                            |
| cd \~           | Home directory                                                            |
| cd /            | Root of drive                                                             |
| cd -            | Previous directory                                                        |
| ls              | Short listing (just names)                                                |
| ls -l           | Long listing (names + extra info)                                         |
| ls -a           | Listing incl. hidden files                                                |
| ls -lh          | Long listing with Human readable file sizes                               |
| ls -R           | Entire content of folder recursively                                      |
| sudo \[command] | Run command with the security privileges of the superuser (Super User DO) |
| open \[file]    | Opens a file ( as if you double clicked it )                              |
| top             | Displays active processes. Press q to quit                                |
| nano \[file]    | Opens the file using the nano editor                                      |
| vim \[file]     | Opens the file using the vim editor                                       |
| clear           | Clears the screen                                                         |
| reset           | Resets the terminal display                                               |

## Chaining Commands

| Key/Command                    | Description                                          |
| ------------------------------ | ---------------------------------------------------- |
| \[command-a]; \[command-b]     | Run command A and then B, regardless of success of A |
| \[command-a] && \[command-b]   | Run command B if A succeeded                         |
| \[command-a] \|\| \[command-b] | Run command B if A failed                            |
| \[command-a] &                 | Run command A in background                          |

## Command History

| Key/Command | Description                                                          |
| ----------- | -------------------------------------------------------------------- |
| history n   | Shows the stuff typed – add a number to limit the last n items       |
| Ctrl + r    | Interactively search through previously typed commands               |
| !\[value]   | Execute the last command typed that starts with ‘value’              |
| !\[value]:p | Print to the console the last command typed that starts with ‘value’ |
| !!          | Execute the last command typed                                       |
| !!:p        | Print to the console the last command typed                          |

## File Management

| Key/Command                | Description                                                    |
| -------------------------- | -------------------------------------------------------------- |
| touch \[file]              | Create a new file                                              |
| pwd                        | Full path to working directory                                 |
| .                          | Current folder, e.g. `ls .`                                    |
| ..                         | Parent/enclosing directory, e.g. `ls ..`                       |
| ls -l ..                   | Long listing of parent directory                               |
| cd ../../                  | Move 2 levels up                                               |
| cat                        | Concatenate to screen                                          |
| rm \[file]                 | Remove a file, e.g. `rm data.tmp`                              |
| rm -i \[file]              | Remove with confirmation                                       |
| rm -r \[dir]               | Remove a directory and contents                                |
| rm -f \[file]              | Force removal without confirmation                             |
| cp \[file] \[newfile]      | Copy file to file                                              |
| cp \[file] \[dir]          | Copy file to directory                                         |
| mv \[file] \[new filename] | Move/Rename, e.g. `mv file1.ad /tmp`                           |
| pbcopy < \[file]           | Copies file contents to clipboard                              |
| pbpaste                    | Paste clipboard contents                                       |
| pbpaste > \[file]          | Paste clipboard contents into file, `pbpaste > paste-test.txt` |

## Directory (Folder) Management

| Key/Command            | Description                                               |
| ---------------------- | --------------------------------------------------------- |
| mkdir \[dir]           | Create new directory                                      |
| mkdir -p \[dir]/\[dir] | Create nested directories                                 |
| rmdir \[dir]           | Remove directory ( only operates on empty directories )   |
| rm -R \[dir]           | Remove directory and contents                             |
| less \[file]           | Output file content delivered in screensize chunks        |
| \[command] > \[file]   | Push output to file, keep in mind it will get overwritten |
| \[command] >> \[file]  | Append output to existing file                            |
| \[command] < \[file]   | Tell command to read content from a file                  |

## Search

| Key/Command                            | Description                                                                                   |
| -------------------------------------- | --------------------------------------------------------------------------------------------- |
| find \[dir] -name \[search\_pattern]   | Search for files, e.g. `find /Users -name "file.txt"`                                         |
| grep \[search\_pattern] \[file]        | Search for all lines that contain the pattern, e.g. `grep "Tom" file.txt`                     |
| grep -r \[search\_pattern] \[dir]      | Recursively search in all files in specified directory for all lines that contain the pattern |
| grep -v \[search\_pattern] \[file]     | Search for all lines that do NOT contain the pattern                                          |
| grep -i \[search\_pattern] \[file]     | Search for all lines that contain the case-insensitive pattern                                |
| mdfind \[search\_pattern]              | Spotlight search for files (names, content, other metadata), e.g. `mdfind skateboard`         |
| mdfind -onlyin \[dir] -name \[pattern] | Spotlight search for files named like pattern in the given directory                          |

## Shortcuts

| Key/Command     | Description                                                                             |
| --------------- | --------------------------------------------------------------------------------------- |
| Ctrl + A        | Go to the beginning of the line you are currently typing on.                            |
| Ctrl + E        | Go to the end of the line you are currently typing on.                                  |
| Ctrl + L        | Clears the Screen                                                                       |
| Cmd + K         | Clears the Screen                                                                       |
| Ctrl + U        | Cut everything backwards to beginning of line                                           |
| Ctrl + K        | Cut everything forward to end of line                                                   |
| Ctrl + W        | Cut one word backwards using white space as delimiter                                   |
| Ctrl + Y        | Paste whatever was cut by the last cut command                                          |
| Ctrl + H        | Same as backspace                                                                       |
| Ctrl + C        | Kill whatever you are running. Also clears everything on current line                   |
| Ctrl + D        | Exit the current shell when no process is running, or send EOF to a the running process |
| Ctrl + Z        | Puts whatever you are running into a suspended background process. fg restores it       |
| Ctrl + \_       | Undo the last command. (Underscore. So it's actually Ctrl + Shift + minus)              |
| Ctrl + T        | Swap the last two characters before the cursor                                          |
| Ctrl + F        | Move cursor one character forward                                                       |
| Ctrl + B        | Move cursor one character backward                                                      |
| Option + →      | Move cursor one word forward                                                            |
| Option + ←      | Move cursor one word backward                                                           |
| Esc + T         | Swap the last two words before the cursor                                               |
| Esc + Backspace | Cut one word backwards using none alphabetic characters as delimiters                   |
| Tab             | Auto-complete files and folder names                                                    |

## Help

| Key/Command               | Description                                       |
| ------------------------- | ------------------------------------------------- |
| \[command] -h             | Offers help                                       |
| \[command] --help         | Offers help                                       |
| info \[command]           | Offers help                                       |
| man \[command]            | Show the help manual for \[command]               |
| whatis \[command]         | Gives a one-line description of \[command]        |
| apropos \[search-pattern] | Searches for command with keywords in description |

Misc:

* _**awk**_ - basically a general-purpose scripting language designed mostly used for printing.
* _**sed**_ - 'stream editor' used for file operations like searching, find and replace, insertion or deletion.
* _**lsof**_ - 'list open files' gives the info to find out the files which are opened by which process.
* _**curl**_ - used for transferring data from/to a server designed to work without user interaction
* _**wget**_ - used for downloading files from the web
  * provides a number of options allowing you to download multiple files, resume downloads, limit the bandwidth, recursive downloads, download in the background, mirror a website, and much more
* _**tail**_ - print the last N number of data of the file; by default it prints the last 10 lines.
* _**head**_ - print the first N number of data of the file; by default it prints the first 10 lines.
* _**ssh**_ - 'secure shell' protocol used to securely connect to a remote server/system
  * transfers the data in encrypted form between host and client. SSH runs at TCP/IP port 22
* _**kill**_ - used to terminate processes manually; sends a signal to a process which terminates the process
