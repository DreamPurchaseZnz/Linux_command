# Linux_command
[Linux tutorial](https://ryanstutorials.net/linuxtutorial/commandline.php)

[bash reference manual](http://tiswww.case.edu/php/chet/bash/bashref.html#SEC31)

## Variable call
You need to mannually invoke the variables by using
```
$ varaible_name or ${variable_name}
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
find . -type f -exec grep "example" '{}' \; -print      # find . -type f -print | xargs grep "example"
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
```
#!/bin/bash
# set variables 
declare -r TRUE=0
declare -r FALSE=1
declare -r PASSWD_FILE=/etc/passwd

##################################################################
# Purpose: Converts a string to lower case
# Arguments:
#   $1 -> String to convert to lower case
##################################################################
function to_lower() 
{
    local str="$@"
    local output     
    output=$(tr '[A-Z]' '[a-z]'<<<"${str}")
    echo $output
}
##################################################################
# Purpose: Display an error message and die
# Arguments:
#   $1 -> Message
#   $2 -> Exit status (optional)
##################################################################
function die() 
{
    local m="$1"	# message
    local e=${2-1}	# default exit status 1
    echo "$m" 
    exit $e
}
##################################################################
# Purpose: Return true if script is executed by the root user
# Arguments: none
# Return: True or False
##################################################################
function is_root() 
{
   [ $(id -u) -eq 0 ] && return $TRUE || return $FALSE
}

##################################################################
# Purpose: Return true $user exits in /etc/passwd
# Arguments: $1 (username) -> Username to check in /etc/passwd
# Return: True or False
##################################################################
function is_user_exits() 
{
    local u="$1"
    grep -q "^${u}" $PASSWD_FILE && return $TRUE || return $FALSE
}
```
You can load myfunctions.sh into the current shell environment, enter:
```
. myfunctions.sh

```

```
#!/bin/bash
# Load the  myfunctions.sh 
# My local path is /home/vivek/lsst2/myfunctions.sh
. /home/vivek/lsst2/myfunctions.sh

# Define local variables
# var1 is not visitable or used by myfunctions.sh
var1="The Mahabharata is the longest and, arguably, one of the greatest epic poems in any language."

# Invoke the is_root()
is_root && echo "You are logged in as root." || echo "You are not logged in as root."

# Find out if user account vivek exits or not
is_user_exits "vivek" && echo "Account found." || echo "Account not found."

# Display $var1
echo -e "*** Orignal quote: \n${var1}"

# Invoke the to_lower()
# Pass $var1 as arg to to_lower()
# Use command substitution inside echo
echo -e "*** Lowercase version: \n$(to_lower ${var1})"
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
 A ; B  – Run A and then B, regardless of the success or failure of A
 A && B  – Run B only if A succeeded
 A || B  – Run B only if A failed
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
## system PATH 
```
echo $PATH               
printf "%s\n" $PATH
```
Modify current PATH

In general, the export command marks an environment variable to be exported with any newly forked child processes and thus it allows a child process to inherit all marked variables.
```
$ export
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
```

use the **-r** to copy a directory to another place.

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
```
egrep [command line options]<pattern>[path]   
```

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
2>             # with a number
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

### Variables

```
When we set a variable, its name followed directly by an equals sign(=)
When we refer a variable, we must place a dollar sign ($) before the variable name
```

```
cat variableexample.sh
#!/bin/bash
# A simple demonstration of variables
# Ryan 14/3/2019
 
name='Ryan'
echo Hello $name
```

- command line arguments and More

```
$0 - The name of the script.
$1 - $9 - Any command line arguments given to the script.
          $1 is the first argument, $2 the second and so on.
$# - How many command line arguments were given to the script.
$* - All of the command line arguments.
```

These are positional arguments of the script.

Executing
```
./script.sh Hello World
Will make
```
```
$0 = ./script.sh
$1 = Hello
$2 = World
```
Note

If you execute ./script.sh, $0 will give output ./script.sh 

but if you execute it with bash script.sh it will give output script.sh.

- backticks

the left of the 1 (one) key on the keyboard

It is also possible to save the output of a command to a variable

Here is a list of all comparison operator
```
-eq # equal to
-ne # not equal to
-lt # less than
-le # less than or equal to
-gt # greater than
-ge # greater than or equal to
```



### if statements
the basic structure of the if statement looks like this

```
if [ conditional-expression ]                          # the condition is inside the brackets; there MUST have a SPACE between the
                                                         the condition and bracket
then       
  commands                                             # if true, the commands following the then statement are executed                                          
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
















