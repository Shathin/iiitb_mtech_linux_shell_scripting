> 📌 I use Visual Studio Code for writing shell scripts and hence I use the command code shell-script-file.sh to open the file with the editor.
You can use nano, gedit or any other code editor of your choice.

# Introduction

- A Unix shell is a command language interpreter, the primary purpose of which is to translate commands typed in the terminal into system actions. Hence, the shell itself is a program through which other programs are invoked.
- Standard Unix commands can be combined to use build our own commands. This is achieved by writing a **shell script** which contains a sequence of commands; this file is then executed as a single command.
- Writing shell scripts can be helpful in automating complex yet periodic tasks.

### Knowing Supported Shells and their location

- To know which shells are supported by the Linux system you can use `cat /etc/shells` command. A sample output of this is -
    
    ```bash
    $ cat /etc/shells
    # /etc/shells: valid login shells
    /bin/sh
    /bin/bash
    /bin/rbash
    /bin/dash
    /usr/bin/tmux
    /usr/bin/screen
    ```
    
- To know where a shell is located you can use `which shell-name` command. A sample output of this is -
    
    ```bash
    $ which bash
    /bin/bash
    ```

### Creating a "Hello world" shell script

> 💡 Giving the `.sh` extension to a shell is optional. The file can be executed as a shell script without the `.sh` extension. Using an extension will help editors to provide linting capabilites.

> ⚠️ Sometimes when you try to execute a shell script you might face an error saying `Permission denied`. When this happens, use the `chmod` command to give the *execute* permission to the user or to one who wants to execute the script.


```bash
$ touch hello-world.sh
$ code hello-world.sh
```

```bash
#! /bin/bash
echo "Hello world"

```

```bash
$ ./hello-world.sh
Hello world
```

- The first line (`!# /bin/bash`) known as *hash bang* helps the interpreter know which shell is being used.

-----

# Comments & Variables

## Comments

A single line comment is written using a `#`.

```bash
#! /bin/bash
# This is a single line comment
echo "Hello world" # This is also a comment

```

## Variables

> 📌 The name of a variable can contain only letters (`a` to `z` or `A` to `Z`), numbers (`0` to `9`) or the underscore character (`_`). Also, the variable name cannot start with a number.

### System Variables

- Created and maintained by the Linux/Unix OS.
- Conventionally these are written using uppercase.
- **Examples of system variables** -
    
    ```bash
    #! /bin/bash
    echo "Location of bash : $BASH"
    echo "Bash Version  : $BASH_VERSION"
    echo "Path to the home directory (/home/user) : $HOME"
    echo "Present working directory : $PWD"
    ```
    
    ```bash
    $ ./system-variables.sh 
    Location of bash (/bin/bash) : /bin/bash
    Bash Version  : 4.4.20(1)-release
    Path to the home directory (/home/user) : /home/shathin
    Present working directory : /mnt/g/Dev/Linux-Subsystem/shell-scripting
    ```
    
### User Variables

- Created by the user.
- Conventionally these are writting using lowercase.
- Defining and echoing a variable
    
    ```bash
    #! /bin/bash
    my_var=10 # don't put a whitespace on either side of equal symbol (=)
    echo The value is $my_var 
    ```
    
    ```bash
    $ ./user-defined-variable.sh 
    The value is 10
    ```

### Deleting a variable

The `unset` command can be used to delete a variable.

**Example**:

```bash
#! /bin/bash
my_var=10
echo "Value: $my_var"

unset my_var
echo "Value: $my_var"
```

```bash
$ ./delete-variables.sh 
Value: 10
Value:
```

### Arrays

- Arrays are defined as follows: `array_var=(val1 val2 ... valn)`.
- An element of the array can be accessed via its index i.e, `$array_var[index]`
- Using the index, an element can be updated or can be added to the array (see example).
- All the elements of the array can be obtained using `${array_var[@]}`
- The indexes of the all the elements in the array can be obtained using `${!array_var[@]}`
- The length of the array can be obtained using `${#array_var[@]}`

