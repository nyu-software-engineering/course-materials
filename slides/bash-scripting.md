---
layout: presentation
title: Bash Scripting
permalink: /slides/bash-scripting/
---

class: center, middle

# Bash Scripting

Automate your life.

---

# Agenda

1. [Overview](#overview)
2. [Script File Setup](#script-file-setup)
3. [Built-In Commands](#built-in-commands)
4. [Programming](#programming)
5. [Grouping](#grouping)
6. [Exit codes](#exiting)
7. [Automation](#automation)
8. [Conclusions](#conclusions)

---

name: overview

# Overview

---

template: overview
name: concept

## Concept

`bash` is the most commonly used **shell** for Unix/Linux

---

template: concept
name: concept-1

- a 'shell' is a command line interpreter that allows users to interface with a computer operating system via simple text commands

---

template: concept-1
name: concept-2

- aimed to be a free (as in 'freedom') replacement for UNIX's proprietary Bourne shell, `sh`, originally created at Bell Labs in 1976.

---

template: concept-2
name: concept-3

- 'bash' is an acronym for '**B**ourne-**A**gain **SH**ell'

---

template: concept-3
name: concept-4

- written by Brian Fox in 1989 at the behest of Richard Stallman, founder of the [GNU project](https://en.wikipedia.org/wiki/GNU_Project) that created GNU, the **free software** clone of UNIX we now call Linux

---

template: overview
name: value

## Value

Of what use to us is a 45-year-old set of rudimentary operating system commands?

---

template: value
name: value-1

- knowledge of the command line is assumed of any software developer

---

template: value-1
name: value-2

- many common tasks are accomplished most quickly via simple shell commands

---

template: value-2
name: value-3

- some tasks simply cannot be performed any other way

---

template: value-3
name: value-4

- a shell script can automate away just about any repetitive task required of a developer

---

template: value-4
name: value-5

- automation is one of the increasingly-important foci of the contemporary software engineer

---

template: overview
name: interfaces

## Interfaces

`bash` commands can be run in one of two ways:

---

template: interfaces
name: interfaces-1

- entered idiosyncratically into the **command line**

---

template: interfaces-1
name: interfaces-2

- saved as a script into a **file** (usually given the `.sh` extension) and executed as a batch

---

name: script-file-setup

# Script File Setup

---

template: script-file-setup
name: shebang

## Shebang

The very first two characters in a bash script file must be shebang `#!`

Follow this with the path name to bash, e.g. (your path may differ)

```bash
#!/bin/bash
```

---

template: shebang
name: shebang-1

You can also usually find the location of bash by referring to your machine's environment settings

```bash
#!/usr/bin/env bash
```

---

template: shebang-1
name: shebang-2

Anytime a shebang is used, the kernel will pass the path to the script as the first argument to the script. Yes, scripts can take arguments.

[Try it!](https://repl.it/repls/DeafeningPushyStack)

---

template: script-file-setup
name: file-permissions

## File Permissions

Give yourself execute permissions to run a script file directly:

```bash
chmod u+x file.sh
```

---

template: file-permissions
name: file-permissions-1

Now execute the script:

```bash
./file.sh
```

---

template: file-permissions-1
name: file-permissions-2

If you don't have execute permission, but do have read permission, you can still run the file:

```bash
bash file.sh
```

---

name: built-in-commands

# Built-In Commands

---

template: built-in-commands
name: show-commands

## All commands

Bash comes with a bunch of built-in commands. To show a list of them all:

```bash
enable | cut -d' ' -f 2
```

---

template: built-in-commands
name: show-keywords

## All keywords

There are also a few reserved keywords you can review:

```bash
compgen -k
```

---

template: built-in-commands
name: path-variable

## PATH Variable

bash's PATH variable contains a list of directories where bash will, by default, look for executable programs and shell commands.

Display the contents of PATH:

```bash
echo $PATH
```

---

template: path-variable
name: path-variable-1

Add a directory to the PATH... directories must be separated by colons.

```bash
PATH=$PATH:/Users/foo/Downloads/spyware
```

---

template: built-in-commands
name: time-keeping

## Time-Keeping

The `time` command can be useful to determine how long a process take to complete. It reports:

---

template: time-keeping
name: time-keeping-1

- **real time** - time the process took in regular human minutes / seconds

---

template: time-keeping-1
name: time-keeping-2

- **user time** - amount of time the CPU was used to execute the process

---

template: time-keeping-2
name: time-keeping-3

- **system time** - CPU time used by the kernel in order to run the process (i.e. running a process includes some additional kernel overhead)

---

template: time-keeping-3
name: time-keeping-4

Measure the time taken by the `ls -la` command:

```bash
time ls -la
```

[Try it!](https://repl.it/repls/OrderlyGruesomeMode)

---

template: built-in-commands
name: pipes

## Pipes

Pipes allow the output of one program to serve as input for another.

---

template: pipes
name: pipes-1

List only .txt files in the current working directory:

```bash
ls -l | grep "\.txt$"
```

---

template: pipes-1
name: pipes-2

Swap all vowels in a file listing with 'u'

```bash
ls -l | sed -e "s/[aeio]/u/g"
```

---

template: pipes-2
name: pipes-3

If you really want to be a devops guru, learn the `grep`, `sed`, and `awk` commands in detail - [here's a decent intro](https://www-users.york.ac.uk/~mijp1/teaching/2nd_year_Comp_Lab/guides/grep_awk_sed.pdf).

---

template: built-in-commands
name: output-redirection

## Output redirection

While the system default output is to print to the command line, it is possible to redirect any command's output to a file or other resource.

---

template: output-redirection
name: output-redirection-1

Output the list of files from the previous example to a file named `long_listing.txt`:

```bash
ls -l | grep "\.txt$" > long_listing.txt
```

---

template: output-redirection-1
name: output-redirection-2

Append the word, `flibbertigibbet` to the file named `will-o-the-whisp.txt`

```bash
echo "flibbertigibbet" >> will-o-the-whisp.txt
```

---

template: output-redirection-2
name: output-redirection-3

Ignore a cry for help by redirecting it to the null device: `/dev/null`:

```bash
echo "Help\!\!\!" > /dev/null
```

Note we need to esape the exclamation points, since `!` has [special meaning](https://unix.stackexchange.com/questions/3747/understanding-the-exclamation-mark-in-bash).

---

template: built-in-commands
name: command-subs

## Command substitution

It is possible to use the output of any bash command as data within a bash script.

---

template: command-subs
name: command-subs-1

Place \$() around the command whose output you wish to capture

```bash
# output the text, "Hello world" the hard way
RECIPIENT=$(echo world)
echo Hello $RECIPIENT!
```

[Try it!](https://repl.it/repls/MoccasinDeterminedAngle)

---

name: programming

# Programming controls

---

template: programming
name: variables

## Variables

Variable assignments must not have spaces around the = sign:

```bash
some_variable_name="this is a string"
```

---

template: variables
name: variables-1

Read value of a variable with a \$ in front of variable name

```bash
echo the value of some_variable_name is $some_variable_name
```

---

template: programming
name: aliases

## Aliases

The `alias` command allow you to set other names for common commands.

```bash
alias ll="ls -l"
```

---

template: aliases
name: aliases-1

To execute a command alias, in this case to perform `ls -la`:

```bash
ll
```

---

template: aliases-1
name: aliases-2

See all aliases currently set in the shell session:

```bash
alias
```

---

template: programming
name: conditionals

## Conditionals

bash supports the usual if/else if/else controls, albeit with archaic syntax:

```bash
#!/usr/bin/env bash

T1="foo"
T2="bar"

if [ "$T1" == "$T2" ]; then
    echo expression evaluated as true
else
    echo expression evaluated as false, obviously
fi
```

[Try it!](https://repl.it/repls/FluffySparklingLightweightprocess)

---

template: programming
name: loops

## Loops

bash supports both `for` and `while` loops:

For:

```bash
#!/usr/bin/env bash

for i in {1..5}; do
  echo $i
done
```

---

template: loops
name: loops-1

While:

```bash
#!/usr/bin/env bash

COUNTER=0

# note the archaic syntax for the less than operator
while [  $COUNTER -lt 10 ]; do
	echo The counter is $COUNTER
	let COUNTER=$COUNTER+1
done
```

---

template: programming
name: loops-continued

## Loops (continued)

It is also possible to loop through lines of output from another command using command substitution:

```bash
for i in $( ls ); do
    echo ... $i ...
done
```

---

template: loops-continued
name: loops-continued-1

```bash
while IFS= read -r line; do
    echo "... $line ..."
done <<< $(ls)
```

[Try it!](https://repl.it/repls/MoccasinDeterminedAngle)

---

template: programming
name: functions

## Functions

A function with a local variable:

```bash
#!/usr/bin/env bash
HELLO=Hello
function hello {
        local HELLO=World
        echo $HELLO
}
echo $HELLO
hello
echo $HELLO
```

---

template: functions
name: functions-1

A function with an argument:

```bash
#!/usr/bin/env bash
function e {
    echo $1
}
e Hello
e World
```

---

template: programming
name: exports

## Exports

A copy of a variable defined within a script can be copied into your command-line environment, which makes it available to any other scripts you run

```bash
export some_variable_name
```

---

template: exports
name: exports-1

Functions can also be exported

```bash
export -f some_function_name
```

---

template: exports-1
name: exports-2

Print what has been exported to the command-line:

```bash
export
```

---

name: exiting

# Exit codes

---

template: exiting
name: exiting-1

## Concept

Bash scripts _can_ and _should_ pass exist codes to their parent processes when they complete.

---

template: exiting-1
name: exiting-1a

- An exit code informs the parent process of the success or failure of the command, so appropriate follow-up actions can be taken automatically.

---

template: exiting-1a
name: exiting-1b

- An exit code of `0` indicates success, and `1` or indicates failure (there are other [more specific failure codes](http://www.tldp.org/LDP/abs/html/exitcodes.html) as well)

---

template: exiting-1b
name: exiting-1c

- The exit code of the last bash command that was run is available in the built-in `$?` variable.

---

template: exiting-1c
name: exiting-1d

- This allows chaining of commands.

---

template: exiting
name: exiting-2

## The \$? variable

Here we, for example, attempt to move a file and indicate whether it was a success or not, by checking the value in the `$?` variable.

```bash
#!/usr/bin/env bash

# attempt to move a file, for example...
mv foo.txt /foo/bar/baz.txt

# check whether it worked.
if [ $? -eq 0 ]
then
  echo "Successfully moved file"
  # we could do any relevant follow-up actions here
else
  echo "Could not move file"
  # we could do any relevant follow-up actions here
fi
```

---

template: exiting
name: exiting-3

## Command chaining

Commands can be chained together using boolean logic operators.

```bash
npm run lint && npm run test-unit && npm run test-casper-runner
```

---

template: exiting-3
name: exiting-3a

- With AND (&&) logic, as long as each command exits with success, the following command will be executed.

---

template: exiting-3a
name: exiting-3b

- If any command in the chain exits with a failure code, the subsequent commands will not be executed.

---

template: exiting
name: exiting-4

## Command chaining (continued)

Or (||) logic can also be useful in command chaining.

```bash
./tmp.sh && echo "bam" || (sudo ./tmp.sh && echo "bam" || echo "fail")
```

---

template: exiting-4
name: exiting-4a

- In this example, if we are able to successfully execute the script, `./tmp.sh`, the message "bam" will be output.

---

template: exiting-4a
name: exiting-4b

- If that command fails, however, we will try to run the same command as a `sudo` super-user, and output "bam" if that works.

---

template: exiting-4b
name: exiting-4c

- If that also fails, we output the text, "fail"

---

template: exiting
name: exiting-5

## Custom exit codes

You can, of course, specify exit codes at relevant places in your own bash scripts using the `exit` keyword.

```bash
#!/usr/bin/env bash

# attempt to move a file, for example...
mv foo.txt /foo/bar/baz.txt

# check whether it worked.
if [ $? -eq 0 ]
then
  echo "Successfully moved file"
  # we could do any relevant follow-up actions here
  exit 0
else
  echo "Could not move file"
  # we could do any relevant follow-up actions here
  exit 1
fi
```

---

name: grouping

# Grouping

---

template: grouping
name: parentheses

## Parentheses

---

template: grouping
name: parentheses

## Parentheses

Commands grouped within parentheses are separate processes. Variables defined within the sub-process are not shared with the parent process.

```bash
a=1
(
a=2
)
echo $a
# prints 1
```

---

template: grouping
name: braces

## Braces

Commands grouped with braces do not spawn a sub-process, so variables therein are shared:

```bash
a=1
{
a=2
}
echo $a
# prints 2
```

---

name: automation

# Automation

---

template: automation
name: startup-scripts

## Startup Scripts

Bash is used for everyday automation by developers:

---

template: startup-scripts
name: startup-scripts-1

- Every time a user logs into a user logs in, a bash script named `.bash_profile` is automatically run.

---

template: startup-scripts-1
name: startup-scripts-2

- Every time a new command shell is started, a script named `.bashrc` is automatically run.

---

template: startup-scripts-2
name: startup-scripts-3

Place whatever bash commands you want in files by either of these names in your user account home directory in order to take advantage of this feature.

---

template: automation
name: aliases-file

## Aliases File

Many developers use bash aliases for common commands.

---

template: aliases-file
name: aliases-file-1

For good housekeeping, store many aliases, if you have them, in a `~/.bash_aliases` file and load them automatically in your `.bashrc` script every time a shell session starts.

---

template: aliases-file-1
name: aliases-file-2

Example `.bashrc` script to check whether such an aliases file exists and execute it, if so:

```bash
if [ -f ~/.bash_aliases ]; then
. ~/.bash_aliases
fi
```

---

template: automation
name: software-dev-automation

## Software Development Automation

Contemporary software developers depend upon automation to simplify and speed up many pedestrian tasks.

---

template: software-dev-automation
name: software-dev-automation-1

- For example, in **continuous integration**, unit tests that automatically validate that the code behaves as expected are automatically executed anytime the codebase in version control is modified.

---

template: software-dev-automation-1
name: software-dev-automation-2

- Similarly, in a practice known as **continuous deployment**, copy files from a version control repository to a live server allow software to be made available to its end-users as soon as changes are committed.

---

template: software-dev-automation-2
name: software-dev-automation-3

- NPM-based projects, including React.js and Express.js, usually include bash scripts in the `scripts` section of the `package.json` settings file that handle common command-line tasks.

---

template: automation
name: software-dev-automation-3

## Continuous integration example

A fragment a script that could be used in [Jenkins](https://jenkins.io/), a popular automation tool, to execute some follow-up actions anytime a change is committed to particular branches of a version control repository:

```bash
#!/usr/bin/env bash

if [[ $BRANCH_NAME == "master" ]] || [[ $BRANCH_NAME == "master_dev" ]]
then
    ./runUnitTests.sh $REPOSITORY_NAME $BASE_BUILD_CORE $BRANCH_NAME $BUILD_NUMBER || echo "The npm may fail but the report exists"
fi
```

---

template: software-dev-automation-3
name: software-dev-automation-4

Jenkin automatically sets up variables named `BRANCH_NAME`, `REPOSITORY_NAME`, etc and this custom code uses those to decide whether to run an automated testing script.

---

template: automation
name: software-dev-automation-5

## Continuous deployment example

[Travis CI](https://travis-ci.com/), another popular automation tool, can run any arbitrary bash script when the changes are committed to the codebase.

```yaml
deploy:
  provider: script
  script: bash scripts/deploy.sh
  on:
    branch: master
```

---

template: software-dev-automation-5
name: software-dev-automation-6

In this case, we see the contents of a [YAML](https://en.wikipedia.org/wiki/YAML) settings file named `.travis.yml` that would be placed in the version control repository. This file informs Travis CI to execute a script named `deploy.sh` anytime new code is pushed to the `master` branch. Typically, such a file would log into a remote server via `ssh`, copy the contents of the repository to the server, build the code, and execute it.

---

template: automation
name: software-dev-automation-7

## NPM script example

All Node.js projects using the Node Package Manager (NPM) contain a `package.json` file that can define a set of labeled bash scripts with names.

```javascript
"scripts": {
    "start": "node server.js",
    "start-dev": "nodemon ./server.js",
    "test-unit": "mocha ./test/unit --exit",
    "test": "npm run lint && npm run test-unit && npm run test-casper-runner",
    "lint": "eslint .",
    "codecov": "npm run test && (codecov || true)",
    "autofix": "eslint --fix .",
    "validate": "npm ls"
  }
```

---

template: software-dev-automation-7
name: software-dev-automation-8

Such scripts can then be easily executed from the command line by referring to their labels.

```bash
npm run test
```

---

template: automation
name: education-automation

## Education automation

Your professor may even use bash scripts to automatically parse git logs to gauge the level of code activity of each student.

- Such statistics do not show the **quality** of the contributions, which must be reviewed in other ways.

```bash
# loop through each contributor
git log --format='%aN' | sort -u | while read user
do
	# show each contributor's stats
    printf '%-25s' "- $user -"
    echo -n $(git log --shortstat --author="$user" --after="$AFTER_DATE" --before="$BEFORE_DATE" | grep -E "Merge" | awk '{merges+=1} END {printf "merges: %03d | ", merges}')
    echo -n $(git log --shortstat --author="$user" --after="$AFTER_DATE" --before="$BEFORE_DATE" | grep -E "fil(e|es) changed" | awk '{commits+=1; files+=$1; inserted+=$4; deleted+=$6} END {printf " commits: %05d | additions: %05d | deletions: %05d | files: %05d", commits, inserted, deleted, files }')
    echo ""
done
```

[Fork it and try it!](https://github.com/bloombar/git-developer-contribution-analysis)

---

name: conclusions

# Conclusions

---

# Conclusions

You are now a beginner bash programmer.

- Thank you. Bye.
