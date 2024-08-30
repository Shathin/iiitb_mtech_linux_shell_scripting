# Basic Commands, I/O Redirection & nano editor

## Basic Commands

### **`man`**

Displays the **user manual** of any command that we can run on the terminal.

**Syntax**: `man [option] command`

> 💡 `$man man` command can be used to obtain the manual for the `man` command.

### `whatis`

Gives one line manual page descriptions.

**Syntax:** `whatis command`

**Example:**
```bash
$ whatis ls
ls (1)           - list directory contents
```

### **`pwd`**

Print name of current/working directory. It prints the path of the working directory, starting from the root.

**Syntax**: `pwd`

**Example**: 
```bash
$ pwd
/home/shathin
```

### **`ls`**

**List** a directory's contents and its properties like *permissions*, *owner*, etc.

**Syntax**: `ls [option] [directory]`

**Examples**: 

1. `ls` with no `option` or `directory` mentioned
    
    ```bash
    $ ls
    Desktop     Downloads   Pictures   Public   Templates
    Documents   Music       Videos
    ```
    
2. `ls` with only `directory` mentioned.
    
    ```bash
    $ ls Downloads
    code1.html  executable.deb  text1.txt
    ```
    
3. `ls` with the  `-l` option (long listing format) 
    
    ```bash
    $ ls -l
    total 36
    drwxr-xr-x 2 shathin shathin 4096 Aug 19 21:09  Desktop
    drwxr-xr-x 2 shathin shathin 4096 Aug 20 06:49  Documents
    drwxr-xr-x 2 shathin shathin 4096 Aug 19 22:06  Downloads
    drwxr-xr-x 2 shathin shathin 4096 Aug 19 21:09  Music
    drwxr-xr-x 3 shathin shathin 4096 Aug 19 21:20  Pictures
    drwxr-xr-x 2 shathin shathin 4096 Aug 19 21:09  Public
    drwxr-xr-x 2 shathin shathin 4096 Aug 19 21:09  Templates
    drwxr-xr-x 2 shathin shathin 4096 Aug 19 22:23  Videos
    ```
    
    1. The *first column* consists of two parts: 
        - The first letter is the file **type** -
            1. `d` - Directory file
            2. `-` - Represents a normal file.
            3. `c` - Character file (special file)
            4. `b` - Binary file (special file)
        - The next 9 characters represent the file **permissions**. `r` is read, `w` is write and `x` is execute permission.
            - First three characters represents the **user** permissions.
            - The next three characters represents the **group** permissions.
            - The last three characters represents the **others** permissions.
    2. The *second column* is the number of symbolic links of the file.
    3. The *third column* specifies the **owner** of the file.
    4. The *fourth column* specifies the **group** to which the owner belongs.
    5. The *fifth column* specifies the **size** of the file.
    6. The *sixth, seventh* and *eight column* specifies the file **modification time**.
4. The *ninth column* specifies the **name** of the file.
5. `ls` with the `-a` option (show all files, including hidden files)
    
    ```bash
    $ ls -a
    .               Desktop     Pictures       .sudo_as_admin_successful
    ..              Documents   .pki           Templates
    .bash_history   Downloads   .PlayOnLinux   Videos
    .bash_logout    .gnupg      .profile       .vscode
    .bashrc         .local      Public                      
    .cache          .mozilla    snap
    .config         Music       .ssh
    
    ```
    
6. Use the `-R` option to list the subdirectories recursively. 
7. Use `-i` or `--inode` to print the  i.e., index number of each file.
8. Saving the output of a `ls` to a file.
    
    ```bash
    $ ls -al > out.txt
    ```

### **`cd`**

Change the current working directory.

**Syntax:** `cd [options] dir`

`dir` is the absolute / relative path to a directory.

**Example:** 

1. Nagivate to `Desktop` from current working directory.
    
    ```bash
    ~$ cd Desktop/
    ~/Desktop$ 
    
    ```