> ⚠️ An important thing to note about arrays here is that the elements of the array need not be present in successive indicies i.e., an index in-between two elements can have no element. For example - we can have an array with elements present only in the odd-index positions or even-index position or at random a random index. (See example)

- An element of an array can be deleted using the `unset` command.

**Example**: 

```bash
#! /bin/bash

# creating an array
os=('ubuntu' 'windows' 'kali')

# accessing the first element and printing it
echo "1st element : ${os[0]}"
# updating the second element
os[1]='windows-10'
# adding an element to the 10th position in the array
os[9]='mac'
# remove an element from the array array
unset os[2]

# print all the elements
echo "Elements : ${os[@]}" 
# print the indexes of the elements
echo "Indices : ${!os[@]}"
# print length of the array
echo "Length : ${#os[@]}"
```

```bash
$ ./arrays.sh 
1st element : ubuntu
Elements : ubuntu windows-10 mac
Indices : 0 1 9
Length : 3
```

-----

# User Input & Command-line Arguments

### Reading user input

We use the `read` command to accept the user's input from the keyboard.

**Example**: 

1. Accepting a user's name
    
    ```bash
    #! /bin/bash
    echo "Enter your name: "
    read name
    echo "Hello there $name"
    ```
    
    In the above example the `read` command stores the input from the keyboard into the variable `name`.
    
2. Accepting multiple inputs
    
    ```bash
    #! /bin/bash
    echo "Enter the names of your mother and father : "
    read father mother
    echo "Hello there Mr. $father and Mrs $mother"
    ```
    
    ```bash
    $ ./inputs.sh
    Enter the names of your mother and father : 
    Roger Rouge
    Hello there Mr. Roger and Mrs Rouge
    ```
    
    Don't press the enter key after entering the value into the first variable, instead press space and enter the value into the next variable. 
    
3. In the above two examples we can observe that the prompt text (`Enter your name`) and the input promt are on separate lines. If we want them to come on the same line we can use the `read -p` command.
    
    ```bash
    #! /bin/bash
    read -p  "Enter the names of your mother and father : " father mother
    echo "Hello there Mr. $father and Mrs $mother"
    ```
    
    ```bash
    $ ./hello-world.sh
    Enter the names of your mother and father : Roger Rouge
    Hello there Mr. Roger and Mrs Rouge
    ```
    
4. To obscure the text during input then use the `-s` option 
    
    ```bash
    #! /bin/bash
    read -sp "Enter your Password: " $password
    echo "Your password is: $password"
    ```
    
    ```bash
    $ ./obscure-text.sh
    Enter your Password: 
    Your password is: mypassword
    ```
    
5. If no variable is given along with the `read` command then it stores it in the `$REPLY` variable by default.
    
    ```bash
    #! /bin/bash
    read 
    echo "Your text is: $REPLY"
    ```
    
    ```bash
    $ ./default-input.sh
    Hello 
    Your text is: Hello
    ```
    
6. You can use `read -a` command to store the input in an array
    
    ```bash
    #! /bin/bash
    echo "Enter the names" 
    read -a names
    echo "Hello there ${names[0]} and ${names[1]}"
    ```
    
    ```bash
    $ ./array-input.sh
    Enter the names
    Dragon Luffy
    Hello there Dragon and Luffy
    ```
    
### Passing arguments to a script

- The arguments passed to a shell script is stored in the variables `$1`, `$2`, and so on. The name of the script in stored in the `$0` variable.
    
    ```bash
    #! /bin/bash
    echo "The arguments are : " $1 $2 $3 
    ```
    
    ```bash
    $ ./command-line-argument-1.sh hello there world
    "The arguments are :
    Argument 1 :  hello
    Argument 2 :  there
    Argument 3 :  world
    ```
    
