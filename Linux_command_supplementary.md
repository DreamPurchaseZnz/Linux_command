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
