# Shell One Liner

Individual Linux commands can be combined in the command line ant it is extremely powerful.  This repo introduces you to linux one liners that will help you accomplish useful tasks.


# Basics


## regular expression



## pipe

```bash
echo '1+2' | bc
```
The output is `3`.

`$ echo '1+2'` will simply show `1+2`in the terminal.<br>
The pipe `|` can use the output of command at the lefthand side as an input to the right.

## save the output to a file

```bash
echo '1+2' | bc > output.txt
```
The output `3` will be stored in the file called "output.txt".

`>` is called redirect because it changes the direction of output from a terminal to a file.

## sed
```bash
echo this_is_an_apple | sed 's/an_apple/a_pen/'
```
The output will be `this_is_a_pen`.

## grep
```bash
seq 100 | grep 0
```

`seq` command is used to generate numbers from FIRST to LAST in steps of INCREMENT.
If the FIRST was not indicated, it starts from 1.

`grep` is used to search text and strings in a given file or strings.
In this case, grep command search the number which contain `0` from 1 to 100.

## 