- To accept the arguments as array we can use the `$@` variable. This variable holds the arguments in the form of an array. An important thing to note here is that the name of the script will not be store in the array and hence we should start accessing the array from index `0`.
The `$#` variable contains the number of command-line arguments passed to the script.
    
    ```bash
    #! /bin/bash
    args=("$@")
    echo "The arguments are : "
    echo "Argument 1 :  ${args[0]}"
    echo "Argument 2 :  ${args[1]}"
    echo "Argument 3 :  ${args[2]}"
    echo "All the arguments : $@"
    echo "Number of arguments : $#"
    ```
    
    ```bash
    ./command-line-argument-2.sh hello there world
    The arguments are : 
    Argument 1 :  hello 
    Argument 2 :  there
    Argument 3 :  world
    All the arguments : hello there world
    Number of arguments : 3
    ```

-----

# Operations

> ⚠️ The space after the opening & before the closing paranthesis / bracket is very important. Not adding a white space will cause an error.

- **String Comparisons**
    - `[[ $s1 = $s2 ]]` or `[[ $s1 == $s2 ]]` → Compare if two strings are equal.
    - `[[ $s1 != $s2 ]]` → Compare if two strings are not equal.
    - `[[ $s1 < $s2 ]]<` → Is `$s1` less than `$s2`, in ASCII alphabetical order.
    - `>` → Is `$s1` greater than `$s2`, in ASCII alphabetical order.
    - `[ $s1 ]`  → True if `$s1` is not empty.
    - `[ -n $s1 ]` → True if length of `$s1` is greater than `0`.
    - `[ -z $s1 ]` → True if length of `$s1` is equal to `0`.

- **Number Comparisons**
    - `[ n1 -eq n2 ]` → True if `$n1` equal to`$n2`.
    - `[ n1 -ne n2 ]` → True if `$n1` is not equal to `$n2` .
    - `[ n1 -ge n2 ]` → True if `$n1` is greater than or equal to `$n2`.
    - `[ n1 -gt n2 ]` → True if `$n1` is greater than `$n2`.
    - `[ n1 -le n2 ]` → True if `$n1` is less than or equal to `$n2`.
    - `[ n1 -lt n2 ]` → True if `$n1` is less than `$n2`.

- **File Test Operator**:
    - `[ -e $file_name]` → Test if a file named `file_name` exists.
    - `[ -f $file_name]` → Test if a file named `file_name` exists and is a regular file or not.
    - `[ -b $file_name]` → Test if a file named `file_name` exists and is a block special file or not.
    - `[ -c $file_name]` → Test if a file named `file_name` exists and is a character special file or not.
    - `[ -d $dir]` → Test if a directory named `dir` exists.
    - `[ -s $file_name]` → Test if a file named `file_name` is empty.
    - `[ -r $file_name]` → Test if a file named `file_name` has read permission.
    - `[ -w $file_name]` → Test if a file named `file_name` has write permission.
    - `[ -x $file_name]` → Test  if a file named `file_name` has execute permission.

- **Logical Operator**
    - There's three ways to implement the `AND` operation
        - `[ expression1 ] && [ expression2 ]`
        - `[ expression1 -a expression2 ]`
        - `[[ expression1 && expression2 ]]`
    - There's three ways to implement the `OR` operation
        - `[ expression1 ] || [ expression2 ]`
        - `[ expresson1 -o expression2 ]`
        - `[[ expression1 || expression2 ]]`

