# Issue lists
## test
Checks file types and compares values.


test exits with the status determined by EXPRESSION. Placing the EXPRESSION between square brackets (\[ and \]) is the same as testing the EXPRESSION with test. 

```
test 100 -gt 99 && echo "Yes, that's true." || echo "No, that's false."
```
To see the exit status at the command prompt, echo the value "$?" A value of 0 means the expression evaluated as true, and a value of 1 means the expression evaluated as false.
```
[ "awesome" = "awesome" ]; echo $?
```
## Manipulating Strings
[advanced bash-scripting guide](http://www.tldp.org/LDP/abs/html/string-manipulation.html)

### string removal
```
${string#substring}                 # Deletes shortest match of $substring from front of $string.
${string##substring}                # Deletes longest match of $substring from front of $string.
```
```
stringZ=abcABC123ABCabc
#       |----|          shortest
#       |----------|    longest

echo ${stringZ#a*C}      # 123ABCabc
# Strip out shortest match between 'a' and 'C'.

echo ${stringZ##a*C}     # abc
# Strip out longest match between 'a' and 'C'.



# You can parameterize the substrings.

X='a*C'

echo ${stringZ#$X}      # 123ABCabc
echo ${stringZ##$X}     # abc
                        # As above.
```
```
${string%substring}     # Deletes shortest match of $substring from back of $string.
${string%%substring}    # Deletes longest match of $substring from back of $string.
```
```
# Rename all filenames in $PWD with "TXT" suffix to a "txt" suffix.
# For example, "file1.TXT" becomes "file1.txt" . . .

SUFF=TXT
suff=txt

for i in $(ls *.$SUFF)
do
  mv -f $i ${i%.$SUFF}.$suff
  #  Leave unchanged everything *except* the shortest pattern match
  #+ starting from the right-hand-side of the variable $i . . .
done ### This could be condensed into a "one-liner" if desired.

# Thank you, Rory Winston.
```
