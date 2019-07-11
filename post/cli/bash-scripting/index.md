---
title: "Introduction to Bash Shell Scripting"
date: 2019-01-15T07:00:00+02:00
description: "A detailed overview to scripting the Bash Shell"
tags: cli
---

Shell scripting is an powerful way to automate tasks that you regularly execute on your computer.

In this tutorial I give an extensive overview of shell scripting, and will be the base reference for more in-depth and advanced tutorials on creating practical shell scripts.

> Check out my [introduction to Bash](/bash/) post.

Bash gives you a set of commands that put together can be used to create little programs, that by convention we call scripts.

Note the difference. We don't say Bash programming but Bash scripting, and we don't call Bash scripts "Bash programs". This is because you can generally reach a certain amount of complexity before feeling that your scripts gets out of hand.

But Bash scripts are great because you don't need anything else than Bash to run them. No compiler, no interpreter, just your shell.

There are many things that you'll miss from programming languages like Perl or JavaScript or Python.

Variables have no scope, they are all global, there is no standard library, you don't have a module system, for instance. But the advantages are pretty great: you can very easily invoke any CLI tool just like you were in the shell, and the Unix approach of having many little utility commands really makes shell scripting shine. Perform network requests with `wget`, process text using `awk`, and more.

Shell scripting is one of the tools you'd better know, at least know how to read a program when you see it, and the goodies it can bring in your day to day work.

This tutorial guides you to the theory and concepts of Bash scripting. I will post more detailed tutorials on specific techniques or how to solve specific problems in the future.

## Basics

Scripts are stored in files. You can give any name and extension to a shell script, it does not matter. The important thing is that it must start with a "shebang" on the first line:

```bash
#!/bin/bash
```

and it must be an executable file.

A file is set as executable using `chmod`, an utility command.

You can use it like this:

```bash
chmod u+x myscript
```