- `.` represents the current working directory
- `..` represents the parent directory of the current working directory
- `~` represents the user's directory i.e., `/home/user/`
- For the directory / file names that contain white space(s) (eg: `My Home`) we cannot directly mention the name of the directory in a command since the space can cause errors. So, to avoid the errors we can do one of the following:
  1. **Escape the space**: Use the backslash `\` character to escape the space (eg: `My\ Home`)
  2. **Add quotes**: Adding single or double quotes around the name of the file will help avoid errors (eg: `'My Home'` or `"My Home"`)


## Printing / Echoing

### `echo`

Display a line of text.

**Syntax:** `echo string`

Example: 

1. Echoing a simple text.
    
    ```bash
    $ echo Hello there...
    Hello there...
    ```
    
2. Echoing the content of a variable.
    
    ```bash
    $ myvar = "Hello there..."
    $ echo $myvar
    Hello there...
    ```
    
3. Echoing the content of a variable along with a custom piece of text
    
    ```bash
    $ x=10
    $ echo "The value of the variable x is $x"
    The value of the variable x is 10
    ```
    
4. To enable interpretation of backslash escapes like `\n` or `\t` use the `-e` option.
    
    ```bash
    $ echo -e "Some \text"
    Some    ext
    ```
    
    Some escape sequences:
    1. `\\` backslash
    2. `\b` backspace
    3. `\n` new line
    4. `\t` horizontal tab
    
### `cat`

Concatenate file(s) to standard output.

**Syntax:** `cat [option] [file]`

**Example:** 

1. Using `cat` to echo something that we type. 
   
   In the below code block, the 1st line after the `cat` command is the text entered by the user and the 2nd line is the text that is echoed back. Use `Ctrl+D` to exit from `cat`.
    
    ```bash
    $ cat
    Hello there...
    Hello there...
    ```
    
2. Using `cat` to display the text file `list1.txt`
    
    ```
    list1.txt
    
    list 1 line 1
    list 1 line 2
    
    list 1 line 3
    ```
    
    ```bash
    $ cat list1.txt
    list 1 line 1
    list 1 line 2
    
    list 1 line 3
    ```
    
3. Using `cat` to concatenate and display the output lines of `list1.txt` and `list2.txt`
    
    ```bash
    list2.txt
    
    list 2 line 1
    
    list 2 line 2
    list 2 line 3
    ```
    
    ```bash
    $ cat list1.txt list2.txt
    list 1 line 1
    list 1 line 2
    
    list 1 line 3
    list 2 line 1
    
    list 2 line 2
    list 2 line 3
    ```
    
4. Using `-b` to number non-empty output lines of text file `list1.txt`
    
    ```bash
    $ cat -b list1.txt
    		1 list 1 line 1
    		2 list 1 line 2
    
    		3 list 1 line 3
    ```
    
    Use `-n` option to give numbers to all lines including empty lines.
    


## I/O Redirection

For redirection we use `>` and `>>`. Both will create a file (if it doesn't exist) and write the contents to that file. The difference in their operations is when the output file already exists. 

`>` will overwrite any content in an already exisiting file while `>>` will append the contents to the end of the output file. 

> ⚠️ An important thing to note while using I/O Redirection is that the input file cannot be the output file.

Syntax: `command > output-file` and `command >> output-file`


## Editor

### `nano`

`nano` stands for Nano's ANOther editor. `nano` is a small and friendly editor.

**Syntax to open a file:** `nano file`

**Few shortcuts used withing the `nano` editor:** (Ctrl → `^`)

1. `^X` → Close current file / exit from `nano`
2. `^O` → Write current file to disk
3. `^S` → Save file without prompting.
4. `^K` → Cut text
5. `^U` → Uncut / paste text
6. `^W` → Search forwards for a string or regex.
7. `^\` → Replace a string or regex.

> 💡 More shortcuts can be found in the help screen inside the editor. To access the help screen press `^G`.

----

# Manipulating Files & Directories 

### `touch`

Update the access and modification times of each file to the current time. By default, if the file with the name written in the command  doesn't exist then the file will be created, hence this command is a  simple way to create files.

**Syntax:** `touch [option] file`

**Example:**

1. Using `touch` to create a file named `file.txt`
    
    ```bash
    $ touch file.txt 
    ```
    
2. Using `touch` to change the file modification time to the current time.
    
    ```bash
    $ ls -l
    total 0
    -rwxrwxrwx 1 shathin shathin 0 Aug 20 07:16 file.txt
    $ touch file.txt
    total 0
    -rwxrwxrwx 1 shathin shathin 0 Aug 21 07:17 file.txt
    ```
    
    > 💡 The `-d` option can be used to pass a date string which is to be used for the modification time instead of the current time.

### `mkdir`

Create the directory(ies), if they do not already exist.

**Syntax:** `mkdir [option] directory`

**Example:**

1. Creating a directory `folder` and creating another folder `subfolder` insider `folder`
    
    ```bash
    $ mkdir folder
    $ mkdir folder/subfolder
    ```
    
2. The above example can be shortened using the `-p` or `--parents` option. This option will create both the parent directory and the subdirectory.
    
    ```bash
    $ mkdir -p folder/subfolder
    $ mkdir -p a/b/c/d/e
    ```
    
3. To create multiple subdirectory inside a parent directory we mention the names inside braces `{dir1,dir2,dir3}`
    
    ```bash
    $ mkdir folder/{dir1,dir2,dir3}
    ```

    > ⚠️ There must be no whitespaces between the directory names and the commas


### `rmdir`

Remove the directory(ies), **if they are empty**.

**Syntax:** `rmdir [option] directory`

**Example:**

1. Deleting a directory named `folder`
    
    ```bash
    $ rmdir folder
    ```
    
2. To recursively remove a directory and its sub directories we can use the `-p`. In the below example our directory structure is `a/b/c`
    
    ```bash
    $ rmdir -p a/b/c
    ```

### `rm`

Remove (unlink) the file(s).

**Options**:

1. `-r` : Recursively delete the entire contents of the directory including the directory itself.
2. `-i` : Prompt before every removal
3. `-f` : Ignore nonexistent files and arguments, never prompt

### `cp`

Copy source to destination, or multiple sources to directory. If the destination file doesn't exist it will be created, else it will be overwritten. 

**Syntax:**  `cp [option] source destination`

`source` and `destination` can be the absolute or relative path to a file.

**Example:**

1. Copying content of `file1.txt` to a new file `file2.txt`
    
    ```bash
    $ cp file1.txt file2.txt
    ```
    
2. Copying a file `file1.txt` to a directory `dir1`
    
    ```bash
    $ cp file1.txt dir1
    ```
    
3. Using the `-R` or `--recursive` option to copy files from one directory to another.
    
    ```bash
    $ cp -R dir1 dir2
    ```
    
    > ⚠️ If `dir2` **doesn't exist**: The below command will copy the files inside a directory `dir1` to a new directory `dir2` and not copy the directory `dir1`  itself to the new directory `dir2` because our directory `dir2` doesn't exist.  
    > If `dir2` **exists**: If the directory `dir2` already exists then the directory `dir1` itself will be copied into `dir2` hence forming a structure like `dir2/dir1`.

> 💡 If there are any files that are susceptible to overwritting then use the `-i` or `--interactive` option to obtain a prompt before overwritting.

### `mv`

Rename source to destination, or move source(s) to directory. If the destination file doesn't exist it will be created, else it will be overwritten. 

**Syntax:** `mv [option] source destination`  
- `source` and `destination` can be the absolute or relative path to a file.

The way of working of `cp` and `mv` are similar with the difference being that the source remains untouched in the `cp` command while in `mv` the source is moved / renamed.

----

# File / Directory Permissions

### `chmod`

Change file mode bits; this is used to change the files' permissions.

The three types of permission are **read** (`r`), **write** (`w`) and **execute** (`x`).

`chmod` allows the user to change the permissions in two ways - Symbolic permission and numerical (octal) permission.

**Symbolic permission:** A combination of the letters `u g o a` controls which users' access to the file will be changed: the user who owns it (`u`), other users in the file's group (`g`), other users not in the file's group (`o`), or all users (`a`) [default].

The operator `+` causes the selected file mode bits to be added to the existing file mode bits of each file; `-` causes them to be removed. 

Example:

1. Adding the execute permission for others.
    
    ```bash
    $ chmod o+x file.txt
    ```
    
2. Removing the execute permission for the user.
    
    ```bash
    $ chmod u-x file.txt
    ```
    
**Numerical (Octal) permission:** A 3-digit octal number (say `abc`) is used to specify the permissions i.e., digit `a` specifies the user permission, digit `b` specifies the group's permissions and `c` specifies other's permissions. 

3 binary digits (say `def`) are required to represent a single-digit octal number. Each digit in the binary number represents the read, write and execute permission i.e., bit `d` - read, `e` - write and `f` - execute. Refer to the below table for better understanding.

```
+-------------+--------+-------+
| Permissions | Binary | Octal |
+-------------+--------+-------+
| ---         |    000 |     0 |
| --x         |    001 |     1 |
| -w-         |    010 |     2 |
| -wx         |    011 |     3 |
| r--         |    100 |     4 |
| r-x         |    101 |     5 |
| rw-         |    110 |     6 |
| rwx         |    111 |     7 |
+-------------+--------+-------+
```

**Example:** 

1. Removing permissions for all
    
    ```bash
    $ chmod 000 file.txt
    ```
    
2. Adding `rwx` permission for user, `rx` permission for group and `x` permission for others.
    
    ```bash
    $ chmod 751 file.txt
    ```
    
### `chown`

Change file owner and group.

### `chgrp`

`chgrp` : **Change group**.

----

# File commands

### `head`

Print the first 10 lines of each file(s) to standard output. With more than one file , precede each with a header giving the file name.

**Syntax:** `head [option] files`

Example: 

1. Simple usage of `head`. This example shows `head` outputting 10 lines.
    
    ```bash
    /var/log$ head dpkg.log
    2020-04-16 16:06:48 startup packages remove
    2020-04-16 16:06:48 status installed linux-virtual:amd64 4.15.0.96.87
    2020-04-16 16:06:48 remove linux-virtual:amd64 4.15.0.96.87 <none>
    2020-04-16 16:06:48 status half-configured linux-virtual:amd64 4.15.0.96.87
    2020-04-16 16:06:48 status half-installed linux-virtual:amd64 4.15.0.96.87
    2020-04-16 16:06:48 status config-files linux-virtual:amd64 4.15.0.96.87
    2020-04-16 16:06:48 status config-files linux-virtual:amd64 4.15.0.96.87
    2020-04-16 16:06:48 status config-files linux-virtual:amd64 4.15.0.96.87
    2020-04-16 16:06:48 status not-installed linux-virtual:amd64 <none>
    2020-04-16 16:06:48 status installed linux-headers-virtual:amd64 4.15.0.96.87
    ```
    
2. Use `-n` command to specify the number of lines to print. We print 3 lines in this example. 
    
    ```bash
    /var/log$ head -n3 dpkg.log
    2020-04-16 16:06:48 startup packages remove
    2020-04-16 16:06:48 status installed linux-virtual:amd64 4.15.0.96.87
    2020-04-16 16:06:48 remove linux-virtual:amd64 4.15.0.96.87 <none>
    ```
    
    > 💡 The `n` in the option can be skipped and only the number can be written.
    
3. A useful option is `-f` or `--follow` which is used to follow the file. As the file grows the new lines of the file will be displayed on the output.search for files in a directory hierarchy

### `tail`

Print the last 10 lines of each file(s) to standard output. With more than one file, precede each with a header giving the file name.

The options available for both `head` and `tail` are similar.

### `find`

Search for files in a directory hierarchy. Wild cards can be used while searching for files.

**Syntax:** `find [option] filename`

**Example:** 

1. Searching for log files.
    
    ```bash
    /var/log$ find *.log
    alternatives.log
    dpkg.log
    ```

### `wc`

Print newline, word, and byte (in this order) counts for each file.

**Syntax:** `wc [option] [file]`

**Example:**

1. Simple use of `wc`
    
    ```bash
    /var/log$ wc dpkg.log
      785  4698 55825 dpkg.log
    ```
    
2. Use `-c` or `--bytes` to get the byte count.
    
    ```bash
    /var/log$ wc -c dpkg.log
    55825 dpkg.log
    ```
    
3. Use `-l` or `--lines` to get the newline count.
    
    ```bash
    /var/log$ wc -l dpkg.log
    785 dpkg.log
    ```
    
4. Use `-w` or `--words` to get the word count.
    
    ```bash
    /var/log$ wc -w dpkg.log
    4698 dpkg.log
    ```

### `cmp`

Compares two files byte by byte and reports the location of the first difference between them.

**Syntax:** `cmp file1 file2`

**Example:**

```bash
$ cmp alternatives.log dpkg.log
alternatives.log dpkg.log differ: byte 1, line 1
```

### `diff`

`diff` : Compares two files line by line and reports all the differences between them.

**Syntax:** `diff file1 file 2`

**Example:** 

```bash
$ diff alternatives.log  dpkg.log
1,4c1,785
< update-alternatives 2020-04-16 16:26:05: run with --install /usr/bin/x-www-browser x-www-browser /usr/bin/wslview 30
< update-alternatives 2020-04-16 16:26:05: link group x-www-browser updated to point to /usr/bin/wslview
< update-alternatives 2020-04-16 16:26:05: run with --install /usr/bin/www-browser www-browser /usr/bin/wslview 30
< update-alternatives 2020-04-16 16:26:05: link group www-browser updated to point to /usr/bin/wslview
---
> 2020-04-16 16:06:48 startup packages remove
> 2020-04-16 16:06:48 status installed linux-virtual:amd64 4.15.0.96.87
...
...
...
```

----

# User & Group management and Superuser

### `useradd`

Create a new user or update default new user information. By default the new user will have no password; to provide a password use the `passwd` command along with the username,

**Syntax**: `useradd [option] username`

**Example**: Creating a user named `mark`. We provide a default home directory for the user (`-m`)  and assign the default shell (`-s`) .

```bash
$ sudo useradd mark -m -s /bin/bash
```

### `userdel`

Delete a user account and related files.

**Syntax:** `userdel [option] username`

**Options:**

1. Use the `-r` or `--remove` option to delete the files in the user's home directory and the home directory itself.
2. User `-f` or `--force` to force remove a user. It deletes all the user's files in the home directory and the home directory itself.

### `groups`

Print the grops a user is in.

**Syntax:** `groups [option] username`

**Example:**

```bash
$ groups shathin
shathin : shathin adm dialout cdrom floppy sudo audio dip video plugdev netdev
```

> 💡 Use `cat /etc/group` command to list all the groups in the linux system.

### `groupadd`

Create a new group.

**Syntax:** `groupadd [option] groupname`


### `groupdel`

Delete a group.

**Syntax**: `groupdel [option] groupname`

### `gpasswd`

Adminisiter `/etc/group` and `/etc/gshadow`. This command is used to add / delete a user to / from a group.

**Syntax:** `gpasswd [option] group`

**Example:** 

1. Add user `Ryu` to `Valorant` group
    
    ```bash
    $ gpasswd -a Ryu Valorant
    ```
    
2. Remove user `Ryu` from `Valorant` group
    
    ```bash
    $ gpasswd -d Ryu Valorant
    ```  

### `passwd`

Change user password. If the username is not specified then a prompt to change the password for the current will be displayed. 

Note that the password will not be displayed while typing

**Syntax**: `passwd [option] [username]`

Example:

```bash
$ passwd 
Changing password for shathin.
(current) UNIX password:
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

