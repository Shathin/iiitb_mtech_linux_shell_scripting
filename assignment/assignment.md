
📌 The following content is in the following format -   
- **Question** - The given question.  
- **Answer** - A short description about the script.  
- **Code block 1** - The code editor - Shows the script's code.  
- **Code block 2** - The terminal - Shows the output(s) of the script.

---

# Question 1

**[Question]** Write a shell script to count the number of block device files in `/dev` directory. 

**[Answer]** The shell script `1-counting-block-files.sh` uses three commands - `ls`, `grep` and `wc` to count the number of block files in the `/dev` directory. The shell script does not take in any command line argument nor does it take any user input (through `read`). 

```bash
#! /bin/bash
echo -e "The number of block device files in the /dev directory is: \c"
ls -la /dev | grep ^b | wc -l
```

```bash
# Executing the shell script 
$ ./1-counting-block-files.sh
The number of block device files in the /dev directory is: 18

```

---

# Question 2

**[Question]** Write a shell program that checks the number of command line arguments and echoes an error message if there are not exactly three arguments or echoes the arguments themselves if there are three. 

**[Answer]** The shell script `2-cmd-line-args.sh` accepts command line arguments. It uses the `$#` variable to count the number of command line arguments passed to the script and then access the arguments passed to it using the `$@` variable. 

```bash
#! /bin/bash
if [ $# -ne 3 ]
then
    echo "ERROR: More / less than 3 command line arguments were passed to this script!"
else
    args=("$@")
    echo "Argument 1: ${args[0]}"
    echo "Argument 2: ${args[1]}"
    echo "Argument 3: ${args[2]}"
fi
```

```bash
$ # Executing the shell script
$ # Output 1 - No errors
$ /2-cmd-line-args.sh a b c
Argument 1: a
Argument 2: b
Argument 3: c
$ # Output 2 - Error
$ ./2-cmd-line-args.sh 
ERROR: More / less than 3 command line arguments were passed to this script!
```

---

# Question 3

**[Question]** Write a shell program called `new_files` that will accept a variable number of command line arguments. The shell program will create a new file associated with each command line argument and echo a message that notifies the user as each file is created. 

**[Answer]** The script `3-create-new-files.sh` accepts the file names (with extension) as the command line arguments to the script. It uses the `touch` command to create the new files in the current working directory and echoes a message when each file is created. 

```bash
#! /bin/bash
if [ $# -gt 0 ]
then 
    file_names=("$@")
    for (( iter=0; iter<$#; iter++ ))
    do
        touch ${file_names[iter]}
        echo "The file ${file_names[iter]} has been created..."
    done
else 
    echo "Please provide file names as the argument to this script!"
fi
```

```bash
$ # Executing the shell script
$ # Output 1 - No errors
$ ./3-create-new-files.sh file1.txt file2.txt
The file file1.txt has been created...
The file file2.txt has been created...
$ # Output 2 - Error
$ ./3-create-new-files.sh 
Please provide file names as the argument to this script!
```

---

# Question 4

**[Question]** Create a directory called `.recyclebin` in your home directory. Write a shell program called `myrm` that will move all of the files you delete into the `.recyclebin` directory, your wastebasket. This is a useful tool which will allow restoration of files after they have been removed. **Remember, the UNIX system has no undelete capability.** 

**[Answer]** The script `4-myrm.sh` accepts the names of the file(s) to be moved to the recycle bin (`~/.recyclebin`). The script creates this directory if it doesn't exist. 

```bash
#! /bin/bash
mkdir -p ~/.recyclebin 
if [ $# -gt 0 ]
then 
    files=("$@")
    for file in ${files[@]}
    do 
        if [ -e $file ]
        then 
            mv $file ~/.recyclebin
            echo "Your file $file have been moved to the recycle bin! You can find it in ~/.recyclebin"
        else 
            echo "The file $file doesn't exist!"
        fi 
    done
else
    echo "Please provide the file names to be deleted as the argument to this script!"
fi
```