- **Integer Arithmetic Operator**

    > 📌 The below mentioned operators only works on integer type numbers.
    
    - `$(( num1 + num2 ))`  or `$(expr $num1 + $num2 )` → Addition
    - `$(( num1 - num2 ))`  or `$(expr $num1 - $num2 )`→ Subtraction
    - `$(( num1 * num2 ))`  or `$(expr $num1 \* $num2 )`→ Multiplication

      > ⚠️ In the second method i.e., `expr`, do not miss the escape character `\`.
    
    - `$(( num1 / num2 ))`  or `$(expr $num1 / $num2 )`→ Division
    - `$(( num1 % num2 ))`  or `$(expr $num1 % $num2 )`→ Modulus

- **Floating Point Arithmetic Operation**
    
    To perform floating point arithmetic operations we need to use a tool called `bc`. The way to use the `bc` command is to pass the expression as an input to the command.
    
    - `"$num1+$num2" | bc` → Floating point Addition
    - `"$num1-$num2" | bc` → Floating point Subtraction
    - `"$num1*$num2 "| bc` → Floating point Multiplication
    - `"scale=x;$num1/$num2" | bc` → Floating point Division
    By default the `bc` command will not give any decimal output i.e., `20.5/5 = 4`. To be able to get the decimal part of the output we have to set the `scale` of the output i.e., `scale=2;20.5/5 = 4.10`.
    - `"$num1%$num2" | bc` → Floating point Modulus
    
    We use the `-l` option with the `bc` command to enable the math library.
    
    - `"$num1^$num2" | bc -l` → Exponentiation
    - `"scale=x;sqrt($num1)" | bc -l` → Square root

    > 💡 The `bc` command has a lot more features. Check out its `man` page to know more.

- **Increment & Decrement Operators**
    - `$(( n++ ))` →Post Increment
    - `$(( n-- ))` →Post Decrement
    - `$(( ++n ))` →Pre Increment
    - `$(( --n ))` →Pre Decrement

-----

# Conditonal & Loop Statements

## Conditional Statements

### `if` statement

```bash
if [ expression ] 
then 
	statement
fi
```

### `if-else` statement

```bash
if [ expression ]
then
   statement1
else
   statement2
fi
```

### `else-if` ladder

```bash
if [ expression1 ]
then
   statement1
elif [ expression2 ]
then
   statement2
else
   statement3
fi
```

### Nested `if`

```bash
if [ expression1 ]
then
   statement1
else
   if [ expression2 ]
   then
      statement2
   fi
fi
```

### `switch` statement

```bash
case "$var"  in
   Pattern-1) Statement 1;;
   Pattern-2) Statement 1;;

   Pattern-n) Statement n;;
esac
```

```bash
# example

CARS="bmw"
  
#Pass the variable in string 
case "$CARS" in 
    #case 1 
    "mercedes") echo "Headquarters - Affalterbach, Germany" ;; 
      
    #case 2 
    "audi") echo "Headquarters - Ingolstadt, Germany" ;; 
      
    #case 3 
    "bmw") echo "Headquarters - Chennai, Tamil Nadu, India" ;; 

		# any other case i.e., default case
		* ) echo "N/A" ;;
esac
```

## Looping statements

### `while` loop

Here `statements` are executed when the `condition` holds true.

```bash
while [ condition ]
do 
	statements
done
```

Example: Reading the contents of a file using `while` and I/O redirection and pipes (respectively)

```bash
#! /bin/bash
# using I/O redirection
while read p
do 
	echo "$p"
done < file.txt
```

```bash
#! /bin/bash
# using pipes
cat file.txt | while read p
do 
	echo "$p"
done
```

### `until` loop

Here the `statements` are executed only when the `condition` is false.

```bash
until [ condition ]
do 
	statements
done
```

### `for` loop

```bash
for (( EXP1; EXP2; EXP3 ))
do
	commands
done
```

```bash
for variable in 1 2 3 ... N
do 
	commands
done
```

```bash
for variable in file1 file2 file3
do 
	commands on $variable
done
```

```bash
for output in $(linux-commands-here)
do
	commands on $output
```

**Examples**: 

```bash
#! /bin/bash
for iter in 1 2 3 4 5
do 
	echo "$iter"
done
```

```bash
#! /bin/bash
# this will work only for bash version greater than 4.0
# range is specified using {START..END..INCREMENT} 
# range is inclusive of START & END
# INCREMENT can be skipped - if skipped defaults to 1
for iter in {1..10}
do 
	echo "$iter"
done
```

```bash
#! /bin/bash
for (( i=0; i<5; i++ ))
do
	echo $i
done
```

```bash
#! /bin/bash
for commands in ls pwd date
do
	echo "---$command---" # print command name
	$command # execute command
done
```