> 💡 User information and password is stored in `/etc/passwd` and `/etc/shadow` respectively.

### `sudo`

`sudo` allows a permitted user to execute a command as the superuser or another user, as specified by the security policy.

**Syntax:** `sudo command`


### `su`

----

# Viewing Processes & Resources 

## Processes

### `ps`

Display all currently active processes.

1. To get a list of all the processes and their PIDs :
    1. For the current user - `ps -ux`
    2. For all the users - `ps -aux`
2. To get the info of a particular process use `ps -C process-name`

### `top`

Display Linux processes.

**Syntax**: `top`

**Example**: 

```bash
$ top
top - 07:37:31 up 52 min,  0 users,  load average: 0.52, 0.58, 0.59
Tasks:   4 total,   1 running,   3 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.4 us, 13.3 sy,  0.0 ni, 83.1 id,  0.0 wa,  1.2 hi,  0.0 si,  0.0 st
KiB Mem :  8276908 total,  3993960 free,  4053596 used,   229352 buff/cache
KiB Swap: 25165824 total, 24881392 free,   284432 used.  4089580 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
  221 shathin   20   0   17624   2076   1504 R 100.0  0.0   0:00.03 top
    1 root      20   0    8936    304    260 S   0.0  0.0   0:00.11 init
    7 root      20   0    8936    212    168 S   0.0  0.0   0:00.01 init
    8 shathin   20   0   16784   3428   3316 S   0.0  0.0   0:00.58 bash
```

