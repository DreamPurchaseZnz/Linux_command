# Shell parameters
A parameter is an entity that stores values
In other words, variables

Declaration functions:
```
alias, declare, typeset, export, readonly, and local builtin commands
```


## Parameter expansion
(Parameter expansion)[https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html]

The ‘$’ character introduces arithmetic expansion, command substitution, or parameter expansion

The basic form of parameter expansion is 
```
${parameter}
```
e.g.
Check whether parameter exists
```
${parameter:-word}           not exist, use word
${parameter:=word}           not exist, use word and assign to parameters
${parameter:?word}           not exist, print word to stderr
${parameter:+word}           exit and use word
```

```
${parameter:offset}
${parameter:offset:length}         start:end-start   
```

Matching pattern
```
${parameter#word}
${parameter##word}
${parameter%word}
${parameter%%word}
```
substitude
```
${parameter/pattern/string}
```