```bash
$ # Creating a sample file for testing
$ touch file1 file2 file3 file4
$ # Executing the script
$ # Output 1
$ ./4-myrm.sh file1 file2 file3 file4
Your file file1 have been moved to the recycle bin! You can find them it in ~/.recyclebin
Your file file2 have been moved to the recycle bin! You can find them it in ~/.recyclebin
Your file file3 have been moved to the recycle bin! You can find them it in ~/.recyclebin
Your file file4 have been moved to the recycle bin! You can find them it in ~/.recyclebin
$ # Output 2 - Trying to delete a file that doesn't exist
$ ./4-myrm.sh filex
The file filex doesn't exist!
$ # Output 3 - No file names passed
$ ./4-myrm.sh 
Please provide the file names to be deleted as the argument to this script!

```

---

# Question 5

**[Question]** Write a script that uses `find` to look for a file and echo a suitable message if the file is not found. You must not store the output of the find to a file.

**[Answer]** `5-find-file.sh`

```bash
#! /bin/bash
if [ $# -gt 0 ]
then 
    args=("$@")
    for (( iter=0; iter<$#; iter++))
    do 
        result=$(find ${args[iter]} 2> /dev/null)
        # The '2> /dev/null' is used to throw away the error message
        if [[ $result == ${args[iter]} ]]
        then 
            echo "File ${args[iter]} found!"
        else 
            echo "File ${args[iter]} not found!"
        fi
    done
else
    echo "Please pass the file names to be searched as the argument to this script!"
fi
```

```bash

$ # Executing the file
$ # Output 1
$ ./5-find-file.sh 4-myrm.sh 3-create-new-files.sh 
File 4-myrm.sh found!
File 3-create-new-files.sh found!
$ # Output 2
$ ./5-find-file.sh file1 file2
File file1 not found!
File file2 not found!
$ # Output 3 - No arguments passed
$ ./5-find-file.sh
Please pass the file names to be searched as the argument to this script!
```

---

# Question 6

**[Question]** Write a script which will give 4 choices to the user 

1. `ls` 

2. `pwd`

3. `who`

4. `exit` and execute the command as per the users choice.

**[Answer]** The script `6-basic-command-choice.sh` does not accept any command line arguments but keeps asking the user to input their choice (using `read`) until they choose to exit. 

```bash
#! /bin/bash

echo "You have the following choices : "
echo "1. List the files in pwd - ls"
echo "2. Check your present working directory - pwd"
echo "3. Who are the users currently logged in - who"
echo "4. Exit this script"

echo -e "Enter your choice: \c"
read user_choice

while [ $user_choice -ne 4 ]
do 
    echo 
    case $user_choice in 
        1) 
            echo "=================ls=================="
            ls
            echo "=====================================" ;;
        2) 
            echo "=================pwd================="
            pwd
            echo "=====================================" ;;
        3) 
            echo "=================who================="
            who
            echo "=====================================" ;;
        * ) echo "====================================="
            echo "Invalid choice!" 
            echo "=====================================" ;;
    esac

    echo -e "\nChoices: 1. ls || 2. pwd || 3. who || 4. exit"
    echo -e "Enter your choice: \c"
    read user_choice
done
```

```bash
$ # Executing the shell script
$ ./6-basic-command-choice.sh 
You have the following choices : 
1. List the files in pwd - ls
2. Check your present working directory - pwd
3. Who are the users currently logged in - who
4. Exit this script
Enter your choice: 1

=================ls==================
10.sh                       15                         4-myrm.sh                  9.sh
11-space-used-by-dir.sh     16                         5-find-file.sh             file2.txt
12-stderr.sh                1-counting-block-files.sh  6-basic-command-choice.sh
13-multiplication-table.sh  2-cmd-line-args.sh         7.sh
14-greetings.sh             3-create-new-files.sh      8.sh
=====================================

Choices: 1. ls || 2. pwd || 3. who || 4. exit
Enter your choice: 2

=================pwd=================
/media/shathin/Data/Dev/IIITB/Assignments [Prep Term]/linux-shell-scripting
=====================================

Choices: 1. ls || 2. pwd || 3. who || 4. exit
Enter your choice: 3

=================who=================
shathin  :0           2020-09-01 09:28 (:0)
=====================================

Choices: 1. ls || 2. pwd || 3. who || 4. exit
Enter your choice: 5

=====================================
Invalid choice!
=====================================

Choices: 1. ls || 2. pwd || 3. who || 4. exit
Enter your choice: 4
```

---

# Question 7