- `PID` is the process ID. This is unique to every process in the system.
- `USER` specifies which the user the process belongs to.
- `COMMAND` specifies the command / process name.

Keys that provide functionality within the `top` window: 

- Press `s` key when to change the delay (in seconds) of refreshing the information.
- Press `i` key filter out idle processes.
- Press `k` to kill a process. When the key is pressed a prompt appears asking for the `PID` of the process to be killed.

### `htop`

Interactive process viewer.

**Syntax:** `htop`

**Example:** 

![Image of htop command output](/assets/htop_1.png)

### `kill`

Send a signal to a process. The default signal (i.e., without specifying the signal using `-s` option) is `TERM` or terminate signal.

> 💡 Use the `pidof` command to get the `PID` of a process if you know the name of that process.

**Syntax**: `kill [option] <pid>[...]`

Send signal to every `pid` listed in `[...]`.

**Example**: 

1. Killing / terminating a process using `kill`
    
    ```bash
    $ kill 3005
    ```
    
2. If the default `SIGTERM` cannot terminate a process then `-SIGKILL` or `-9` or `-KILL` flags can be specified to force ther termination.
    
    ```bash
    $ kill -KILL 3294
    ```

## Resources

### `df`

Report file system disk space usage.

**Syntax:** `df [option] [file]`

