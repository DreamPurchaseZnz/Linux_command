# Bash functions
(base on this)[https://ryanstutorials.net/bash-scripting-tutorial/bash-functions.php]
function statement or brackets
```
function_name () {
<commands>
}
```
or 
```
function function_name {
<commands>
}
```

break once meet return
```
return <value>
```
Exit the function with a return status of value

## Parsing arguments
put arguments directly after the function name 

```
function_name arguments
```

## variable scope
A local variable can only be accessed within the function. 

Local statement

```
local variable_name=variable_value
```
## overriding commands

create a wrapper

keyword command in front of the name 
```
#!/bin/bash
# Create a wrapper around the command ls
ls () {
command ls -lh
}

ls
```
It's easy to forget the command keyword and end up in an endless loop




  