**[Question]** Write an interactive file-handling shell program that offers the user choice of copying, removing, rename. Once the user has made a choice, the program should ask the user for the necessary information, such as the file name, new name. 

**[Answer]** The script `7-file-handling.sh` does not accept any command line arguments but keeps asking the user to input their choice (using `read`) until they choose to exit. 

```bash
#! /bin/bash

echo "File handling operations: "
echo "1. Copy a file"
echo "2. Remove a file"
echo "3. Rename a file"
echo "4. Exit"
echo -e "Enter your choice: \c"
read user_choice

while [ $user_choice -ne 4 ]
do 
    echo 
    case $user_choice in 
        1) 
            echo "===========Copy==========="
            read -p "Enter the Source File's name: " source_file_name
            read -p "Enter the Destination File's name: " destination_file_name
            cp -i $source_file_name $destination_file_name
            echo "==========================";;
        2) 
            echo "==========Remove=========="
            read -p "Enter the File's name: " file_name
            rm -i $file_name
            echo "==========================";;
        3) 
            echo "==========Rename==========="
            read -p "Enter the Source File's name: " source_file_name
            read -p "Enter the File's new name: " new_file_name
            mv -i $source_file_name $new_file_name
            echo "==========================";;
        *) 
            echo "=========================="
            echo "Invalid Choice!"
            echo "==========================";;
    esac

    echo -e "\nChoices: 1. Copy || 2. Remove || 3. Rename || 4. exit"
    echo -e "Enter your choice: \c"
    read user_choice
done
```

```bash
$ # Creating a sample file
$ touch file1
$ # Executing the script
$ ./7-file-handling.sh 
File handling operations: 
1. Copy a file
2. Remove a file
3. Rename a file
4. Exit
Enter your choice: 1

===========Copy===========
Enter the Source File's name: file1
Enter the Destination File's name: file2
==========================

Choices: 1. Copy || 2. Remove || 3. Rename || 4. exit
Enter your choice: 2

==========Remove==========
Enter the File's name: file2
rm: remove regular empty file 'file2'? y
==========================

Choices: 1. Copy || 2. Remove || 3. Rename || 4. exit
Enter your choice: 3

==========Rename===========
Enter the Source File's name: file1
Enter the File's new name: file-1
==========================

Choices: 1. Copy || 2. Remove || 3. Rename || 4. exit
Enter your choice: 5

==========================
Invalid Choice!
==========================

Choices: 1. Copy || 2. Remove || 3. Rename || 4. exit
Enter your choice: 4
```

---

# Question 8

**[Question]** Write shell script that takes a login name as command – line argument and reports when that person logged in. 

**[Answer]** The script `8-user-logged-in.sh` accepts the name of user as the command line argument and uses the `w` and `grep` command to find if the user is logged in.

```bash
#! /bin/bash

username=$1
search_result=$(w -h | grep -w ^$username)
if [ `expr length "$search_result"` -gt 0 ]
then
    logged_in_at=$(echo $search_result | awk '{print $4}')
    echo "The user $username has logged in at $logged_in_at"
else 
    echo "User not found / isn't logged in"
fi
```

```bash
$ # Executing the script
$ # Output 1
$ ./8-user-logged-in.sh shathin
The user shathin has logged in at 09:28
$ # Output 2
$ ./8-user-logged-in.sh ryu
User not found / isn't logged in
```

---

# Question 9

**[Question]** Write a shell script that accepts a starting and ending line numbers and file name (in that order) as arguments and displays all the lines between the given line numbers. 

**[Answer]** 

```bash
#! /bin/bash

starting_line_no=$1
ending_line_no=$2
file_name=$3

head -n $ending_line_no $file_name | tail -n $(( ending_line_no - starting_line_no + 1 ))
```

```bash
$ # Executing the script
$ ./9-printing-lines.sh 5 7 9-printing-lines.sh 
starting_line_no=$1
ending_line_no=$2
file_name=$3
```

---

# Question 10

**[Question]** Write a script to backup a given directory to a given file name in your home directory. Both, the directory name and the backup file has to be passed as command line input. Design the script with suitable exception handling.

**[Answer]** The script `10-backup.sh` uses the `tar` and `gzip` commands for archiving and compressing the directory. It then moves this to the home directory. The name of the directory to be backed up is passed as the command line arguement to the script followed by the name of the backup file.