**Example**: 

1.  Simple usage of `df`. We use the `-h` option to make the output look human readable i.e., in terms of KB, MB or GB.
    
    ```bash
    $ df -h
    Filesystem      Size  Used Avail Use% Mounted on
    rootfs          220G  129G   92G  59% /
    none            220G  129G   92G  59% /dev
    none            220G  129G   92G  59% /run
    none            220G  129G   92G  59% /run/lock
    none            220G  129G   92G  59% /run/shm
    none            220G  129G   92G  59% /run/user
    tmpfs           220G  129G   92G  59% /sys/fs/cgroup
    C:\             220G  129G   92G  59% /mnt/c
    G:\             631G   27G  605G   5% /mnt/g
    ```

### `du`

Estimate file space usage.

**Syntax:** `du [option] [file]`

**Example:** 

1. Using `du -h` to obtain the file space usage of directory. (In this example we navigate into the directory and execute the command)
    
    ```bash
    java-programming$ du -h
    4.0K       ./BalancedParanthesis
    0          ./FindTheWinner
    4.0K       ./GarbageCollection
    20K        ./HomegrownStack
    4.0K       ./UniqueID
    32K        .
    ```
    
    Alternatively, we execute the command without navigating into the directory and instead pass the name of the directory / file  to command.
    
