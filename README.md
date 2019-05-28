# Linux_command
[Man-pages search for the command](http://man7.org/linux/man-pages/man1/find.1.html)

[Linux tutorial](https://ryanstutorials.net/linuxtutorial/commandline.php)

[bash reference manual](http://tiswww.case.edu/php/chet/bash/bashref.html#SEC31)

[bash_reference Manual](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameter-Expansion)

## Compare two files for matching lines and store positive results

```
File 1:
A0001  C001
B0003  C896
A0024  C234
.
B1542  C231
.
upto 28412 such lines
```
File 2:
```
A0001
A0024
B1542
.
.
and 12000 such lines.
```

Use awk:
```
$ awk 'FNR==NR{a[$1];next}($1 in a){print}' file2 file1
A0001   C001
A0024   C234
B1542   C231
```
Or
```
grep -Ff File2 File1
```
The -f File2 reads the patterns from File2 and the -F treats the patterns as fixed strings (ie no regexes used).




## Use SCP Command to Securely Transfer Files
SCP (secure copy) is a command line utility that allows you to securely copy files and directories between two locations.

With scp, you can copy a file or directory:
```
From your local system to a remote system.
From a remote system to your local system.
Between two remote systems from your local system.
```
The scp utility expressions take the following form:
```
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```
## Link
Create a hard link to the file public_html/myfile1.txt in the current directory.
```
ln public_html/myfile1.txt
```
Create a symbolic link to the file public_html/myfile1.txt in the current directory.
```
ln -s public_html/myfile1.txt
```
Create a symbolic link to the directory public_html named webstuff.
```
ln -s public_html/ webstuff
```
You can use rm to delete the symlink.
Example:
```
-rw-rw-r-- 1 2014-01-02 09:21 tmo
lrwxrwxrwx 1 2014-01-02 09:21 tmo2 -> tmo
```
Then ...
```
rm tmo2
```
will remove the symlink.

## Copy first n files into another folder
```
find . -maxdepth 1 -type f |head -1000|xargs cp -t "$destdir"
```
copy
Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY
```
cp [OPTION]... [-T] SOURCE DEST
cp [OPTION]... SOURCE... DIRECTORY
cp [OPTION]... -t DIRECTORY SOURCE...
```
```
-t, --target-directory=DIRECTORY
              copy all SOURCE arguments into DIRECTORY
```
```
cp test/  new-test                # copy files under the test folder to the new folder
cp test  new-test                 # copy the test folder to the new folder.
cp a.txt b.txt
```
### Copying multiple files to a directory
Or, perhaps you want to copy multiple files into another directory. To accomplish this, you can specify multiple files as the source, and a directory name as the destination
```
cp ~/pictures/picture-*.jpg        ~/picture-backup
```
### Copying files recursively
You can use cp to copy entire directory structures from one place to another using the -R option to perform a recursive copy. Let's say you are the user steve and you have a directory, /home/steve/files, which contains many files and subdirectories. You want to copy all those files, and all the subdirectories (and the files and subdirectories they contain), to a new location, /home/steve/files-backup. You can copy all of them using the command:

```
cp -R ~/files ~/files-backup
```
### Creating symbolic links instead of copying data

Another useful trick is to use cp to create symbolic links to your source files. You may already be familiar with using the ln command to create symlinks; cp is a great way to create multiple symlinks all at once.

cp will create symbolic links if you specify the -s option. So, for instance,
```
cp -s file.txt file2.txt
```
This will work with a recursive copy, as well. So the command:
```
cp -R -s ~/myfiles ~/myfiles2
```
### Copy a file into another directory, and give it a new name
Creates a copy of the file in the working directory named origfile. The copy will be named newfile, and will be located in the directory /directory/subdirectory.
```
cp origfile /directory/subdirectory/newfile
```

## File numbers
This should work:
```
find DIR_NAME -type f | wc -l
```
Explanation:
```
-type f                   # to include only files.
| (and not ¦)             # redirects find command's standard output 
                            to wc command's standard input.
wc                        # (short for word count) counts newlines, 
                            words and bytes on its input (docs).
-l                        # to count just newlines.
```

## HowTo: Check If a Directory Exists In a Shell Script
```
[ -d "/path/to/dir" ] && echo "Directory /path/to/dir exists."
[ ! -d "/path/to/dir" ] && echo "Directory /path/to/dir DOES NOT exists."

[ -d "/path/to/dir" ] && echo "Directory /path/to/dir exists." || 
echo "Error: Directory /path/to/dir does not exists."
```
```
if [ -d "/path/to/dir" ] 
then
    echo "Directory /path/to/dir exists." 
else
    echo "Error: Directory /path/to/dir does not exists."
fi
```




## Xargs and find
This manual page documents the GNU version of xargs.  xargs reads
       items from the standard input, delimited by blanks (which can be
       protected with double or single quotes or a backslash) or newlines,
       and executes the command (default is /bin/echo) one or more times
       with any initial-arguments followed by items read from standard
       input.  Blank lines on the standard input are ignored.
```
xargs [options] [command [initial-arguments]]
```
The specified command will be invoked as many times as necessary to use up the list of input items. Some commands can usefully be executed in parallel too; see the -P option


### find
find - search for files in a directory hierarchy
```
find [-H] [-L] [-P] [-D debugopts] [-Olevel] [starting-point...]
       [expression]
```
This manual page documents the GNU version of find.  GNU find
       searches the directory tree rooted at each given starting-point by
       evaluating the given expression from left to right, according to the
       rules of precedence (see section OPERATORS), until the outcome is
       known (the left hand side is false for and operations, true for or),
       at which point find moves on to the next file name.  If no starting-
       point is specified, `.' is assumed.






## Extract files
```
tar xzf file.tar.gz          # to uncompress a gzip tar file (.tgz or .tar.gz)
tar xjf file.tar.bz2         # to uncompress a bzip2 tar file (.tbz or .tar.bz2) to extract the contents.
tar xf file.tar              # to uncompressed tar file (.tar)
tar xC /var/tmp -f file.tar  # to uncompress tar file (.tar) to another directory
```
```
x = eXtract, this indicated an extraction c = create to create )
v = verbose (optional) the files with relative locations will be displayed.
z = gzip-ped; j = bzip2-zipped
f = from/to file ... (what is next after the f is the archive file)
C = directory. In c and r mode, this changes the directory 
before adding the following files. In x mode, changes directoriy after 
opening the archive but before extracting entries from the archive.
```
The files will be extracted in the current folder (most of the times in a folder with the name 'file-1.0').

## magic colon

Bash and sh both use colons (":") in more than one context. 
You'll see it used as 
```
a separator ($PATH, for example),
a modifier (${n:="foo"})
a null operator ("while :")
```
## Shell parameter expansion
```
${parameter%word}
${parameter%%word}
```
The word is expanded to produce a pattern and matched according to the rules described below (see Pattern Matching). If the pattern matches If the pattern matches a trailing portion of the expanded value of parameter, then the result of the expansion is the value of parameter with the shortest matching pattern (the ‘%’ case) or the longest matching pattern (the ‘%%’ case) deleted. If parameter is ‘@’ or ‘*’, the pattern removal operation is applied to each positional parameter in turn, and the expansion is the resultant list. If parameter is an array variable subscripted with ‘@’ or ‘*’, the pattern removal operation is applied to each member of the array in turn, and the expansion is the resultant list.

## If and for statements

### if statements
the basic structure of the if statement looks like this

```
if [ conditional-expression ]                          # the condition is inside the brackets; there MUST 
                                                         have a SPACE between the
                                                         the condition and bracket
then       
  commands                                             # if true, the commands following 
                                                         the then statement are executed
else
  other-commands
fi                                                     # the fi(backward) marks the end of the if block
```

```
#!/bin/bash 
echo “How old are you?” 
read age 
if [ “$age” -ge 21 ] ; then 
echo “You are old enough. Welcome!” 
else 
echo “Sorry, you are not allowed to be here, you are too young!” 
fi

```
### for statement
1) In this form the for statement executes the commands enclosed in a body, once for each item in the list.
```
for varname in list
do
       command1
       command2
       ..
done
```
Caution: 
The list option contains list of values. The list can be a variable that contain several words sperated by spaces(a b c), but not comma (a, b, c). Otherwise, the comma will be treated as part of the value, instead of"mon", it will use "Mon,"

2) The list of values should not be enclosed in a double quote, otherwise it will be treated as a single value.
```
for (( expr1; expr2; expr3 ))    # initialization, condition, updation
do
       command1
       command2
       ..
done
```
In the above bash for command syntax
```
expr1        # it is evaluated before the first iteration, initialize the variables for the loop
expr2        # all the commands between the do and the done is executed repeatly until the value of expr2 is True
expr3        # it is evaluated after each iteration. This is usually used to increment a loop counter.
```
3) Don't specify the list; get it from the postional parameters.
```
$ cat for3.sh
i=1
for day
do
 echo "Weekday $((i++)) : $day"
done

$ ./for3.sh Mon Tue Wed Thu Fri
Weekday 1 : Mon
Weekday 2 : Tue
Weekday 3 : Wed
Weekday 4 : Thu
Weekday 5 : Fri
```
4) Unix command output as list values after “in” keyword
The list is enclosed by the back-tick \`\` as shown below.
```
$ cat for4.sh
i=1
for username in `awk -F: '{print $1}' /etc/passwd`
do
 echo "Username $((i++)) : $username"
done

$ ./for4.sh
Username 1 : ramesh
Username 2 : john
Username 3 : preeti
Username 4 : jason
..
```

5) Loop through files and directories in a for loop

6) Break out of the for loop - break command
```
$ cat for6.sh
i=1
for day in Mon Tue Wed Thu Fri
do
 echo "Weekday $((i++)) : $day"
 if [ $i -eq 3 ]; then
   break;
 fi
done

$ ./for6.sh
Weekday 1 : Mon
Weekday 2 : Tue
```
7) Continue from the top of the for loop

Under certain conditions, you can ignore the rest of the commands in the for loop, 
and continue the loop from the top again 
```
$ cat for7.sh
i=1
for day in Mon Tue Wed Thu Fri Sat Sun
do
 echo -n "Day $((i++)) : $day"
 if [ $i -eq 7 -o $i -eq 8 ]; then
   echo " (WEEKEND)"
   continue;
 fi
 echo " (weekday)"
done

$ ./for7.sh
Day 1 : Mon (weekday)
Day 2 : Tue (weekday)
Day 3 : Wed (weekday)
Day 4 : Thu (weekday)
Day 5 : Fri (weekday)
Day 6 : Sat (WEEKEND)
Day 7 : Sun (WEEKEND)
```
8) Bash for loop using C program syntax 

9) Infinite Bash for loop

When you don’t provide the start, condition, and increment in the bash C-style for loop, it will become infinite loop. You need to press Ctrl-C to stop the loop.
```
for (( ; ; ))
```

10) Range of numbers after “in” keyword
```
for num in {1..10}
```
11) range of numbers with increments after in keyword
```
for num in {1..10..2}
```


## check free disk
```
df                   # disk free; shows available and used disk space
-h                   # show the disk space in human-readable format
-a                   # show complete disk
```
```
du                   # shows the disk usage of files, folders, etc
-a                   # all
-s                   # specific file or directory
```
```
ls -al
```
```
stat  <file/folder>   # display the size and other status 
```
```
fdisk -l              # shows disk size along with disk partitioning information
```


-------------------------------------------------------------------------------------------------------------------------------

## Realpath and readlink
Both realpath and readlink commands display resolved path for symlinks in the output.
```
realpath [OPTION]... FILE...                    # the resolved absolute file name
readlink [OPTION]... FILE..                     # print resolved symbolic links or canonical file names
```

```
readlink:
-f, --canonicalize
      canonicalize  by  following  every symlink in every component of
      the given name recursively; all  but  the  last  component  must
      exist

-e, --canonicalize-existing
   canonicalize  by  following  every symlink in every component of
   the given name recursively, all components must exist

-m, --canonicalize-missing
   canonicalize by following every symlink in  every  component  of
   the  given  name recursively, without requirements on components
   existence
```


---------------------------------------------------------------------------------------------------------------------------------------

## [Read and Set Environmental and shell variables](https://www.digitalocean.com/community/tutorials/how-to-read-and-set-environmental-and-shell-variables-on-a-linux-vps)


### Set, env and export
set or unset values of shell options and positional parameters
```
set [--abefhkmnptuvxBCHP] [-o option-name] [arg ...]
```
Change the value of shell attributes and positional parameters or display the names and values of shell variable
```
set -e                   # Exit immediately if a command exits with a non-zero status.
set -o pipefail          # Pipelines fail on the first command which fails instead of dying later on down the pipeline. 
                           This is especially good when cmd3 is a command that always succeeds (like echo):
                           cmd1 | cmd2 | cmd3
set -x                   # print each command to the stderr before running it.
```
```
(set -euxo pipefail; echo hi ;non-existent-command; echo bye)
hi
non-exist: command not found
```
```
(%set -euxo pipefail; echo hi ;non-existent-command; echo bye)
hi
non-exist: command not found
bye
```
```
cmd1 && cmd2 && cmd3 
```
is equivalent to
```
set -e
cmd1
cmd2
cmd3
```





### Special parameters
These parameters may only be referenced; assignment to them is not allowed.
```
$0            # The name of the script.
$1 - $9       # Any command line arguments given to the script.
                $1 is the first argument, $2 the second and so on.
$#            # How many command line arguments were given to the script.
$*            # All of the command line arguments.
$@
$?            # Expands to the exit status of the most recently executed foreground pipeline.
$-
$$            # Expands to the process ID of the shell
$!        
$_
env or printenv            # show env variables
set | less                 # all the variables, shell and env
VAR='a'                    # set a variable
$VAR or ${VAR}             # refer a variable
$(command)                 # command substitution
export var                 # set env var
unset                      # degrade var
```
An example is as follows:
```
# touch variable
# vi variable
#!/bin/sh
echo "number:$#"
echo "scname:$0"
echo "first :$1"
echo "second:$2"
echo "argume:$@"
echo "show parm list:$*"
echo "show process id:$$"
echo "show precomm stat: $?"
# chmod +x variable
```
Output results are :
```
# ./variable aa bb 
number:2
scname:./variable                  # path+filename
first:aa                           # first positional value
second:bb
argume:aa bb                       # positional value
show parm list:aa bb               # all params include keyvalue
show process id:24544
show precomm stat:0
```

The shell keeps track of all of these settings and details is through an area it maintains called the environment. 
```
Environmental variables                        # inherited by any child shells or processes.
Shell variables                                # the current working directory
```
We can see a list of all of our environmental variables by using commands
```
env or printenv 
export
```
we will get a list of all shell variables, environmental variables, local variables, and shell functions
```
set | less
```
### Creating Shell Variables
```
TEST_VAR='Hello World!'
set | TEST_VAR                       # We can see this by grepping for our new variable 
                                            within the set output
```
- When we set a variable, its name followed directly by an equals sign(=)
- When we refer a variable, we must place a dollar sign ($) before the variable name
```
$ varaible_name or ${variable_name}
```
As you can see, reference the value of a variable by preceding it with a $ sign. 
The shell takes this to mean that it should substitute the value of the variable when it comes across this.
There is another point to note, you can use the following sentence to assign value
```
var = $(command)
```
The echo demonstrate a way of accessing the value of any shell or environmental variable.
```
echo $TEST_VAR
```

We can spawn a new bash shell from within our current one to demonstrate:
```
bash
echo $TEST_VAR
```
Get back to our original shell by typing 
```
exit
echo $TEST_VAR        # reference again
```

### Creating Environmental Variables
Now, let's turn our shell variable into an environmental variable. We can do this by exporting the variable. 
The command to do so is appropriately named:
```
export TEST_VAR               # This will change our variable into an environmental variable
```
```
printenv | grep TEST_VAR     
```
We can set environmental variables in a single step like this
```
export NEW_VAR="Testing export"
printenv | grep NEW_VAR                  # output
exit
echo $NEW_VAR                            # nothing is returned
```
This is because environmental variables are only passed to child processes. 
There isn't a built-in way of setting environmental variables of the parent shell. 
This is good in most cases and prevents programs from affecting the operating environment from which they were called.
The NEW_VAR variable was set as an environmental variable in our child shell. 
This variable would be available to itself and any of its child shells and processes. 
When we exited back into our main shell, that environment was destroyed.

```
echo $PATH               
printf "%s\n" $PATH
```
Modify current PATH

In general, the export command marks an environment variable to be exported with any newly forked child processes 
and thus it allows a child process to inherit all marked variables.
```
$ export
```
```
declare -x MAIL="/var/mail/zhengnianzu"
declare -x NODE_HOME="/mnt/sdb/dengliqun/node-v9.0.0-rc.0-linux-x64"
declare -x NODE_PATH="/mnt/sdb/dengliqun/node-v9.0.0-rc.0-linux-x64/lib/node_modules"
declare -x OLDPWD="/home/zhengnianzu"
```
```
export | grep http_proxy
declare -x http_proxy="http://root:huawei@10.61.34.138:3128"
```

You can assign value before exporting using the following syntax
```
export VAR=value                  # VAR=value; export VAR     
```
```
PATH=$PATH:~/opt/bin
PATH=~/opt/bin:$PATH
```
depending on whether you want to add ~/opt/bin at the end (to be searched after all other directories, 
in case there is a program by the same name in multiple directories) or 
at the beginning (to be searched before all other directories).

### Demoting and Unsetting Variables 
We still have our TEST_VAR variable defined as an environmental variable.
We can change it back into a shell variable by typing:
```
export -n TEST_VAR
```
```
printenv | grep TEST_VAR
set | grep TEST_VAR
```

If we want to completely unset a variable, either shell or environmental, we can do so with the unset command
```
unset TEST_VAR
echo $TEST_VAR           # Nothing is returned because the variable has been unset.
```
### Setting Environmental Variables at Login



---------------------------------------------------------------------------------------------------------------------------------

## Find out if file exists with conditional expression
he general syntax is as follows:
```
[ parameter FILE ]
```
OR
```
test parameter FILE
```
OR
```
[[ parameter FILE ]]
```
Where parameter can be any one of the following:
```
-e: Returns true value if file exists.
-f: Return true value if file exists and regular file.
-r: Return true value if file exists and is readable.
-w: Return true value if file exists and is writable.
-x: Return true value if file exists and is executable.
-d: Return true value if exists and is a directory.
```
Examples are as follow
```
$ [ -f /etc/passwd ] && echo "File exist" || echo "File does not exist"
$ [ -f /tmp/fileonetwo ] && echo "File exist" || echo "File does not exist"
```
```
$ [ -d /var/logs ] && echo "Directory exist" || echo "Directory does not exist"
$ [ -d /dumper/fack ] && echo "Directory exist" || echo "Directory does not exist"
```
### test
Checks file types and compares values.


test exits with the status determined by EXPRESSION. Placing the EXPRESSION between square brackets (\[ and \]) is the same as testing the EXPRESSION with test. 

```
test 100 -gt 99 && echo "Yes, that's true." || echo "No, that's false."
```
To see the exit status at the command prompt, echo the value "$?" A value of 0 means the expression evaluated as true, and a value of 1 means the expression evaluated as false.
```
[ "awesome" = "awesome" ]; echo $?
```

---------------------------------------------------------------------------------------------------------------------------------
## Change permission for a folder

The other answers are correct, in that chmod -R 755 will set these permissions to all files and subfolders in the tree. But why on earth would you want to? It might make sense for the directories, but why set the execute bit on all the files?

I suspect what you really want to do is set the directories to 755 and either leave the files alone or set them to 644. For this, you can use the find command. For example:

To change all the directories to 755 (drwxr-xr-x):
```
find /opt/lampp/htdocs -type d -exec chmod 755 {} \;
```
To change all the files to 644 (-rw-r--r--):
```
find /opt/lampp/htdocs -type f -exec chmod 644 {} \;
```
## Find Linux Files by Name or Extension
```
-O1           (Default) filter based on file name first.
-O2           File name first, then file-type.
-O3           Allow find to automatically re-order the search based on efficient use of resources and likelihood. of success
-maxdepth X   Search current directory as well as all sub-directories X levels deep.
-iname        Search without regard for text case.
-not          Return only results that do not match the test case.
-type f       Search for files.
-type d       Search for directories.
```


Use Grep to Find Files Based on Content
```
find . -name testfile.txt        # Find a file called testfile.txt in current and sub-directories.
find /home -name *.jpg           # Find all .jpg files in the /home and sub-directories.
find . -type f -empty            #Find an empty file within the current directory.
find /home -user exampleuser -mtime 7 -iname ".db"     
                                 # Find all .db files (ignoring text case) modified in the last 7 days 
                                   by a user named exampleuser.                                                        
```
```
find . -type f -exec grep "example" '{}' \; -print     
```
```
find . -type f -print | xargs grep "example"
```
This searches every object in the current directory hierarchy (.) that is a file (-type f) and then runs the command grep "example" for every file that satisfies the conditions. The files that match are printed on the screen (-print). The curly braces ({}) are a placeholder for the find match results. The {} are enclosed in single quotes (') to avoid handing grep a malformed file name. The -exec command is terminated with a semicolon (;), which should be escaped (\;) to avoid interpretation by the shell.

```
find . -name "rc.conf" -exec chmod o+r '{}' \;
```
This filters every object in the current hierarchy (.) for files named rc.conf and runs the chmod o+r command to modify file permissions of the find results.

```
find . -name "*.bak" -delete    # find will delete all files that end with the characters .bak:
```


---------------------------------------------------------------------------------------------------------------------------------
## [Shell functions library](https://bash.cyberciti.biz/guide/Shell_functions_library#How_do_I_load_myfunctions.sh_into_the_script.3F)
```
declare             # variables
function            # define functions
```
-------------------------------------------------------------------------------------------------------------------------------


## Source: Executes the content of the file passed as argument

source is a bash shell built-in command that executes the content of the file passed as argument, 
in the current shell. It has a synonym in . (period).\
```
. filename [arguments]
source filename [arguments]
```
Be careful! ./ and source are not quite the same.
```
./script runs the script as an executable file, launching a new shell to run it
source script reads and executes commands from filename in the current shell environment
```
Note: 
```
./script is not . script, but . script == source script
```
The sourced file can be:
```
script.sh
#! /bin/sh
var1="hello the world"              # classical variable defination 
```
Then use source to export variables to shell environment
```
source  script.sh
```


---------------------------------------------------------------------------------------------------------------------------------
## Group a function call
If your $VARIABLE is a string containing spaces or other special characters, and single square brackets are used (which is a shortcut for the test command), 
then the string may be split out into multiple words. Each of these is treated as a separate argument.

So that one variable is split out into many arguments:
```
VARIABLE= "foo bar oni" ;  
# returns "hello world"

if [ $VARIABLE == 0 ]; then            # that is, foo bar oni = 0 
  # fails as if you wrote:
  # if [ hello world == 0 ]
fi 
```
Easy Fix

Wrap the variable output in double quotes, forcing it to stay as one string (therefore one argument). For example,
```
VARIABLE="foo bar oni";
if [ "$VARIABLE" == 0 ]; then
  # some action
fi 
```
Or, an alternate fix is to use double square brackets (which is a shortcut for the new test command)
```
VARIABLE="foo bar oni";
if [[ $VARIABLE == 0 ]]; then
  # some action
fi 
```

NOTE that:

== is a bash-specific alias for =, which performs a string (lexical) 

comparison instead of the -eq numeric comparison. (It's backwards from Perl: the word-style operators are numeric, the symbolic ones lexical.)



--------------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------------
##  Double or single brackets, parentheses, curly braces
Brackets
```
if [ CONDITION ]    Test construct  
if [[ CONDITION ]]  Extended test construct  
Array[1]=element1   Array initialization  
[a-z]               Range of characters within a Regular Expression
$[ expression ]     A non-standard & obsolete version of $(( expression )) [1]
[1] http://wiki.bash-hackers.org/scripting/obsolete
```
Curly Braces
```
${variable}                             Parameter substitution  
${!variable}                            Indirect variable reference  
{ command1; command2; . . . commandN; } Block of code  
{string1,string2,string3,...}           Brace expansion  
{a..z}                                  Extended brace expansion  
{}                                      Text replacement, after find and xargs
```
Parentheses
```
( command1; command2 )             Command group executed within a subshell  
Array=(element1 element2 element3) Array initialization  
result=$(COMMAND)                  Command substitution, new style  
>(COMMAND)                         Process substitution  
<(COMMAND)                         Process substitution 
```
Double Parentheses
```
(( var = 78 ))            Integer arithmetic   
var=$(( 20 + 5 ))         Integer arithmetic, with variable assignment   
(( var++ ))               C-style variable increment   
(( var-- ))               C-style variable decrement   
(( var0 = var1<98?9:21 )) C-style ternary operation
````

1. A single bracket (\[) usually actually calls a program named \[; man test or man \[ for more info. Example:
```
$ VARIABLE=abcdef
$ if [ $VARIABLE == abcdef ] ; then echo yes ; else echo no ; fi
yes
```
2. The double bracket (\[\[) does the same thing (basically) as a single bracket, but is a bash builtin.
```
$ VARIABLE=abcdef
$ if [[ $VARIABLE == 123456 ]] ; then echo yes ; else echo no ; fi
no
```
3. Parentheses (()) are used to create a subshell. For example:
```
$ pwd
/home/user 
$ (cd /tmp; pwd)
/tmp
$ pwd
/home/user
As you can see, the subshell allowed you to perform operations without affecting the environment of the current shell.
```
4a. Braces ({}) are used to unambiguously identify variables. Example:
```
    $ VARIABLE=abcdef
    $ echo Variable: $VARIABLE
    Variable: abcdef
    $ echo Variable: $VARIABLE123456
    Variable:
    $ echo Variable: ${VARIABLE}123456
    Variable: abcdef123456
```
4b. Braces are also used to execute a sequence of commands in the current shell context, e.g.
```
    $ { date; top -b -n1 | head ; } >logfile 
    # 'date' and 'top' output are concatenated, 
    # could be useful sometimes to hunt for a top loader )

    $ { date; make 2>&1; date; } | tee logfile
    # now we can calculate the duration of a build from the logfile
```
There is a subtle syntactic difference with ( ), though (see bash reference) ; essentially, a semicolon ; after the last command within braces is a must, and the braces {, } must be surrounded by spaces.

--------------------------------------------------------------------------------------------------------------------------------
## Execute combine multiple linux commands in one line

```
 A ; B   - Run A and then B, regardless of the success or failure of A
 A && B  – Run B only if A succeeded
 A || B  – Run B only if A failed
 A | B   - the output of A will be tranported as the input of B
```

If you want to execute each command only if the previous one succeeded, then combine them using the && operator:
```
cd /my_folder && rm *.jar && svn co path to repo && mvn compile package install
```

If one of the commands fails, then all other commands following it won't be executed.

If you want to execute all commands regardless of whether the previous ones failed or not, separate them with semicolons:
```
cd /my_folder; rm *.jar; svn co path to repo; mvn compile package install
```
In your case, I think you want the first case where execution of the next command depends on the success of the previous one.
You can also put all commands in a script and execute that instead:
```
#! /bin/sh
cd /my_folder \
&& rm *.jar \
&& svn co path to repo \
&& mvn compile package install
```
(The backslashes at the end of the line are there to prevent the shell from thinking that the next line is a new command; if you omit the backslashes, you would need to write the whole command in a single line.)

Save that to a file, for example myscript, and make it executable:
```
chmod +x myscript
```
You can now execute that script like other programs on the machine. But if you don't place it inside a directory listed in your PATH environment variable (for example /usr/local/bin, or on some Linux distributions ~/bin), then you will need to specify the path to that script. If it's in the current directory, you execute it with:
```
./myscript
```
The commands in the script work the same way as the commands in the first example; the next command only executes if the previous one succeeded. For unconditional execution of all commands, simply list each command on its own line:
```
#! /bin/sh
cd /my_folder
rm *.jar
svn co path to repo
mvn compile package install
```

--------------------------------------------------------------------------------------------------------------------------------

## unzip and zip
```
zip [options] zipfile files_list
$zip myfile.zip filename.txt
```
```
Syntax :
$unzip myfile.zip 
unzip file.zip -d destination_folder
```

--------------------------------------------------------------------------------------------------------------------------------


## Install APT
Many (if not most) apt-get operations require write access to the the APT lock file, 
which requires administrator privileges — so most commands listed here are prefixed with sudo, 
and require your password.

APT(the advanced package tools)
```
apt-get                    # it is the command line tool for working with APT software packages
```

--------------------------------------------------------------------------------------------------------------------------------

## Network
```
wget                             # stands for web get
```
Set proxy
```
wget -e use_proxy=yes -e http_proxy=http://xxxx:huawei@10.61.34.138:3128 $sptk_url
```
hash command in Linux system is the built-in command of bash which is used to maintain a hash table of recently executed programs.
It remembers and shows the program locations. It will give the full pathname of each command name.
```
hash
```
```
curl
curl -x <protocol>://<user>:<password>@<host>:<port> --proxy-anyauth <url>
```

The main differences are:
```
wget's major strong side compared to curl is its ability to download recursively.
wget is command line only. There's no lib or anything, but curl's features are powered by libcurl.
curl supports FTP, FTPS, HTTP, HTTPS, SCP, SFTP, TFTP, TELNET, DICT, LDAP, LDAPS, FILE, POP3, IMAP, SMTP, RTMP and RTSP. wget supports HTTP, HTTPS and FTP.
curl builds and runs on more platforms than wget.
wget it's released under a free software copyleft license (the GNU GPL). curl is released under a free software permissive license (a MIT derivate).
curl offers upload and sending capabilities. wget only offers plain HTTP POST support.
```


--------------------------------------------------------------------------------------------------------------------------------

## Navigation
Check the current working directory
```
pwd  # stand for the Print Working Directory
```
Show the content of the current working path

```
ls [option][location]   # it's short for list
ls -l       # long information
```
Path is composed of two parts: relative path and absolute path
More on path:
```
~(tide)      # This is a shortcut for your home directory, 
               that is, /home/znz/a equal to ~\a

.(dot)       # This is a reference to the current directory
..(ddot)     # This is a reference to the parent directory
```

Change the path
```
cd [location] 
```

Shortcut of typing the path
```
Typing out these paths can be tedious, 
we can use the Tab Completion to help us. 
```


--------------------------------------------------------------------------------------------------------------------------------
## Files
Everything is actually a file

Linux is an extensionless system
```
my image = my_image.png=my_image.txt=...
```

We can use the **file** to find out 
```
file [path]
```
Linux is case sensitive
```
test != tesT
```
Spaces in names
```
cd Holiday Photos # x
cd 'Holidy Photos' # use Quotes
cd Holidy\ Photos  # use the Espape Characters: backslash(\)
```
Hidden files or folders
```
use the .          # you can use the 'ls -a' to see the contents 
```

--------------------------------------------------------------------------------------------------------------------------------
## Manual Pages
The manual pages are a set of pages that explain every command 
available in your system.

You can invoke the manual pages with the following command
```
man <command to look up>
```
It is possible to do a keyword search on the manual pages

This can be helpful if you're not quite sure of what command you may 
want to use but you know what you want to achieve.
```
man -k<search term>
```
--------------------------------------------------------------------------------------------------------------------------------
## file manipulation and folder
###  Find out tree
```
tree path
```

When dirname is given a pathname, it will delete any suffix beginning with the last slash ('/') character and return the result
```
dirname
```
```
$ dirname /home/martin/docs/base.wiki
/home/martin/docs

$ dirname /home/martin/docs/.
/home/martin/docs

```
### making a directory
```
mkdir [options]<Directory>
```
If parent directories is needed, we can set the option as **-p**

the second one is **-v** which makes mkdir tell us what it is doing

### Remving a directory
```
rmdir [options]<Directory>       # the file must be empty
```

### Creating a blank file
```
touch [options]<Directory> 
```

###  Copying a file or Directory
```
cp [options] <source><destination>     # created a path if the 
                                         destination doesn't exist
cp [OPTION] Source Destination
cp [OPTION] Source Directory
cp [OPTION] Source-1 Source-2 Source-3 Source-n Directory                                    
```
First and second syntax is used to copy Source file to Destination file or Directory.
Third syntax is used to copy multiple Sources(files) to Directory.

use the **-r** to copy a directory to another place.
```
$ ls
a.txt

$ cp a.txt b.txt

$ ls
a.txt  b.txt
```


### Moving a file or directory
```
mv [options]<source><destination>
```
### rename files and directories
```
mv will be used to move a file or dirctory into a new directory
```

### remove a file (and non empty directories)
```
rm [options]<file> 
```
```
-f                       # delete compulsively
-r                       # recursive
```

### file test operator
```
-e    # file exists
-f    # file exists and is not a directory
-d    # directory exists
-x    # file is executable
-w    # file is writable
-r    # file is readable
```
```
if [ -e path ]; then echo "whatever" fi
```




--------------------------------------------------------------------------------------------------------------------------------
## Sed stream editor

short for "stream editor", allow you to filter and transform text.
```
s/BRE/replacement/flags
sed 's/find/replace/flags' file
```
Substitute the replacement string for instances of the BRE in the pattern space. Any character other than backslash or newline can be used instead of a slash to delimit the BRE and the replacement. Within the BRE and the replacement, the BRE delimiter itself can be used as a literal character if it is preceded by a backslash."

```
echo "Welcome to LikeGeeks page" | sed 's/page/website/'
```

Sample Commands
- The sed command replaces the first occurrence of the pattern in each line
```
sed 's/unix/linux/' geekfile.txt            # replaces the word “unix” with “linux” in the file
                                              Here the “s” specifies the substitution operation
                                              The “/” are delimiters
                                              
sed 's/unix/linux/2' geekfile.txt           # Use the /1, /2 etc flags to 
                                              replace the first, second occurrence of a pattern 
sed 's/unix/linux/g' geekfile.txt           # /g global: Replacing all the occurrence of the pattern in a line 
sed 's/unix/linux/3g' geekfile.txt          # /3-n
```
```
echo "Welcome To The Geek Stuff" | sed 's/\(\b[A-Z]\)/\(\1\)/g'   # Parenthesize first character of each word

```
- Deleting lines from a particular file 

#### Using different delimiters in sed
What if, in sed, you have lots of slashes in the pattern and/or replacement?
```
sed 's/\/a\/b\/c\//\/d\/e\/f\//'    # change "a/b/c/" to "d/e/f/"
```
the so-called toothsaw effect. but that is ugly and unreadable. 
It's a not-so-known fact that sed can use any character as separator for the "s" command
```
sed 's_/a/b/c/_/d/e/f/_'
sed 's;/a/b/c/;/d/e/f/;'
sed 's#/a/b/c/#/d/e/f/#'
sed 's|/a/b/c/|/d/e/f/|'
sed 's /a/b/c/ /d/e/f/ '       # yes, even space
# etc.
```
### Remove character
```
sed 's/a//' file            # To remove a specific character a
sed 's/^.//' file           # remove 1st character
sed 's/.$//' file           # remove last character of every line
sed 's/.//;s/.$//' file     # Two commands can be given together 
                              with a semi-colon separated in between
sed 's/x$//' file           # To remove last character only if it is a specific character
sed 's/...//' file          # remove 1st 3 characters of every line
                              A single dot(.) removes 1st character, 
                              3 dots remove 1st three characters
sed -r 's/.{4}//' file      # To remove 1st n characters of every line
sed -r 's/(.{3}).*/\1/' file # remove everything except the 1st n characters in every line
sed 's/[aoe]//g' file        # remove multiple characters present in a file
```



## Vi Text Editor

Two modes: Insert and Edit mode.
```
Edit - use keyboard to input "i"    ->  Insert
Insert - press "Esc" -> Edit
```


We will look at a tool to put content into files and edit that content
as well.

```
Edit mode:
ZZ        : save and exit
:w        : save file but don't exit
:wq       : again save file and exit
:q!       : discard all changes, since the last save, and exit
```

### view a file

```
cat <file>
```
```
Ctrl+ c          # universal signal for Cancel in linux
```

less allows you to move up and down within a file using the 
arrow keys. pressing b, 
you may go forward a whole page using **spacebar**

When you are done you can press q for quit
```
less <file>
```

### Navigating a file in Vi
```
Arrow keys - move the cursor around
j, k, h, l - move the cursor down, up, left and right (similar to the arrow keys)
^ (caret) - move cursor to beginning of current line
$ - move cursor to end of the current line
nG - move to the nth line (eg 5G moves to 5th line)
G - move to the last line
w - move to the beginning of the next word
nw - move forward n word (eg 2w moves two words forwards)
b - move to the beginning of the previous word
nb - move back n word
{ - move backward one paragraph
} - move forward one paragraph
```
### Deleting content
```
x - delete a single character
nx - delete n characters (eg 5x deletes five characters)
dd - delete the current line
dn - d followed by a movement command. Delete to where the movement command would have taken you. (eg d5w means delete 5 words)
```
### Undoing
Undoing changes in vi is fairly easy
```
u - Undo the last action (you may keep pressing u to keep undoing)
U (Note: capital) - Undo all changes to the current line
```

### several operations
```
copy and paste
search and replace
buffers
markers
ranges
settings
```

## Wildcards
Wildcards are a set of building blocks that allow you 
to create a pattern defining a set of files or directories.

```
* - represents zero or more characters
? - represents a single character
[] - represents a range of characters
```
```
[sv]   : s or  v
[0-9]  : 0~9
[^a-k] : any character except a-k
```

## Permissions
Linux permissions dictate 3 you may do with a file: read,write and execute

```
r read - you may view the contents of the file.
w write - you may change the contents of the file.
x execute - you may execute or run the file if it is a program or script.
```
We can define 3 sets of people for whom we may specify permissions
```
owner - a single person who owns the file. (typically the person who created the file but ownership may be granted to some one else by certain users)
group - every file belongs to a single group.
others - everyone else who is not in the group or the owner.
```
### view permissions
```
ls -l [path]
 ```

- rwx r-- --x 1 harry users 2.7K Jan 4 07:32 
```
first character identifies the file type: dash(-) means it is normal file
                                          d means it is a directory
the following 3 character represent the permissions for owner: dash means the absence of permission
--------------3------------------------------------ for the group
--------------3------------------------------------ for the others
                                 
```
### change permissions
```
chmod   [permissions] [path]               # it stands for change file mode which is a bit of a mouthfull

Who are we changing the permission for? 
[ugoa] - user (or owner), group, others, all

Are we granting or revoking the permission 
- indicated with either a plus ( + ) or minus ( - )

Which permission are we setting? 
- read ( r ), write ( w ) or execute ( x )
```
```
ls -l frog.png
-rwxr----x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod g+x frog.png
ls -l frog.png
-rwxr-x--x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod u-w frog.png
ls -l frog.png
-r-xr-x--x 1 harry users 2.7K Jan 4 07:32 frog.png

```
## change the permissions of the whole folder 
The other answers are correct, in that chmod -R 755 will set these permissions to all files and subfolders in the tree. 

To change all the directories to 755 (drwxr-xr-x):
```
find /opt/lampp/htdocs -type d -exec chmod 755 {} \;
```
To change all the files to 644 (-rw-r--r--):
```
find /opt/lampp/htdocs -type f -exec chmod 644 {} \;
```


### Setting permission shorthand

```
Octal	Binary
0	0 0 0
1	0 0 1
2	0 1 0
3	0 1 1
4	1 0 0
5	1 0 1
6	1 1 0
7	1 1 1
```

```
ls -l frog.png
-rw-r----x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod 751 frog.png
ls -l frog.png
-rwxr-x--x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod 240 frog.png
ls -l frog.png
--w-r----- 1 harry users 2.7K Jan 4 07:32 frog.png

```

Permissions for Directories
```
r - you have the ability to read the contents of the directory (ie do an ls)
w - you have the ability to write into the directory (ie create files and directories)
x - you have the ability to enter that directory (ie cd)
```

### the root user

On a linux system there are only 2 people usually who may change the permissions of a file or directory
, the owner of the file or directory and the root user.

### basic security

##  Filters
A fitler, in context of the linux command line, is a program that accept textual data and then
transform it in particular way.
### View
```
cat                                      # look the whole article
head [-number of lines to print] [path]  # it is a program that prints the first n lines of the article
tail                                     # the last n lines of the article
```
### sort and numberate
```
sort                                     # it will sort alphabetically but there are many
                                           options available to modify the sorting mechanism
nl                                       # it stands for numbering lines
```
### word count
```
wc                                       # it stands for word count

wc by default will give a count fo all 3 but using command line options we may limit it to
just we are after
-l         # number of lines
-w         # number of words
-m         # number of characters
```
### get column
```
cut [-options] [path]                   # cut is a nice program to use if your content is 
                                          seperated into fields(columns) and you only want 
                                          certain fields

-f          # field
-d          # seperator
```

### replace  and remove tediousness
```
sed <expression> [path]                   # stream editor; it effectively allows us to do a search
                                          and replace on our data

expression: 
s                    # substitude
/search
/replace/
g                    # global
```
```
uniq                                      # it stands for unique and its job is to remove duplicate
                                            lines in data
                                            Its limitation is those lines must be adjacent
```

### reverse view
```
tac                                       # tac is actually cat in reverse; Given data it will
                                            print the last line first
```

## Grep and Regular Expressions
The basic behaviour of egrep is that it will print the entire line for every line which contains a string of characters matching the given pattern. This is important to note, we are not searching for a word but a string of characters.

### Grep
The grep command is used to search text. It searches the given file for lines containing a match to the given strings or words. It is one of the most useful commands on Linux and Unix-like system. Let us see how to use grep on a Linux or Unix like system.
```
grep [command line options]<pattern>[path]

grep 'word' filename
grep 'word' file1 file2 file3
grep 'string1 string2'  filename
cat otherfile | grep 'something'
command | grep 'something'
command option1 | grep 'data'
grep --color 'data' fileName
```

The name, “grep”, derives from the command used to perform a similar operation, using the Unix/Linux text editored:
```
g/re/p
```
grep command examples
Common grep command explained with examples in Linux:
```
grep 'word' filename         # Search any line that contains the word in filename on Linux
grep -i 'bar' file1          # A case-insensitive search for the word ‘bar’ in Linux and Unix
grep -R 'foo'                # Search all files in the current directory and in all of its subdirectories 
                              in Linux for the word ‘foo’
grep -c 'nixcraft' frontpage.md           # Search and display the total number of times 
                                            that the string ‘nixcraft’ appears 
                                            in a file named frontpage.md
```
#### use grep to search words only
When you search for boo, grep will match fooboo, boo123, barfoo35 and more. You can force the grep command to select only those lines containing matches that form whole words i.e. match only boo word:
```
$ grep -w "boo" file
```
#### use grep to search 2 different words
Use the egrep command as follows:
```
$ egrep -w 'word1|word2' /path/to/file
```
#### Force grep invert match
You can use -v option to print inverts the match; that is, it matches only those lines that do not contain the given word. For example print all line that do not contain the word bar:
```
$ grep -v bar /path/to/file
```
#### UNIX / Linux pipes and grep command
Display cpu model name:
```
# cat /proc/cpuinfo | grep -i 'Model'
```
However, above command can be also used as follows without shell pipe:
```
# grep -i 'Model' /proc/cpuinfo
```
#### conclusion
```
Linux grep command options	Description
-i  Ignore case distinctions on Linux and Unix
-w  Force PATTERN to match only whole words
-v  Select non-matching lines
-n  Print line number with output lines
-h  Suppress the Unix file name prefix on output
-r  Search directories recursivly on Linux
-R  Just like -r but follow all symlinks
-l  Print only names of FILEs with selected lines
-c  Print only a count of selected lines per FILE
--color	Display matched pattern in colors
-f  file : Takes patterns from file, one per line.
```






### Regular Expressions
```
. (dot) - a single character.
? - the preceding character matches 0 or 1 times only.
* - the preceding character matches 0 or more times.
+ - the preceding character matches 1 or more times.
{n} - the preceding character matches exactly n times.
{n,m} - the preceding character matches at least n times and not more than m times.
[agd] - the character is one of those included within the square brackets.
[^agd] - the character is not one of those included within the square brackets.
[c-f] - the dash within the square brackets operates as a range. In this case it means either the letters c, d, e or f.
() - allows us to group several characters to behave as one.
| (pipe symbol) - the logical OR operation.
^ - matches the beginning of the line.
$ - matches the end of the line.
```
## Piping and Redirection

Every program we run on the command line automatically has three data streams connected 
to it

```
STDIN(0)            # standard input 
STDOUT(1)           # standard output 
STDERR(2)           # standard error
``` 
Piping and redirection is the means by which we may connect these streams between programs
and files to direct data in interesting and useful ways.

### redirecting to a file

Normally we will get our output on the screen, which is convenient most of the time. but sometime we
may wish to save it into a file to keep as a record.
```
>              # the greater operator indicates to saved in a file insteed of printed to the screen
                 New file | old file: cleared and rewrite
>>             # double greater than operator, old file: the new data to be appended to the file 
```
### redirecting from a file
```
<              # we use the less than operator, read data from file and feed it into program 
```

### redirecting stderr
```
0            # STDIN
1            # STDOUT
2            # STDERR
```
```
app    1> /2>              #  redirect stdout/stderr to a file
1>                        ->  can be shortened to just >
1>foo 2>&1                ->  >&foo or &>foo
2>&1 | program            ->  |& program
```
The following is the same
```
app    1>file1  2>file2       
app    &>file1               # redirect all to the same file
app    1>/dev/null 2>&1      # points file descriptor #2 to where #1 already pointing
app    2>/dev/null 1>&2
```
Send the output to standard error instead of standard out.
```
echo >&2 "message"                # redirect stdout from echo command to stderr
```
```
> redirect standard output (implicit 1>)
& what comes next is a file descriptor, not a file (only for right hand side of >)
2 stderr file descriptor number
```




### piping
So far we've dealt with sending data to and from files, 

now we'll take a look at a mechanism for
sending data from one program to another. It's called piping
```
|                                  # operator
```

```
ls
barry.txt bob example.png firstfile foo1 myoutput video.mpeg
ls | head -3
barry.txt
bob
example.png
```
```
ls | head -3 | tail -1 > myoutput
cat myoutput
example.png
```

## process management
tweak the running fo the system to better suit our need.

a program is a series of instructions that tell the computer what to do.
When we run a program, those instruction are copied into memory and space is allocated to variables
and other stuff required to manage its execution.
```
top                   # what is currently running ?
ps [aux]              # process
df -h                 # report file system disk space usage in human way
```

```
PID  # process ID
```

### killing a crahsed process

```
ps aux | grep 'firefox'
ryan 6978 8.8 23.5 2344096 945452 ? Sl 08:03 49:53 /usr/lib64/firefox/firefox

```
Normal users may only kill processes which they are the owner for. 
The root user on the system may kill anyones processes.
```
kill [signal]<PID>
```

### foreground and background jobs

```
sleep   <seconds>                # to wait for seconds
jobs                             # it lists currently running background jobs for us
ampersand &                      # we are telling the terminal to run this process in the 
                                   background
ENTER(keyboard)                  # you will see a message come up telling you the job has completed
ctrl + z                         # the currently running foreground process will be paused and 
                                   moved into background
fg                               # the terminal will bring background processes into foreground

```



## Bssh Scripting


Anything you can run on the command line you may place into a script and 
they will behave exactly the same. 
Vice versa, anything you can put into a script, 
you may run on the command line and again it will perform exactly the same.

```
echo <message>
```
```
cat myscript.sh                               # the extension is not essential
#!/bin/bash                                   # to identify which interpreter should be used
                                                #! is a shebang + path
# A simple demonstration script               # comment
# Ryan 14/3/2019
 
echo Here are the files in your current directory:      # print whatever you place after it
ls

ls -l myscript.sh                                       # a script must have the execute permission
-rwxr-xr-x 1 ryan users 2 Jun 4 2012 myscript.sh         

```
### important Points
- The Shebang

The very first line of a script should tell the system which interpreter should be used on this file

If we don't know where our interpreter is located then we may use a program called which to find out
```
which <program>
```
```
which bash
```

- the name

Linux is an extensionless system, we can call our script whatever we like


- comments
A comment is just a note in the script that does not get run.

all you need to do is to place a bash(#) then anything after that is considered a comment.

- why the ./

We can override this behaviour however by supplying a path
``` 
echo $PATH                 # directory is seperated by colon(:)
```

-permissions




## Bonus Material- Useful Commands

### cron - task scheduling
cron stands for Command Run On that allow you tell the system to run certain commands at certain times
```
* * * * * command to execute

Where the *'s represent (in order from left to right:
Minutes (0 - 59)
Hours (0 - 23)
Day of Month (1 - 31)
Months (1 - 12)
Day of week (0 - 7) (0 and 7 are Sunday)
```

```
crontab -l
crontab -e
```
### xargs
Xargs is a useful tool to run a particular command for every item in a list.
```

ls
image1.JPG image2.JPG image3.JPG image4.jpg

basename -s .JPG -a *.JPG | xargs -n1 -i mv {}.JPG {}.jpg
#     -s remove suffix, -a all files | -n1 executed once for each item, -i a replacement
ls
image1.jpg image2.jpg image3.jpg image4.jpg
```

### find
```
find /home -size +200M -exec ls -sh {} \;
# -size a search option; -exec tell find to execute the following command for each files it finds


452M /home/barry/backups/everything.tar.gz
941M /home/lisa/projects/loony/servermigration.tar.gz
768M /home/mark/Documents/gregs_birthday.mpg

```
### Tar
Tar stands for Tape ARchive and is a popular means for 
combining and compressing several files into a single file

### Awk
Awk is a good program to use if you need to work with data 
that is organised into records with fields (such as the sample data below). 
It allows you to filter the data and control how it is displayed. 


```
du -sh ./*
               Find the size of every directory in your current directory.
df -h
               Display how much disk space is used and also free.
basename -s .jpg -a *.jpg | xargs -n1 -i cp {}.jpg {}_original.jpg
               Make a copy of every jpg image file in the current directory and rename adding _original.
find /home -mtime -1
               Find all files in the given directory (and subdirectories) which have been modified in the last 24 hours.
shutdown -h now
               Shutdown the system. (Replace -h with -r for reboot.)
```
