```jsx
#! /bin/bash

dir_to_backup=$1
backup_file=$2

if [ $# -eq 2 ] 
then
    tar -cf ~/$backup_file.tar $dir_to_backup
    gzip ~/$backup_file.tar
else 
    echo "Invalid number of command line arguements. You need to specify <file_to_backup> & <backup_file> names (in that order)"
fi
```

```bash
$ # Executing the script
$ ./10-backup.sh . lss
shathin@shathin-ubuntu:linux-shell-scripting$ ls ~/
 Desktop     lss.tar.gz     Public                
 Documents   Music          Templates    
 Downloads   Pictures       Videos       
```

---

# Question 11

**[Question]** Write a script to check how much space is used by each directory of a given file system. The name of the file system has to be provided from the command line parameter. 

**[Answer]** The script `11-space-used-by-dir.sh` uses the `findmnt` and `du` command to get the amount of space used by each directory in the file system. The name of the filesystem like `/dev/sda4` is passed as the command line argument to the script.

```bash
#! /bin/bash

file_system=$1
mount=$(findmnt -o TARGET -n $file_system)
if [ `expr length "$mount"` -gt 0 ]
then 
	  du -c -s -h $mount 2> /dev/null
else 
    echo "File system not found. Make sure it exists and that you've written the correct name (ex: /dev/sda4)"
fi
```

```bash
$ # Executing
$ ./11-space-used-by-dir.sh /dev/sda3
MOUNT : /
84G     /
84G     total
```

---

# Question 12

**[Question]** Write a script in `/root/myscript.sh` according to the following criteria:

1. If you search for the IIT the output is NIT
2. If you search for NIT the output is IIT
3. If you search any other keyword or not give any input, the output is `STDERR` should be displayed.

**[Answer]** The script `12-stderr.sh` accepts the words IIT, NIT or anythin else as the command line argument(s).

```jsx
#! /bin/bash
if [ $# -eq 0 ]
then 
    echo "Please give some input!"
else 
    inputs=("$@")
    for (( iter=0; iter<$#; iter++ ))
    do
        if [[ ${inputs[iter]} ==  "IIT" ]]
        then
            echo "NIT"
        elif [[ ${inputs[iter]} ==  "NIT" ]]
        then 
            echo "IIT"
        else
            echo "Invalid Keyword"
        fi
    done
fi
```

```bash
$ # Executing the script
$ # Output 1
$ ./12-stderr.sh NIT IIT IIIT
IIT
NIT
Invalid Keyword
$ # Output 2
$ ./12-stderr.sh 
Please give some input!
```

---

# Question 13

**[Question]** Write a shell script to print a multiplication table. 

**[Answer]** The script `13-multiplication-table.sh` accepts the multiplicand and the number of multiplier (in that order) as the command line arguments.

```bash
#! /bin/bash
number=$1
length_of_multiplication=$2

for (( iter=1; iter<=$length_of_multiplication; iter++ ))
do
    printf "| %3d * %3d = %3d |\n" $number $iter $(( number * iter ))
done
```

```bash
$ # Executing the script
$ ./13-multiplication-table.sh 10 10
|  10 *   1 =  10 |
|  10 *   2 =  20 |
|  10 *   3 =  30 |
|  10 *   4 =  40 |
|  10 *   5 =  50 |
|  10 *   6 =  60 |
|  10 *   7 =  70 |
|  10 *   8 =  80 |
|  10 *   9 =  90 |
|  10 *  10 = 100 |
```

---

# Question 14

**[Question]** Write a shell script to print, "Good Morning/Afternoon/Evening" based on the current system time.

**[Answer]** The script `14-greetings.sh` does not accept any arguments.

```bash
#! /bin/bash

hour=$(date "+%H")
if [ $hour -gt 5 ] && [ $hour -lt 12 ]
then 
    echo "Good Morning! "
elif [ $hour -ge 12 ] && [ $hour -lt 17 ]
then
    echo "Good Afternoon!"
elif [ $hour -ge 17 ] && [ $hour -lt 20 ]
then
    echo "Good Evening!"
else 
    echo "Good Night!"
fi
```

```bash
$ # Executing the script
$ # The time at execution is 11:26
$ ./14-greetings.sh 
	Good Morning!
```

---

# Question 15