2. If we only want the summary i.e., the total size of a directory we can use the `-s` command.
    
    ```bash
    java-programming$ du -sh
    32K     .Display amount of free and used memory in the system
    ```

### `free`

Display amount of free and used memory in the system.

**Syntax:** `free [option]`

**Example:** 

1. Simple usage of `free -h`
    
    ```bash
    $ free -h
            total    used    free   shared  buff/cache   available
    Mem:     7.9G    3.7G    4.0G      17M        223M        4.1G
    Swap:     24G    101M    23G
    ```
    
----

# Archival and Compression

### `tar`

An **archiving** utility. `tar` stands for tape archive.

**Syntax:** `tar [options] [archive] [file]`

**Example:** 

1. Using the `-cvf` option to archive a file. The `-c` option is used to create the archive, `-v` displays a verbose message about the process and `-f` is used when the user wants to specify the name of the archive file.
    
    ```bash
    $ tar -cvf java.tar java-programming/
    java-programming/
    java-programming/BalancedParanthesis/
    java-programming/BalancedParanthesis/BalancedParanthesis.java
    java-programming/FindTheWinner/
    java-programming/FindTheWinner/FindTheWinner.java
    java-programming/GarbageCollection/
    java-programming/GarbageCollection/GarbageCollection.java
    java-programming/HomegrownStack/
    java-programming/HomegrownStack/HomegrownStack.java
    java-programming/UniqueID/
    java-programming/UniqueID/UniqueID.java
    ```
    
