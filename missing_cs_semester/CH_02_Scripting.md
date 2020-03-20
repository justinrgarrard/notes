---
layout: page
---

# CH 2 | Shell Tools and Scripting

### Shell Scripting
* Control Flow (loops, variables, functions)
```bash
#!/bin/bash

echo "Starting program at $(date)" # Date will be substituted

echo "Running program $0 with $# arguments with pid $$"

for file in $@; do
	grep foobar $file > /dev/null 2> /dev/null
	# When pattern is not found, grep has exit status 1
	# We redirect STDOUT and STDERR to a null register since we do not care about them
	if [[ $? -ne 0 ]]; then
		echo "File $file does not have any foobar, adding one"
		echo "# foobar" >> "$file"
	fi
done
```
* Single-quote strings are literal, double-quote strings permit variable substitution
```bash
foo=bar
echo "$foo"
# prints bar
echo '$foo'
# prints $foo
```

* Built-in Variables
```
$0 - Name of the script
$1 to $9 - Arguments to the script. $1 is the first argument and so on.
$@ - All the arguments
$# - Number of arguments
$? - Return code of the previous command
$$ - Process Identification number for the current script
!! - Entire last command, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions, then you can quickly execute it with sudo by doing sudo !!
$_ - Last argument from the last command. If you are in an interactive shell, you can also quickly get this value by typing Esc followed by .
```

* Error handling with exit codes
```bash
false || echo "Oops, fail"
# Oops, fail

true || echo "Will not be printed"
#

true && echo "Things went well"
# Things went well

false && echo "Will not be printed"
#

false ; echo "This will always run"
# This will always run
```

* Shell globbing for wildcards
```bash
convert image.{png,jpg}
# Will expand to
convert image.png image.jpg

cp /path/to/project/{foo,bar,baz}.sh /newpath
# Will expand to
cp /path/to/project/foo.sh /path/to/project/bar.sh /path/to/project/baz.sh /newpath

# Globbing techniques can also be combined
mv *{.py,.sh} folder
# Will move all *.py and *.sh files


mkdir foo bar
# This creates files foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h
touch {foo,bar}/{a..j}
touch foo/x bar/y
# Show differences between files in foo and bar
diff <(ls foo) <(ls bar)
# Outputs
# < x
# ---
# > y
```

* Use [shellcheck](https://github.com/koalaman/shellcheck) to check Bash syntax

* Use [TLDR Pages](https://tldr.sh/) for simple command usage lookups

### Shell Tools
* Use `find` and `fd` to figure out where files are located
```bash
# Find all directories named src
find . -name src -type d
# Find all python files that have a folder named test in their path
find . -path '**/test/**/*.py' -type f
# Find all files modified in the last day
find . -mtime -1
# Find all zip files with size in range 500k to 10M
find . -size +500k -size -10M -name '*.tar.gz'

# Delete all files with .tmp extension
find . -name '*.tmp' -exec rm {} \;
# Find all PNG files and convert them to JPG
find . -name '*.png' -exec convert {} {.}.jpg \;
```

* Use `grep` or `rg` to find the contents of files

* Use `history` or CTRL+R to find previously run Bash commands

* Use `ln -s` or `z` to bookmark common directories

* Use `tree` or `broot` to look over large directories

* Use `nnn` or `ranger` for a full file manager solution