to make the `myscript` file executable for your user (I'm not going in the permissions rabbit hole here, but I will cover them soon).

Now you can execute the script if you are in the same folder by calling it `./myscript`, or using the full path to it.

While learning I encourage you - when possible - to use an online playground [like this one](https://rextester.com/l/bash_online_compiler), it makes things easier to test.

## Comments

Comments are one of the most important things when writing programs. A line starting with the `#` symbol is a comment (with the exception of the shebang line you saw above here).

```bash
#!/bin/bash
# this is a comment
```

A comment can start at the end of a line too:

```bash
#!/bin/bash
echo ok # this is a comment
```

## Variables

You can set variables by using the `=` operator:

```bash
name=value
```

Examples:

```bash
ROOM_NUMBER=237
name=Flavio
nickname="Flavio"
```

You can print a variable by using the `echo` built-in command and prepending a `$` to the var name:

```bash
echo $ROOM_NUMBER
echo $name
```

## Operators

Bash implements some arithmetic operators commonly used across programming languages:

- `+` add
- `-` subtract
- `*` multiply
- `/` divide
- `%` modulo (remainder of the division)
- `**` exponentiation

You can compare values using

- `<`
- `<=`
- `==`
- `>=`
- `>`

You can also use these comparison operators:

- `-lt` lower than
- `-gt` greater than
- `-le` lower or equal than
- `-ge` greater or equal than
- `-eq` equal to
- `-ne` not equal to

In this way:

```bash
#!/bin/bash
age=23
minimum=18
if test $age -lt $minimum
then
  echo "Not old enough"
fi
```

Logical operators:

- `&&` logical AND
- `||` logical OR

These shortcuts allow to perform an arithmetic operation and then an assignment:

- `+=`
- `-=`
- `*=`
- `/=`
- `%=`

There are some more operators, but those are the most common ones.

## Print to the screen

You can print anything to the screen using the `echo` command:

```bash
#!/bin/bash
echo "test"
echo test
echo testing something
```

## Logical conditions

AND: evaluates to `0` (zero) if both `command` and `anothercommand` execute and return `0`. Returning zero in shell commands means the command was successful. An error message is identified by a non-zero return value.

```bash
command && anothercommand
```

OR: evaluates to `0` (zero) if at least one of `command` and `anothercommand` execute and return `0`.

```bash
command || anothercommand
```

NOT: invert the logic return value of `command`:

```bash
! command
```

## Control structures

In you can use several control structures which you might be familiar with:

### If/else statements

Simple `if`:

```bash
if condition
then
  command
fi
```

`if` then `else`:

```bash
if condition
then
  command
else
  anothercommand
fi
```

Nested `if` - then - `else`:

```bash
if condition
then
  command
elif
  anothercommand
else
  yetanothercommand
fi
```

You can keep the `else` on the same line by using a semicolon:

```bash
if condition ; then
  command
fi
```

Example:

```bash
#!/bin/bash
DOGNAME=Roger
if [ "$DOGNAME" == "" ]; then
  echo "Not a valid dog name!"
else
  echo "Your dog name is $DOGNAME"
fi
```

Notice the brackets? We must add brackets when we have to do any kind of evaluation of a boolean expression.

### Loops

#### While loop

While `condition` resolves to a true value, run `command`

```bash
while condition
do
  command
done
```

#### Until

Until `condition` resolves to a true value, run `command`

```bash
until condition
do
  command
done
```

#### For in

Iterate a list and execute a command for each item

```bash
for item in list
do
  command
done
```

#### Break and continue

Inside the loops, you can use the `break` and `continue` statements to break the loop completely, or just skip the current iteration.

### Case

A case control structure lets you pick different routes depending on a value.

```bash
case value in
  a)
    command
    #...
    ;;
  b)
    command
    #...
    ;;
esac
```

Like with `fi`, `esac` ends the case structure and as you can notice it's `case` spelled backwards.

We add a double semicolon after each case.

A `*)` case would handle all the cases not explicitly expressed.
Using a `|` symbol you can express multiple choices for a single case.

Example:

```bash
#!/bin/bash
read -p "How many shoes do you have?" value
case $value in
  0|1)
    echo "Not enough shoes! You can't walk"
    ;;
  2)
    echo "Awesome! Go walk!"
    #...
    ;;
  *)
    echo "You got more shoes than you need"
    #...
    ;;
esac
```

### Select

A `select` structure shows the user a menu of choices to choose:

```bash
select item in list
do
  command
done
```

Example:

```bash
#!/bin/bash
select breed in husky setter "border collie" chiwawa STOP
do
  if [ "$breed" == "" ]; then
    echo Please choose one;
  else
    break
  fi
done

echo "You chose $breed"
```

## Testing conditions

I used the term `condition` in the above control structures.

You can use the `test` Bash built-in command to check for a condition and return a true (`0`) or false value (not `0`).

Here is an example:

```bash
#!/bin/bash
if test "apples" == "apples"
then
  echo Apples are apples
fi

if ! test "apples" == "oranges"
then
  echo Apples are not oranges
fi
```

## Reading input from the command line

You can make your scripts interactive by using the `read` built-in command. This command reads a line from the standard input, and it can format input in a very flexible way.

The simplest usage is:

```bash
echo "Age:"
read age
```

this is going to print "Age:" and you can enter a number, press enter and that number will be assigned to the `age` variable.

The `-p` option of `read` provides a built-in prompt, and puts the input in the `age` variable:

```bash
read -p "Age: " age
```

The `read` command has many more options, which you can inspect by typing `help read` in Bash.

## Adding options

Options are specified using a hyphen followed by a letter, like this:

```bash
ls -a
driveCar -b "Ford"
```

In your code you use the built-in command `getopts` to parse the options and get the value.

If we accept options `a` and  `b` , we feed `getopts ab` to a while loop.

If option `b` accepts a value, we append a colon `:` after it, so we format our `getopts` call like this: `getopts ab: arg`

Here's a snippet:

```bash
while getopts xy: arg
do
  case $arg in
    x) echo "Option $arg enabled" ;;
    y) echo "The value of $arg is $OPTARG" ;;
    esac
done
```

In this script, `$OPTARG` is automatically assigned the option letter. We tell `getopts` which options we accept, and we handle each case separately.

Errors are handled automatically by `getopts`. We can choose to handle error messages ourselves, by prepending a colon `:` before the arguments definition: `getopts :xy: arg`.

Then we also handle the `\?`  and `:` cases. The first is called when we pass an invalid option, and the second is called when we miss an option:

```bash
while getopts :xy: arg
do
  case $arg in
    x) echo "Option $arg enabled" ;;
    y) echo "The value of $arg is $OPTARG" ;;
    :) echo "$0: Must supply an argument to -$OPTARG." >&2
       exit 1 ;;
    \?) echo "Invalid option -$OPTARG ignored." >&2 ;;
    esac
done
```

Now if you miss to add an argument, the error messages are different.

## Working with parameters

Inside a script you can access any parameter that was passed at invocation time. You access them using `$0`, `$1`, `$2` and so on, depending on the position, where `$0` is the name of the command and incrementing the number the position of the parameter is incremented. After position 9 you need curly braces: `${10}`, `${11}` ...

For example running this `startCar` script:

```bash
#!/bin/bash
echo $0
echo $1
```

as  `./startCar fiesta` will print

```bash
./startCar
fiesta
```

The special `$*` syntax prints all the parameters, and `$#` the number of parameters passed:

```bash
#!/bin/bash
echo $# $*
```

```bash
./test.sh Milan Florence Rome
3 Milan Florence Rome
```

## Separating options from parameters

If you have both options and parameters you need to separate them. You do this with a hyphen:

```bash
driveCar -m "Ford Fiesta" - Milan Florence Rome
```

## Working with strings

Given a string:

```bash
dogname="Roger"
```

You can get its length using `${#dogname}`

Always use quotes around strings, when working with them, to avoid Bash interpreting the special characters inside them.

You can compare 2 strings using the `=` or `==` operator, it's the same:

```bash
"$dogname" = "$anotherdogname"
"$dogname" == "$anotherdogname"
```

It's not an assignment because of the spaces surrounding the `=`.

You can also check for unequality:

```bash
"$dogname" != "$anotherdogname"
```

## Arrays

An array is a list of items, declared inside parentheses:

```bash
breeds=(husky setter "border collie" chiwawa)
```

You can reference any item inside an array using square brackets:

```bash
breeds[0]
breeds[1]
```

and you can get the total number of items using this special syntax:

```bash
${#breeds[@]}
```

## Built-in commands

So far you've seen a few built-in commands already, like these:

- `test`
- `read`
- `echo`

Bash has a number of them. You can see them all by calling `help` and then you can find the help for each command using for example `help read`.

## Functions

Just like in JavaScript or in any other programming language, you can create little reusable pieces of code, give them a name, and call them when you need.

Bash calls them *functions*.

You define a function with

```js
function name {

}
```

Example:

```js
function cleanFolder {

}
```

and you invoke it like this:

```js
cleanFolder
```

You can pass parameter to folders, without the need of declaring them - you just reference them as `$1`, `$2` etc. Like you do for script parameters:

```js
function cleanFolder {
  echo "Clean folder $1"
}
cleanFolder "/Users/flavio/Desktop"
```

## Wrapping up

That's it for this introductory post on Bash Shell scripting! Hopefully I will make more tutorials on it soon.
