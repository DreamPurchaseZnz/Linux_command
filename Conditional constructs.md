# Conditional 
(here)[https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Conditional-Constructs]
 
## if
The syntax of the if command is:
```
if test-commands; then
  consequent-commands;
[elif more-test-commands; then
  more-consequents;]
[else alternate-consequents;]
fi
```
## case
The syntax of the case command is:
```
case word in
    [ [(] pattern [| pattern]…) command-list ;;]…
esac
```
Each clause must be terminated with ‘;;’, ‘;&’, or ‘;;&’
```
echo -n "Enter the name of an animal: "
read ANIMAL
echo -n "The $ANIMAL has "
case $ANIMAL in
  horse | dog | cat) echo -n "four";;
  man | kangaroo ) echo -n "two";;
  *) echo -n "an unknown number of";;
esac
echo " legs."
```
It’s a common idiom to use ‘*’ as the final pattern to define the default case, since that pattern will always match

## ((…))
((…)) The arithmetic expression
```
((2+2))
((2+))
```
## [[…]]
```
-f -d       premaries
== =!       
=~
```
## ( expression )
Returns the value of expression

## ! expression
True if expression is false.

# Grouping Commands
## ()
```
( list )
```
open a subshell
## {}
current shell


