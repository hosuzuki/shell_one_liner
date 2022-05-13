# Shell One Liner

Individual Linux commands can be combined in the command line ant it is extremely powerful.  This repo introduces you to linux one liners that will help you accomplish useful tasks.


# Basics

## regular expressions (a.k.a. regex, regexp, or r.e.)

A regular expression is a pattern that matches strings or pieces of strings. 

| example | explanation |
| --- | --- |
| ^The   | matches any string that starts with The |
| end$　| matches a string that ends with end |
| abc* | matches a string that has ab followed by zero or more c |
| abc+ | matches a string that has ab followed by one or more c |
| abc? | matches a string that has ab followed by zero or one c |
| abc{2} | matches a string that has ab followed by 2 c |
| abc{2,} | matches a string that has ab followed by 2 or more c |
| abc{2,5} | matches a string that has ab followed by 2 up to 5 c |
| a(bc)* | matches a string that has a followed by zero or more copies of the sequence bc |
| a(bc){2,5} | matches a string that has a followed by 2 up to 5 copies of the sequence bc |
| a(b\|c) | matches a string that has a followed by b or c (and captures b or c) |
| a[bc]  | same as previous, but without capturing b or c |
| \d | matches a single character that is a digit |
|\D |  matches a single non-digit character |
|\\$\d  |  matches a string that has a $ before one digit|
| \w | matches a word character (alphanumeric character plus underscore) |
| \s | matches a whitespace character (includes tabs and line breaks) |
| . |  matches any character |
| a(bc) |  parentheses create a capturing group with value bc |
| a(?:bc)* | using ?: we disable the capturing group |
| a(?\<foo\>bc)| using ?<foo> we put a name to the group |
| [abc] | matches a string that has either an a or a b or a c \-\> is the same as a\|b\|c |
| [a-c] | same as previous |
| [a-fA-F0-9] | a string that represents a single hexadecimal digit, case insensitively |
| [0-9]%  | a string that has a character from 0 to 9 before a % sign |
| [^a-zA-Z] |  a string that has not a letter from a to z or from A to Z. In this case the ^ is used as negation of the expression |
|  <.+?>| matches any character one or more times included inside < and >, expanding as needed | 
|  <[^<>]+> | matches any character except < or > one or more times included inside < and > | 
| \babc\b |  performs a "whole words only" search| 
| \Babc\B |  matches only if the pattern is fully surrounded by word characters| 
| ([abc])\1 |  using \1 it matches the same text that was matched by the first capturing group | 
| ([abc])([de])\2\1 | we can use \2 (\3, \4, etc.) to identify the same text that was matched by the second (third, fourth, etc.) capturing group| 
| (?\<foo\>[abc])\k\<foo\>| we put the name foo to the group and we reference it later (\k<foo>). The result is the same of the first regex | 
| d(?=r) | matches a d only if is followed by r, but r will not be part of the overall regex match| 
| (?<=r)d |  matches a d only if is preceded by an r, but r will not be part of the overall regex match| 
| d(?!r) | matches a d only if is not followed by r, but r will not be part of the overall regex match | 
| (?<!r)d | matches a d only if is not preceded by an r, but r will not be part of the overall regex match| 
  
 Ref.:
 https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285
  
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

## awk
  
```bash
seq 5 | awk 'BEGIN{a=0}$1%2==0{print $1, "Even"}$1%2==1{print $1, "Odd"}{a+=$1}END{print "sum",a}'
 ```

result
```bash
1 Odd
2 Even
3 Odd
4 Even
5 Odd
sum 15
```

In an awk rule, either the pattern or the action can be omitted, but not both. If the pattern is omitted, then the action is performed for every input line. If the action is omitted, the default action is to print all lines that match the pattern.
In this case, `$1%2==0` and `$1%2==1` are patterns.

## sort and uniq

```bash
seq 5 | awk '{print $1%2 ? "Odd" : "Even"}' | sort | uniq -c | awk '{print $2,$1}'
```
  
result
```bash
Even 2
Odd 3
```
  
awk version (without using sort and uniq)
```bash
seq 5 | awk '{print $1%2 ? "Odd" : "Even"}' | awk '{a[$1]++}END{for(k in a)print k, a[k]}'
```