2. Using the `-xvf` to extract a archive file. The `-x` option is used to specify that we want to extract the archive.
    
    ```bash
    $ tar -xvf java.tar
    java-programming/
    java-programming/BalancedParanthesis/
    java-programming/BalancedParanthesis/BalancedParanthesis.java
    java-programming/FindTheWinner/
    java-programming/FindTheWinner/FindTheWinner.java
    java-programming/GarbageCollection/
    java-programming/GarbageCollection/GarbageCollection.java
    java-programming/HomegrownStack/
    java-programming/HomegrownStack/HomegrownStack.java
    java-programming/UniqueID/
    java-programming/UniqueID/UniqueID.java
    ```
    
3. Compressing an archive into `.gz` format using `-z` command. 
    
    ```bash
    $ tar -czf java.tar.gz java-programming/
    
    $ ls
    java.tar.gz
    ```
    

### `gzip` & `gunzip`

Used for compressing a file. You can use `gzip` for both compression and decompression and use `gunzip` for decompression.

**Syntax for `gzip`**: `gzip [option] filename`

**Syntax for `gunzip`**: `gunzip [option] filename`

**Example**: 

1. Compressing using `gzip`
    
    ```bash
    $ ls
    file.txt
    
    $ gzip file.txt
    
    $ ls
    file.txt.gz
    ```
    
2. Decompressing using `gzip` using `-d` option.
    
    ```bash
    $ gzip -d file.txt.gz
    
    $ ls
    file.txt
    ```
    
3. Decompressing using `gunzip`
    
    ```bash
    $ gunzip file.txt
    
    $ ls
    file.txt
    ```
    
----

# Network Commands

### `ifconfig`

Configure a network interface.

**Syntax:** `ifconfig [option] [interface]`

**Example:** 

1. Using `ifconfig` to view all the newtork interfaces.
    
    ```bash
    $ ifconfig
    eth0: flags=64<RUNNING>  mtu 1500
            inet 169.254.25.13  netmask 255.255.0.0
            inet6 fe80::4928:c109:790e:190d  prefixlen 64  scopeid 0xfd<compat,link,site,host>
            ether 30:e1:71:9a:51:e1  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ....
    ```
    