**[Question]** **`SED`** - Write a shell script to perform the following (input file `example` will be given).

1. For a given file, find all the lines containing our search pattern.
2. List the lines not containing the search string
3. Matching lines starting with a given pattern and ending in a second pattern
4. Print a file starting from a certain line until to the end of file.
5. Search a given pattern in a file and replace with a new pattern and display the file.
6. Insert a given string at the beginning of each line of the file.
7. Insert a given string at the end of each line of the file

**[Answer]**

- Contents of the `example` file
    
    ```
    This is the first line of an example text.
    It is a text with erors.
    Lots of erors.
    So much erors, all these erors are making me sick.
    This is a line not containing any errors.
    This is the last line.
    ```
    
1. Find all the lines containing our search pattern - The script `15a.sh` accepts the pattern to search and the file name (in that order).
    
    ```bash
    #! /bin/bash
    
    search_pattern=$1
    file=$2
    echo $(sed -n '/'$search_pattern'/p' $file)
    ```
    
    ```bash
    $ # Executing the script
    $ $ ./15a.sh eror example
    It is a text with erors. Lots of erors. So much erors, all these erors are making me sick.
    ```
    
2. Lines not containing the search string - The script `15b.sh` accepts the pattern to search and the file name (in that order). 
    
    ```bash
    #! /bin/bash
    
    search_pattern=$1
    file=$2
    echo $(sed '/'$search_pattern'/d' $file)
    ```
    
    ```bash
    $ # Executing the script
    $ ./15b.sh eror example
    This is the first line of an example text. This is a line not containing any errors. This is the last line.
    ```
    
3. Lines starting with a given pattern and ending in a second pattern - The script `15c.sh` accepts the starting and ending pattern to search and the file name (in that order).
    
    ```bash
    #! /bin/bash
    
    starting_pattern=$1
    ending_pattern=$2
    file=$3
    echo "$(sed -n '/^'$starting_pattern'.*'$ending_pattern'.$/p' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./15c.sh It erors example
    It is a text with erors.
    ```
    
4. Print starting from a certain line until to the end of file - The script `15d.sh` accepts the starting line number and the file name (in that order).
    
    ```bash
    #! /bin/bash
    
    starting_line=$1
    file=$2
    echo "$(sed -n ''$starting_line',$'p $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./15d.sh 5 example
    This is a line not containing any errors.
    This is the last line.
    ```
    
5. Find and replace pattern - The script `15e.sh` accepts the search pattern, replace pattern and file name (in that order).
    
    ```bash
    #! /bin/bash
    
    search_pattern=$1
    replace_pattern=$2
    file=$3
    echo "$(sed 's/'$search_pattern'/'$replace_pattern'/g' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./15e.sh eror error example
    This is the first line of an example text.
    It is a text with errors.
    Lots of errors.
    So much errors, all these errors are making me sick.
    This is a line not containing any errors.
    This is the last line.
    ```
    
6. Insert a given string at the beginning of each line - The script `15f.sh` accepts the string to prepend and the file name (in that order).
    
    ```bash
    #! /bin/bash
    
    string=$1
    file=$2
    echo "$(sed 's/^/'$string' /' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./15f.sh PP example
    PP This is the first line of an example text.
    PP It is a text with erors.
    PP Lots of erors.
    PP So much erors, all these erors are making me sick.
    PP This is a line not containing any errors.
    PP This is the last line.
    ```
    
7. Insert a given string at the end of each line - The script `15g.sh` accepts the string to append and file name (in that order).
    
    ```bash
    #! /bin/bash
    
    string=$1
    file=$2
    echo "$(sed 's/$/'$string' /' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./15g.sh dd example
    This is the first line of an example text.dd 
    It is a text with erors.dd 
    Lots of erors.dd 
    So much erors, all these erors are making me sick.dd 
    This is a line not containing any errors.dd 
    This is the last line.dd
    ```
    

---

# Question 16

**[Question]**  **`AWK`** – Write a Shell script to (The input file `employee.txt` will be given)

1. Display a given file.
2. Print the lines which match with a given pattern.
3. Print only a specific field in the file.
4. Format a given file with Name, Designation, Department and Salary headings and at the end of a file print Report Generated.
5. Find the employees, who has $id>200$.
6. Find the list of employees in a Technology Department.
7. Print the number of employees in Technology Department.