2. Using `ifconfig` to enable (`up`) or disable (`down`) a network interface.
    
    ```bash
    $ ifconfig etho0 down
    $ ifconfig eth0 up
    ```

----

# Date, Calendar & other Miscellenous Commands

## Date & Calendar

### `date`

Print or set the system date and time.

**Example**: 

1. Simple usage of `date` to display current date & time.
    
    ```bash
    $ date
    Fri Aug 21 18:25:31 IST 2020
    ```
    
2. Set system time using `-s` or `--set`command.
    
    ```bash
    $ date -s "11/20/2021 12:30:00"
    ```
    
3. Format the date that is printed using the following
    
    ```bash
    +----------------+------------------------------------+
    | Format         | Specifies                          |
    +----------------+------------------------------------+
    | +%m            | Month number                       |
    | +%h            | Abbrivieated month (Jan, Feb, etc) |
    | +%B            | Full month name                    |
    | +%d            | Day of the month                   |
    | +%y            | Year                               |
    | +%H, +%M & +%S | Hour, minute & seconds             |
    | +%D            | Date as mm/dd/yy                   |
    | +%T            | Time as hh:mm:ss                   |
    +----------------+------------------------------------+
    ```
    
    ```bash
    $ date "+%d-%h-%y"
    21-Aug-20 
    ```

### `cal`

Displays a calendar.

> 💡 Use `ncal` for an alternative layout.

**Example**:

1. Simple use of `cal`
    
    ```bash
    $ cal
        August 2020
    Su Mo Tu We Th Fr Sa
                       1
     2  3  4  5  6  7  8
     9 10 11 12 13 14 15
    16 17 18 19 20 21 22
    23 24 25 26 27 28 29
    30 31 
    ```
    
2. Use `-y` to display the calendar of the specified year.
3. Use `-m` to display the calendar of the specified month (month is a decimal number).

## Miscellaneous

### `alias`

Define or display aliases. Without arguments, alias' prints the list of aliases in the reusable form alias `NAME=VALUE` on standard output.

**Syntax:** `alias [-p] [name=value]`

**Example:**

```bash
$ alias longlist="ls -l"
```

### `uptime`

Tell how long the system has been running.

Example:

```bash
$ uptime
 20:37:04 up  4:36,  0 users,  load average: 0.52, 0.58, 0.59
```

### `w`

Show who is logged on and what they are doing.

**Example:**

```bash
$ w 
07:36:17 up  2:21,  1 user,  load average: 1.73, 1.06, 0.82
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
shathin  :0       :0               05:15   ?xdm?   1:12m  0.01s /usr/lib/gdm3/gdm-x-session
```

### `whoami`

Who are you logged in as.

**Example:** 

```bash
$ whoami
shathin
```


### `uname`

`uname` : About kernel

Examples: 

1. Simple use of `uname`
    
    ```bash
    $ uname
    Linux
    ```
    
2. Show kernel information using `-a` 
    
    ```bash
    $ uname -a
    Linux Shathin 4.4.0-19041-Microsoft #1-Microsoft Fri Dec 06 14:06:00 PST 2019 x86_64 x86_64 x86_64 GNU/Linux
    ```
    

3. Show kernel version using `-r`

```bash
$ uname -r
4.4.0-19041-Microsoft
```

## Locating Commands

### `which`

Locate a command(s). 

**Syntax:** `which [-a] filename`

Example:

1. Locating the `ls` command
    
    ```
    $ which ls
    /bin/ls
    ```
    
2. Locating multiple commands
    
    ```
    $ which cat echo mkdir
    /bin/cat
    /bin/echo
    /bin/mkdir
    ```
    
### `whereis`

Locate the binary, source, and manual page files for a command

**Syntax:** `whereis [option] command`

**Example**: 

```
$ whereis cat
cat: /bin/cat /usr/share/man/man1/cat.1.gz
```