**[Answer]**

- Contents of `example.txt` file
    
    ```bash
    100 Thomas Manager Sales $5,000
    200 Jason Developer Technology $5,500
    300 Sanjay Sysadmin Technology $7,000
    400 Nisha Manager Marketing $9,500
    500 Randy DBA Technology $6,000
    ```
    
1. Display a given file - The script `16a.sh` accepts the name of the file to be displayed.
    
    ```bash
    #! /bin/bash
    
    file=$1
    echo "$(awk '{print;}' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./16a.sh example.txt
    100 Thomas Manager Sales $5,000
    200 Jason Developer Technology $5,500
    300 Sanjay Sysadmin Technology $7,000
    400 Nisha Manager Marketing $9,500
    500 Randy DBA Technology $6,000
    ```
    
2. Print the lines which match with a given pattern - The script `16b.sh` accepts the name of the file and the pattern(s) in that order.
    
    ```bash
    #! /bin/bash
    
    args=("$@")
    file=${args[0]}
    patterns='/'${args[1]}'/'
    for (( iter=2; iter<$#; iter++ )) 
    do
        newpattern='||/'${args[iter]}'/'
        patterns=$patterns$newpattern
    done
    echo "$(awk ''$patterns'' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./16b.sh example.txt Thomas Nisha Jason
    100 Thomas Manager Sales $5,000
    200 Jason Developer Technology $5,500
    400 Nisha Manager Marketing $9,500
    ```
    
3. Print only a specific field in the file - The script `16c.sh` accepts the name of the file and the field numbers (in that order).
    
    ```bash
    #! /bin.bash
    
    args=("$@")
    file=${args[0]}
    fields='$'${args[1]}''
    for (( iter=2; iter<$#; iter++ )) 
    do
        newfield=',$'${args[iter]}''
        fields=$fields$newfield
    done
    echo "$(awk '{print '$fields';}' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./16c.sh example.txt 1 2 3 
    100 Thomas Manager
    200 Jason Developer
    300 Sanjay Sysadmin
    400 Nisha Manager
    500 Randy DBA
    ```
    
4. Format a given file with Name, Designation, Department and Salary headings and at the end of a file print Report Generated - The script `16d.sh` accepts the file name.
    
    ```bash
    #! /bin/bash
    
    file=$1
    echo "$(awk 'BEGIN {print "Name\tDesignation\tDepartment\tSalary";} {print $2,"\t",$3,"\t",$4,"\t",$NF;} END {print "Report Generated\n--------------";}' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./16d.sh example.txt 
    Name    Designation     Department      Salary
    Thomas   Manager         Sales   $5,000
    Jason    Developer       Technology      $5,500
    Sanjay   Sysadmin        Technology      $7,000
    Nisha    Manager         Marketing       $9,500
    Randy    DBA     Technology      $6,000
    Report Generated
    --------------
    ```
    
5. Find the employees, who has $id>200$ - The script `16e.sh` accepts the name of the file and the field number for the ID column (in that order)
    
    ```bash
    #! /bin/bash
    
    file=$1
    id_column=$2
    echo "$(awk '$'$id_column'>200' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./16e.sh example.txt 1
    300 Sanjay Sysadmin Technology $7,000
    400 Nisha Manager Marketing $9,500
    500 Randy DBA Technology $6,000
    ```
    
6. Find the list of employees in a Technology Department - The script `16f.sh` accepts the name of the file and the field number for the Department column (in that order)
    
    ```bash
    #! /bin/bash
    file=$1
    tech_column=$2
    echo "$(awk '$'$tech_column' ~/Technology/' $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./16f.sh example.txt 4
    200 Jason Developer Technology $5,500
    300 Sanjay Sysadmin Technology $7,000
    500 Randy DBA Technology $6,000
    ```
    
7. Print the number of employees in Technology Department - The script `16g.sh` accepts the name of the file.
    
    ```bash
    #! /bin/bash
    file=$1
    echo "$(awk 'BEGIN {count=0; } $4 ~/Technology/ { count++; } END {print "No. of employess in Technology dept. = ",count;}'  $file)"
    ```
    
    ```bash
    $ # Executing the script
    $ ./16g.sh example.txt
    No. of employess in Technology dept. =  3
    ```
    
---
